---
tags:
    - Build
---
# Multithreaded build

The builder can process documentation pages in parallel, in several threads. This speeds up large projects: page processing is the longest part of a build and it is CPU bound.

The mode is off by default: the build runs in a single thread.

## Enabling it {#enable}

Pass the [`--jobs`](settings.md#jobs) flag:

```shell script
# 4 worker threads
yfm build -i ./input-folder -o ./output-folder --jobs 4

# the number of threads is chosen automatically: number of cores minus one
yfm build -i ./input-folder -o ./output-folder -j
```

A value of `1` or less is equivalent to the mode being off: no worker threads are started.

How many threads to use:

* on your own machine, `-j` without a number is a good default;
* in CI, base the number on the cores available to the agent rather than on the cores of the physical machine: eight threads in a two-core container will only make the build slower;
* on a project of a few dozen pages multithreading may not pay off - starting the threads takes time by itself.

## What gets faster and what does not {#scope}

What runs in parallel is the processing of individual pages: parsing YFM, substituting variables, resolving includes, rendering the resulting file.

Everything else runs sequentially, in a single thread:

* project preparation and resolving the tables of contents;
* building the search index;
* [single-page build](singlepage.md) and PDF generation;
* writing manifests, redirects and the file map.

That is why the speedup is not proportional to the number of threads: on a project with a heavy table of contents and a large search index the gain is smaller than on a project made of many simple pages.

## Memory usage {#memory}

Every worker thread keeps its own copy of the project data, so memory usage grows with the number of threads. If the build runs out of memory, reduce the number of threads or cap each thread with the [`--worker-max-old-space`](settings.md#worker-max-old-space) flag:

```shell script
yfm build -i ./input-folder -o ./output-folder --jobs 4 --worker-max-old-space 2048
```

The value is in megabytes and applies to each thread separately.

## Limitations {#limitations}

* **[Watch mode](build.md#watch) runs in a single thread.** The initial build may use several threads, but once the builder switches to watching for changes the threads are stopped and rebuilds run sequentially.
* **File write order is not defined.** In a single threaded build pages are processed in a predictable order, in a multithreaded one they are not. This does not affect the build result, but the order of lines in the log will differ from run to run.
* **Third party extensions may not be ready for it.** An extension runs inside worker threads, and not every implementation survives that. If an extension stops working after you enable `--jobs`, compare the result with a single threaded build and see the [Multithreading and hooks](../../dev/extensions/multithreading.md) article.

## Troubleshooting {#troubleshooting}

Compare a build with `--jobs` against one without it: if the results differ, multithreading is the cause and the mode is best turned off until the reason is found.

The `Threads setup timed out` line in the log means the worker threads failed to start within 30 seconds. The build does not fail, it silently continues in a single thread. This usually indicates a lack of resources on the build machine.
