# Rendering a single file

The `yfm content` command processes a **single** Markdown file and prints the result to `stdout` (or writes it to a file). Unlike [`yfm build`](build.md), it does not traverse the whole project and does not produce a full page: for the `html` format it emits only the **content fragment** — without the table of contents, header, or page chrome.

The command is handy when you need the preprocessed content of a single file quickly — for example, to pipe it into another tool, render a preview in an editor, or use it in your own pipeline.

## Usage {#usage}

```shell
# self-contained markdown to stdout
yfm content -i ./page.md -f md

# html content fragment into a file
yfm content -i ./page.md -f html -o ./page.html
```

Run `yfm content --help` to see the full list of options.

## Output format {#output-format}

The format is set with the `--output-format` (`-f`) option:

* `md` — self-contained Markdown: [includes](../../syntax/includes.md) and autotitles are merged into the file, and frontmatter is added. This is the default for a single file.
* `html` — the content HTML fragment only (no toc, header, or page chrome).

The same transformations as in a [YFM → YFM build](build.md) are applied: visibility conditions, [variable substitutions](../../syntax/vars.md), inline SVG, and heading substitutions.

## Project root {#project-root}

Presets (`presets.yaml`), includes, links, and variables are resolved relative to a project root:

* by default the root is the **current working directory**;
* pass `--config` (`-c`) with a path to a `.yfm` file — its directory becomes the root.

{% note info %}

If the processed file lives outside the chosen root, the file's own directory becomes the root, so includes and presets resolve correctly.

{% endnote %}

## Output streams {#streams}

Warnings and errors are always written to `stderr`. On any build error the process exits with a non-zero code.

By default the rendered content is printed to `stdout` wrapped in delimiter markers so it can be extracted from the surrounding output (version line, build timer):

```
<<<<<< YFM CONTENT START >>>>>>
...content...
<<<<<< YFM CONTENT END >>>>>>
```

When `--output` (`-o`) is used, the result is written to the file raw — without the markers.

## `--raw` mode {#raw}

The `--raw` flag prints **only** the content to `stdout` — without the delimiter markers and without the framework banners (version line, build timer, completion banner). This is useful when piping the result straight to a file or another tool:

```shell
yfm content -i ./page.md -f md --raw > page.md
```

Diagnostics (warnings, errors) still go to `stderr`, and the exit code stays non-zero on error, so `stdout` carries valid content only.

`--raw` has no effect together with `-o`: file output is always raw.

## Watch mode {#watch}

{% note info "Beta feature" %}

If you run into problems, please report them via [GitHub issues](https://github.com/diplodoc-platform/cli/issues).

{% endnote %}

With the `--watch` (`-w`) option the command watches the input file, its includes, and presets, and re-renders the result on every save.

## Options {#options}

| Option                              | Default | Description                                                  |
| ----------------------------------- | ------- | ------------------------------------------------------------ |
| `-i, --input <file>`                | —       | Path to the Markdown file to process (required)              |
| `-o, --output <file>`               | stdout  | Write the result to a file instead of stdout                 |
| `-f, --output-format <md \| html>`  | `html`  | Output format                                                |
| `--raw`                             | `false` | Print only the content to stdout (no markers, no banners)    |
| `-w, --watch`                       | `false` | Re-render on changes to the file, its includes, and presets  |
| `-c, --config <path>`               | `.yfm`  | Config file; its directory becomes the project root          |
| `--vars-preset <name>`              | `default` | Variables preset to apply                                  |
| `-v, --vars <json>`                 | —       | Inline variables (JSON) overriding presets                   |
| `--allow-html` / `--no-allow-html`  | `true`  | Allow raw HTML in Markdown                                   |
| `--sanitize-html`                   | `true`  | Sanitize the produced HTML                                   |
| `-s, --strict`                      | `false` | Exit with a non-zero code on warnings                        |

Other options match the [build](settings.md) options.
