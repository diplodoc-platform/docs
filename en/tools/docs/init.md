# Creating a project

You can create a documentation project using the `yfm init` command.

By default, the command runs *interactive mode* for entering parameters — project settings are specified sequentially.

When passing `--skip-interactive`, *manual mode* is launched, in which the following parameters are available:

* `--output, -o` — path to the output directory (by default, the current folder);
* `--langs languages` — a comma-separated list of documentation languages (by default, "en");
* `--default-lang language` — the default language (if not specified, the first one from the `langs` list is used);
* `--name name` — the project name, inserted into the table of contents title (by default, the name of the project directory);
* `--header` — enable [extended navigation](../../project/navigation.md) in the project;
* `--force` — overwrite the folder contents if it contains files;
* `--template template` — the template of the project to create: `minimal` (by default) or `full`;
* `--dry-run` — only show what will be created as a result of the call, instead of creating the project.

```shell script
# example of a call without interactive mode
yfm init --skip-interactive -o ./output-folder --name example --langs ru,en
```

The current list of initialization parameters can be displayed in the console using the `yfm init --help` command.
