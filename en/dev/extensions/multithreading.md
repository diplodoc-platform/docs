# Multithreading

The builder can process pages in several threads. The mode is off by default and is enabled with the [`--jobs`](../../tools/docs/settings.md) flag.

| Flag | Description |
| --- | --- |
| `--jobs, -j [number]` | Build in the given number of threads. If no number is passed, `number of cores - 1` is used. A value of `1` or less does not enable multithreading. |
| `--worker-max-old-space <MB>` | Old space memory limit for each worker thread. |

## Execution model {#model}

A worker thread is not a single function executed on another core, it is a full copy of the program. Every thread parses the configuration again, loads all extensions and creates its own instances of every [service](./services.md): `markdown`, `leading`, `meta`, `vars`, `toc`, `vcs`, `search`, `redirects`.

How the work is split:

* **The main thread** resolves the table of contents, hands pages out to worker threads, collects the results and emits the final artifacts: search index, singlepage, PDF, manifests, redirects, file map.
* **Worker threads** process individual pages: they turn a markdown or a leading page into the resulting file and write it.

Exactly one thing runs in parallel - processing of a single page. Everything else stays in the main thread.

## Where each hook runs {#hooks}

With respect to multithreading, hooks fall into three groups.

### Registration hooks {#registration-hooks}

`Base.Command`, `Base.RawConfig`, `Base.Config`, `Base.BeforeAnyRun`, `Build.BeforeRun`, `Vars.PresetsLoaded`, `Markdown.Collects`, `Markdown.Plugins`, `Leading.Plugins`, `Vcs.VcsConnector`, `Search.Provider`.

These run in every thread: in the main one and in each worker. They are the points where an extension declares itself - adds a command line flag, adjusts the configuration, registers a markdown plugin, replaces the search provider, subscribes to other hooks.

{% note warning %}

A handler of such a hook is called `N + 1` times, where `N` is the number of worker threads. Side effects here - writing files, network requests, incrementing counters - happen the same number of times.

{% endnote %}

### Main thread hooks {#main-thread-hooks}

`Toc.Item`, `Toc.Includer`, `Toc.Included`, `Toc.Loaded`, `Toc.Dump`, `Toc.Filtered`, `Build.Entry`, `Build.AfterRun`, `Base.AfterAnyRun`, `Search.Page`, `Redirects.Page`, `Redirects.Release`.

These run in the main thread only, regardless of the `--jobs` value. This is the only place where project wide state can be accumulated safely.

The key hook is `Build.Entry`: it is called in the main thread once a page has been processed and receives the result of that processing. This is how the built-in features that need data about all pages at once are implemented: search, singlepage, PDF, crawler manifest, build stats.

```typescript
import {join} from 'node:path';
import {getBuildHooks} from '@diplodoc/cli';

export class Extension {
    apply(program: Build) {
        const index = new Map();

        // Called in the main thread, the state survives the build
        getBuildHooks(program)
            .Entry.for('html')
            .tap('MyExtension', (run, entry, info) => {
                index.set(entry, info.title);
            });

        getBuildHooks(program)
            .AfterRun.for('html')
            .tapPromise('MyExtension', async (run) => {
                await run.write(join(run.output, 'index.json'), JSON.stringify([...index]));
            });
    }
}
```

### Isolated hooks {#isolated-hooks}

`Markdown.Loaded`, `Markdown.Resolved`, `Markdown.Dump`, `Leading.Loaded`, `Leading.Resolved`, `Leading.Dump`, `Meta.Dump`, `Entry.Dump`, `Entry.State`, `Entry.Page`.

With `--jobs > 1` they run in a worker thread, in a single threaded build they run in the main one. A handler only sees the state of its own thread: the changes it made to services do not come back to the main thread, and data accumulated by other pages is not available to it.

What works here without reservations:

* transforming the content of the current page;
* reading source files;
* writing files to the output directory;
* logging via `run.logger`.

What does not work: accumulating state in the extension's memory expecting to read it later in the main thread. Such state must be returned through `Build.Entry` or collected again in the main thread.

## What crosses the thread boundary {#serialization}

Only serializable data is passed between threads:

* from the main thread to the workers - the resolved table of contents and VCS data (once, before processing starts), plus the path and metadata of every page;
* from a worker to the main thread - the result of processing a page: title, metadata, page data and dependency graphs;
* worker logs are merged into the common output through the `info`, `warn` and `error` channels;
* errors are passed with their message and stack preserved.

Functions, classes and closures do not cross the thread boundary. If an extension puts its own data into page metadata or into the processing result, that data must be plain objects.

The `Base.Error` hook fires in the thread where the error occurred. Errors from processing individual pages are propagated to the main thread and logged there.

## Limitations {#limitations}

* **Watch mode is single threaded.** Worker threads are stopped after the first build, incremental rebuilds run in one thread.
* **VCS data is collected in the main thread only** and is sent to the workers ready made. Version control cannot be accessed from isolated hooks.
* **Fallback to a single threaded build.** If worker threads fail to initialize within 30 seconds, the build silently continues in one thread. The log will contain the `Threads setup timed out` line.
* **File write order is not defined.** The same file can be written by different processing paths: as a page from the table of contents and as an included file. In a single threaded build the order is stable, in a multithreaded one it is not. Therefore every write path must produce the same result: write the file as a whole, with complete metadata, instead of amending it in parts.
* Multithreading pays off on CPU bound work - parsing and rendering a large number of pages. On projects with a few dozen pages the cost of starting the threads may outweigh the gain.

## What to read next {#see-also}

* [Extension Development Principles](./core-concepts.md)
* [Diplodoc Services](./services.md)
* [Documentation build settings](../../tools/docs/settings.md)
