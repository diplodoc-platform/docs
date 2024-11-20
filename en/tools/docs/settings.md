# Build settings

The build settings are listed below. You can configure them and [standard YFM settings](../../settings.md) in one of the following ways:

* Using startup keys when executing the `yfm` command.
* In a [configuration file](../../project/config.md).

The name of the startup key corresponds to the name of the setting.

| Startup key                 | Description |
|-----------------------------| --- |
| `--input, -i`               | Path to the project directory (required parameter). |
| `--output, -o`              | The path to the folder for output data (required parameter). |
| `--varsPreset`              | Name of the [variable preset](../../project/presets.md) used. |
| `--vars, -v`                | Values of [variables](../../syntax/vars.md). |
| `--strict, -s`              | Launch in strict mode.</br></br>YFM warnings are treated as errors. Disabled by default. |
| `--quiet, -q`               | Start in quiet mode.</br></br>Do not output logs to stdout. Disabled by default. |
| `--config, -c`              | Path to the [configuration file](../../project/config.md). |
| `--singlePage`              | Build the project as a single HTML file. For more information, see [Single-page build](./singlepage.md). |
| `--output-format`           | Generation format. HTML by default, but you can choose to [build in YFM](build.md#yfm). |
| `--apply-presets`           | Substitute variable values from presets when building in YFM. |
| `--add-system-meta`         | Add variables from the system presets section to [metadata](../../syntax/meta.md#meta) files. Disabled by default. |
| `--remove-hidden-toc-items` | Remove hidden pages from the build result. Disabled by default. |
| `--version`                 | Current version. |
| `--lint-disabled`           | Should whether to turn off a linter |
| `--build-disabled`          | Should whether to turn off a build |
| `--add-map-file`            | Should add all paths of documentation into file.json. Disabled by default. |
| `--included`                | Activation of gluing all dependencies of md files into 1 file to speed up display, more details in the section [Gluing dependencies](./included.md) of files. Disabled by default. |

To view the full list of keys, run the `yfm --help` command.
