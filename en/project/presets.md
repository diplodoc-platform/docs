# Variable presets

Presets are groups of [variables](../syntax/vars.md) with different values.

Presets are used to support multiple documentation versions from the same source files. For example, if the documentation contains internal information, you can create two presets: `internal` and `external`, and you won't need to store the variable values in the build files.

How to work with presets:

1. Describe the presets in `presets.yaml`.
1. When [building](../tools/docs/index.md), specify the name of the preset used in the `varsPreset` parameter.

## Structure {#structure}

The `presets.yaml` file should contain a `default` preset. When calculating variables, the values specified in `default` are taken into account first. Then the values from the preset passed at the start of the build override them, since it takes priority.

```yaml
default:
    position: The Wizard
internal:
    place: Emerald City
external:
    place: The Land of Oz
```

## Hierarchy of preset files {#hierarchy }

You can use multiple preset files. When calculating variables, the ones that are closer to the converted file will have higher priority.

{% note tip %}

We recommend using top-level presets: the ones closest to the root of the project.

{% endnote %}

#### Example

```
input-folder
|-- .yfm
|-- toc.yaml
|-- presets.yaml // 2
|-- index.yaml
|-- quickstart.md
|-- pages
    |-- presets.yaml // 1
    |-- faq.md
    |-- how-to.md
```

* When building a file named `faq.md`, the variable values declared in file 1 take priority over file 2.
* When building `quickstart.md`, only the variable values declared in file 2 are taken into account.

