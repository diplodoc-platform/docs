# Documentation build parameters

The build parameters supported when running the `yfm build` command are listed below.

#|
||
**Launch flag** | **Description**
||
||
`--input, -i` | Path to the project directory. By default, the current directory.
||
||
`--output, -o` | Path to the output directory (required parameter).
||
||
`--vars-preset <name>` {#vars-preset} | Name of the [variable preset](../../project/presets.md) used.
||
||
`--vars, -v` | Values of [variables](../../syntax/vars.md).
||
||
`--strict, -s`
|
Run in strict mode.

YFM warnings are treated as errors. Disabled by default.
||
||
`--quiet, -q`
|
Run in quiet mode.

Do not output logs to stdout. Disabled by default.
||
||
`--jobs, -j`
|
Run in multithreaded mode.
If a specific number of threads is not specified, it is calculated automatically based on system parameters

`--jobs 4`, `-j4`, `-j`
||
||
`--config, -c` {#config} | Path to the [configuration file](../../settings.md).
||
||
`--extensions, -e`
|
Connecting external extensions at startup.

The path passing differs for exec flags and the .yfm configuration. For exec flags, paths are specified relative to the directory where the command is executed. For configuration, paths are passed from the configuration directory.

Example:

```bash
yfm -e @diplodoc/openapi-extension
yfm -e ./local-extension
```

||
||
`--watch, -w` | Launch [watch build mode](build.md#watch).
||
||
`--lang, --langs` | Configure supported languages.
||
||
`--output-format, -f` | Format of the final build files. Available options: `html`, `md`. By default, `html`.
||
||
`--allow-html` | Allow using HTML in markdown files.
||
||
`--sanitize-html` | Enable HTML sanitization.
||
||
`--allow-custom-resources`
|
Allow loading custom resources on statically generated pages.
||
||
`--static-content`
|
Build the article's HTML content as part of the layout. By default, it is in a JS object and is inserted into the page during rendering in the browser.
||
||
`--theme <color>` | Enable the themer. More details - [here](../../style/theme.md).
||
||
`--ignore`
|
Do not process paths matching the pattern.

Example:

```bash
build -i ./input -o ./output --ignore *.bad.md
```

or

```bash
build -i ./ -o ./build --ignore ./build
```

||
||
`--ignore-stage`
|
Do not process table of contents files with the specified level. By default, `["skip"]`.
||
||
`--template`
|
Select the operating mode for [templates](../../syntax/vars.md). By default, text mode is enabled, which ignores code blocks. Use `all` or `code` to process code blocks.

Possible values:

- `text`;

- `all`;

- `code`.
||
||
`--template-vars`
|
Toggle the processing mode for [variables](../../syntax/vars.md#subtitudes) in double curly braces. Enabled by default.
||
||
`--template-conditions`
|
Toggle the processing mode for [conditional operators](../../syntax/vars.md#conditions). Enabled by default.
||
||
`--vcs` | Enable fetching data from the VCS. This parameter only controls enabling/disabling.
Each VCS connector has its own configuration. It should be described in the connector's documentation.
||
||
`--mtimes` | Enable displaying the article modification date. The data is taken from the VCS.
||
||
`--authors` | Enable displaying the article author. The data is taken from the VCS.
||
||
`--contributors` | Enable displaying contributors in the article. The data is taken from the VCS.
||
||
`--lint` | Attach the [linter file](../../project/lint.md). Enabled by default. To disable, use `--no-lint`.
||
||
`--llms` | Enable [generation of llms.txt and llms-full.txt files](../../guides/llms.md) for the project.
||
||
`--llms-full-max-size <value>` | Limit on the size of the generated llms-full.txt file for a single article; if exceeded, filling the file with data stops with code ##YFM022## (the build does not fail with an error). Accepts numbers and strings like: ##1024##, ##512K##, ##2M##.
||
||
`--changelogs` | Beta feature. Toggle processing of the experimental changelog syntax.
||
||
 `--single-page` | Build the project as a single HTML file. See more in the [Single-page build](./singlepage.md) section.
||
||
 `--output-format` | Generation format. HTML by default, but you can configure [building in YFM](build.md#yfm).
||
||
 `--apply-presets` | Substitute variable values from presets when building in YFM.
||
||
 `--remove-hidden-toc-items` | Remove hidden pages from the build result. Disabled by default.
||
||
 `--skip-html-extension` | Remove the `.html` extension and the `index.html` file name from internal links to articles.

{% note info %}

For links without extensions to open correctly, configure the web server to handle paths without `.html` and `index.html` at the end.

{% endnote %}
||
||
 `--add-map-file` | Add creation of file.json with all paths to the documentation. Disabled by default.
||
||
 `--build-stats` {#build-stats-flag} | Write a `yfm-build-stats.json` file next to the output with build metrics (duration, page and asset counters, artifact size). See more in [Build statistics](build.md#build-stats). Enabled by default for builds with `--output-format=md`, disabled for others. To disable, use `--no-build-stats`.
||
||
 `--build-content` {#build-content-flag} | Write a `yfm-build-content.json` file next to the output with content hashes of each file and `page → assets` dependencies. Used by external tools (search reindexing, change notifications) to compute the set of pages changed between two builds. See more in [Build content map](build.md#build-content). Enabled by default for builds with `--output-format=md`, disabled for others. To disable, use `--no-build-content`.
||
||
 `--disable-csp` | Disable adding the [Content-Security-Policy](../../guides/csp.md#disable-csp) meta tag to generated HTML pages. Enabled by default.
||
||
 `--max-asset-size <value>` {#max-asset-size} | Limit on the asset size in the project; if exceeded, the build fails with the error ##YFM013##. Accepts numbers and strings like: ##1024##, ##512K##, ##2M##.

If you specify ##0##, asset size checking will not be performed.

By default, ##64M##.
||
||
 `--max-html-size <value>` {#max-html-size} | Limit on the size of the HTML content of a single article; if exceeded, the build fails with the error ##YFM012##. Accepts numbers and strings like: ##1024##, ##512K##, ##2M##.

Works only when building with `--output-format html`.

By default, ##42M##, maximum value ##96M##.
||
||
 `--max-inline-svg-size <value>` {#max-inline-svg-size} | Maximum allowed size of an SVG image at which it is [automatically inlined into the article content](../../syntax/media.md#img-inline). If the size is exceeded, the SVG image is inserted via the ##\<img\>## tag. Accepts numbers and strings like: ##1024##, ##512K##, ##2M##.

If you specify ##0##, SVG images will not be inlined during the build.

By default, ##2M##, maximum value ##16M##.
||
||
 `--max-openapi-include-size <value>` {#max-openapi-include-size} | Maximum allowed size of a file built from an [OpenAPI specification](./../../guides/openapi.md). If the file size is exceeded, the JSON schema is cut out of it. Accepts numbers and strings like: ##1024##, ##512K##, ##2M##.

If you specify ##0##, there is no limit.
||
||
 `--multiline-term-definitions` {#multiline-term-definitions} | Enables support for multiple line breaks in [tooltips](../../syntax/term.md).
||
||
 `--version` | Current version.
||
|#

To view the full list of keys, run the command `yfm build --help`.
