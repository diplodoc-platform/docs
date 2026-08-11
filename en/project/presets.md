# Variable presets

Presets are sets of [variables](../syntax/vars.md) with different values.

Presets are used to maintain multiple versions of documentation with minor differences from the same source files. If the documentation contains internal information, you can [mark up the content](../syntax/vars.md) and split the information into two presets: `internal` and `external`. This will simplify the work and restrict access to confidential data. Then you will not need to store variable values in build files.

The workflow with presets:
1. Describe the presets in the `presets.yaml` file.
1. When building, specify the name of the preset to use in the [##vars-preset# parameter](../tools/docs/settings#vars-preset).

## Structure {#structure}

The `presets.yaml` file must contain the `default` preset. When computing variables, the values specified in `default` are taken into account first. Then the values from the preset passed at build startup are applied on top of them, since it has higher priority.

Variables in a preset are specified in the format `<variable name>`: `<variable value>`.

```yaml
default:
    position: Волшебник
internal:
    place: Изумрудный город
external:
    place: Страна Оз
```

## Hierarchy of preset files {#hierarchy }

You can use multiple preset files. When computing variables, those located closer to the file being converted take priority.

{% note tip %}

It is recommended to use top-level presets: those closest to the project root.

{% endnote %}

#### Example

```
input-folder
|-- .yfm
|-- toc.yaml
|-- presets.yaml # файл 2
|-- index.yaml
|-- quickstart.md
|-- pages
    |-- presets.yaml # файл 1
    |-- faq.md
    |-- how-to.md
```

When building the `faq.md` file, variable values from file No. 1 take priority over variables from file No. 2.
When building the `quickstart.md` file, only variable values from file No. 2 will be taken into account.

## Example of a local build with reuse {#reuse}

To build a document, run the command:

```
yfm build -i ./<document root directory> -o ./<directory with the build output> --vars-preset "<preset name>"
```

If your document uses variable presets, the build must be run separately for each preset.

If the document has no variable presets, the `--vars-preset` flag does not need to be used. In this case, the document will be built with the `default` preset value.

The build output directory will contain one folder with files in the `.html` format for the selected preset. If you run the build with different values into the same directory, the files will be overwritten.

