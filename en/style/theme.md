# Theming

Theming configures the visual appearance of the documentation.

You can manage the documentation theme using the configuration file `theme.yaml` in the project root, during build using the flag `--theme`, or in the root section of `.yfm`.

## Defining the theme in the configuration file {#config}

### File structure {#config-structure}

The configuration file `theme.yaml` sets the color palette of your documentation. A color can be defined both globally for the light and dark themes, and separately for each.

Parameters specified in the `light` or `dark` sections take precedence over global values. If a variable is defined both in the main section and in the `light` or `dark` section, the value of the specific theme will be used.

A color can be specified in the format `rgb`, `rgba`, `hex`, `hsl`, `hsla`, or as a color name. 

Example of a configuration file:

```yaml
base-brand: rgb(152 223 37)
link: red

light:
    link: rgb(0 255 170)
    quote: rgb(255 0 255)

dark:
    quote: rgba(0, 208, 255, 1)
    base-background: hsl(30 46% 41%)
```

### Parameter base-brand {#base-brand}

The `base-brand` parameter is the main accent color of the theme. The following dependent parameters are automatically determined from the value of `base-brand`:

* `base-selection`
* `link`
* `link-hover`
* `tab-active`
* `tab-text`
* `tab-text-hover`
* `quote`

Any variable value automatically calculated from the main accent color can be manually overridden in the configuration.

### Parameters {#config-options}

All possible parameters are listed below.

Parameters | Description
--- | --- 
`base-brand`| The main accent color. The color of tabs, quotes, and active switches.
`base-background`| Page background.
`base-selection`| The selected page in the table of contents and the selected dropdown item.
`base-simple-hover`| Color when hovering over interface elements.
`quote`| Quote color.
`tab-active`| Active tab color.
`tab-text`| Tab text color.
`tab-text-hover`| Tab text color on hover.
`link`| Link color.
`link-hover`| Color of links, tab text, radio buttons, and accordion items on hover.
`term-dfn-background`| Background of tooltips.
`text-primary`| Main text, text in tables.
`text-secondary`| Color of secondary text. Table of contents items, settings, language icons, etc.
`line-generic`| Color of lines between page elements, external table borders, the common tab line, and the common article table of contents line.
`code`| Text color in a code block.
`code-background`| Background of a code block.
`inline-code`| Text color in a code fragment.
`inline-code-background`| Background of a code fragment.
`table`| Text color in a table.
`table-background`| Table background.
`table-row-background`| Background color of highlighted table rows.
`table-border`| Table border.
`note-info-background`| Background color in the "Note" notice and in a notice with a custom title.
`note-tip-background`| Background color in the "Tip" notice.
`note-warning-background`| Background color in the "Important" note.
`note-important-background`| Background color in the "Warning" note.
`mini-toc-border` | Color of the article table of contents general line.
`mini-toc` | Text color of the article table of contents.
`mini-toc-hover` | Text color of the article table of contents on hover.
`mini-toc-active` | Text color of the active item in the article table of contents.
`mini-toc-active-border` | Line color of the active item in the article table of contents.

> See also: [Ajv schema of the themizer configuration theme.yaml](https://raw.githubusercontent.com/diplodoc-platform/ajv/refs/heads/master/src/json/theme-schema.json)

## Defining base-brand during build {#build}

If there is no configuration file, the base-brand color can be set using the launch key `--theme`

For example:

```shell
yfm build -i ./input-folder -o ./output-folder --theme green
```

The base-brand color can also be set using a setting in the root section of `.yfm`.

For example:

```shell
theme: green
```

If both the setting in `.yfm` and the flag `--theme` are set simultaneously, the flag takes priority.

If both the configuration file and the flag `--theme` are set simultaneously, the flag will override the `base-brand` parameter only in the main section of the configuration file. Values in the `light` and `dark` sections remain unchanged.