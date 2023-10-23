# Build

The [package](https://www.npmjs.com/package/@doc-tools/docs) provides the `yfm` CLI command.

## HTML {#html}

Default output format of the builder is html

To start rendering, run the command specifying the required [startup keys](settings.md):

* `--input, -i`: The path to the project folder.
* `--output, -o`: The path to the folder for output data (static HTMLs).

```shell script
yfm -i ./input-folder -o ./ouput-folder
```

## YFM {#yfm}

You can choose to build project in YFM.

To do this, when executing the `yfm` command, specify the startup key `--output-format=md`.

Building in YFM allows you to use:

* [Inserts](../../project/toc.md#includes) and [section visibility conditions](../../project/toc.md#when) in tables of contents files.
* [Content visibility conditions](../../syntax/vars.md#conditions) on document pages.
* [Variable substitutions](../../syntax/vars.md#subtitudes) if the `apply-presets` parameter is specified.

Use this type of build to support multiple document versions for different users. For example, if there are sections with internal information in the documentation, you can keep two repositories: private and public, and synchronize private with public using conditions.
