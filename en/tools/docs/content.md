# Building a single file

The command `yfm content` processes **a single** md file and outputs the result to `stdout` (or writes it to a file). Unlike [`yfm build`](build.md), it does not build a full page: for the `html` format, only the **content** is output — without a table of contents, header, or page wrapper.

The command is convenient when you need to quickly get preprocessed content of a single file — for example, to pass it to another tool, render a preview in an editor, or use it in your own pipeline.

## Usage {#usage}

```shell
# self-contained markdown in stdout
yfm content -i ./page.md -f md

# html fragment to a file
yfm content -i ./page.md -f html -o ./page.html
```

The full list of parameters can be displayed in the console with the command `yfm content --help`.

## Output format {#output-format}

The format is set by the parameter `--output-format` (`-f`):

* `md` — preprocessed Markdown. Default for a single file.
* `html` — HTML content of the page (without a table of contents, header, or wrapper).

The same transformations are applied as in [YFM → YFM build](build.md#yfm): visibility condition checks, [variable substitution](../../syntax/vars.md#subtitudes), [SVG inlining](../../syntax/media.md#img-inline), [title insertion](../../syntax/links.md#autotitle), and [content from files](../../syntax/includes.md).

## Project root {#project-root}

Presets (`presets.yaml`), [includes](../../syntax/includes.md), links, and [variables](../../syntax/vars.md) are searched relative to the project root:

* by default, the **current working directory** is considered the root;
* pass `--config` (`-c`) with a path to `.yfm` — the directory of this file will become the root.

{% note info %}

If the processed file is located outside the selected root, the directory of the file itself becomes the root.

{% endnote %}

## Output streams {#streams}

Warnings and errors are always written to `stderr`. On any build error, the process exits with a non-zero return code.

By default, the built content is output to `stdout`, framed with delimiter markers so it can be separated from accompanying output (version line, build timer):

```
<<<<<< YFM CONTENT START >>>>>>
...контент...
<<<<<< YFM CONTENT END >>>>>>
```

When using `--output` (`-o`), the result is written to a file "raw" — without markers.

## The `--raw mode` {#raw}

The `--raw` flag outputs **only** the content to `stdout` — without delimiter markers and without framework banners (version line, build timer, completion banner). This is convenient when the result needs to be directed straight to a file or another tool.

```shell
yfm content -i ./page.md -f md --raw > page.md
```

At the same time, diagnostics (warnings, errors) still go to `stderr`, and the exit code remains non-zero on error — so `stdout` contains only valid content.

Together with the `-o` flag, the `--raw` flag changes nothing: the file always receives "raw" content.

## Watch mode {#watch}

With the `--watch` (`-w`) parameter, the command tracks changes to the input file, its includes, and presets, and redraws the result on every save.

## Parameters {#options}

| Parameter                            | Default | Description                                                       |
| ----------------------------------- | ------------ | -------------------------------------------------------------- |
| `-i, --input <file>`                | —            | Path to the md file to process (required)          |
| `-o, --output <file>`               | stdout       | Write the result to a file instead of stdout                        |
| `-f, --output-format <md \| html>`  | `html`       | Output format                                                  |
| `--raw`                             | `false`      | Output only content to stdout (without markers and banners)     |
| `-w, --watch`                       | `false`      | Rebuild when the file, its includes, or presets change         |
| `-c, --config <path>`               | `.yfm`       | Configuration file; its directory becomes the project root    |
| `--vars-preset <name>`              | `default`    | Variable preset to apply                                  |
| `-v, --vars <json>`                 | —            | Inline variables (JSON) that override presets             |
| `--allow-html` / `--no-allow-html`  | `true`       | Allow raw HTML in Markdown                              |
| `--sanitize-html`                   | `true`       | Sanitize the resulting HTML                                 |
| `-s, --strict`                      | `false`      | Exit with a non-zero code on warnings              |

The remaining parameters match those of [build](settings.md).
