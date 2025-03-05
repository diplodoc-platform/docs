# Themization

## Defining the theme in the configuration file
### File structure
The `theme.yaml` configuration file define the color palette of your documentation. The color can be defined for both a light and a dark theme in general, or separately for each.
The parameters specified in the `light` or `dark` sections has priority over the general values. So if a variable is defined both in the general section and in the `light` or `dark` section, then the value of a specific section will be used.
The color can be set in the format `rgb`, `rgba`, `hex`, `hsl`, `hsla` or the color name. 

Example of configuration file:
```yaml
base-brand: rgb(152, 223, 37)
text-link: red

light:
    text-link: rgb(0, 255, 170)
    quote: rgb(255, 0, 255)

dark:
    quote: rgba(0, 208, 255, 0.33)
    base-background: hsl(30, 46, 41)
```

### base-brand parameter
The `base-brand` parameter is the main accent color of the theme. The following dependent parameters are automatically determined from the `base-brand` value:

* `base-selection`
* `text-link`
* `text-link-hover`
* `tab`
* `tab-text-hover`
* `quote`

Any variable value that is automatically calculated from the main accent color can be manually redefined in the configuration.
### Parameters
All possible parameters are listed below.
Parameter | Description
--- | --- 
`base-brand`| The main accent color. The color of tabs, quotes, and active switches. The colors `base-selection`, `text-link`, `text-link-hover`, `tab`, `tab-text-hover` and `quote` are automatically determined relative to it.
`base-background`| Page background.
`base-selection`| The selected page in the table of contents and the selected dropdown point. Depends on the `base-brand`.
`base-misc-light`| Background of code fragments in the text and large blocks of code
`base-generic`| The color of the highlighted rows in tables, buttons, and search bar
`base-generic-hover`| The color of the hovered buttons.
`quote`| The color of the quotes. Higher priority than `base-brand`.
`tab`| Tab line color.  Higher priority than `base-brand`
`tab-text-hover`| The color of the tab text when hovering over it.  Higher priority than `text-link`
`popup-background`| Background of popup
`popup-border`| Border of popup
`text-link`| Link color. Depends on the `base-brand`.
`text-link-hover`| The color of the hovered links, tab text, radio buttons, and the accordion. Depends on the `base-brand`.
`text-primary`| Primary text, text in tables.
`text-secondary`|Secondary text. The points of the table of contents, the icons of settings, language, etc.
`text-complementary`| The color of the text in the code block and the table of contents items when hovering over. Depends on the `base-brand`.
`text-hint`| "Previous" and "Next" at the bottom of the page
`line-generic`| The color of the line between the page elements, the outer borders of the table, the general line of tabs, the general line of the article content.
`simple-hover`| The color when hovering over the page in the table of contents, the selected dropdown point, on the icons of settings, language, etc.
`code`| The color of the text in the code block. Higher priority than `text-complementary`.
`code-background`| Background of the code block.
`inline-code`| The color of the text in the code snippet.
`inline-code-background`| Background of the code fragment.
`table`| The color of the text in the table. Higher priority than `text-primary`.
`table-background`| Table background.
`table-row-background`| The background color of the highlighted rows of the table.
`table-table-outer-border`| The frame of the table.
`table-table-inner-border`| The internal framework of the table.
`note-info`| The color of the icon in the "Note" and the note with its own header.
`note-info-background`| Background color in the "Note" and the note with its  own header.
`note-info-border`| The frame in the "Note" and the note with its own title
`note-tip`| The color of the icon in the "Tip" note
`note-tip-background`| Background color in the "Tip" note
`note-tip-border`| The frame in the "Tip" note
`note-warning`| The color of the icon in the "Warning" note
`note-warning-background`| Background color in the "Warning" note
`note-warning-border`| The frame in the "Warning" note
`note-important`| The color of the icon in the "Alert" note
`note-important-background`| Background color in the "Alert" note
`note-important-border`| The frame in the "Alert" note
`mini-toc-border` | The color of mini-toc. Higher priority than`line-generic`.
`mini-toc` | The color of text in mini-toc.  Higher priority than `text-secondary`.
`mini-toc-hover` | The color of hovered text in mini-toc.  Higher priority than `text-complementary`.
`mini-toc-active`, | The color of text in active item in mini-toc.  Higher priority than `text-primary`.
`mini-toc-active-border` | The color of line in active item in mini-toc.  Higher priority than `text-primary`.


## Defining the base-brand in the sturtup
If there is no configuration file, the base-brand color can be set using the startup key `--theme`

For example:
```shell
yfm -i ./input-folder -o ./ouput-folder --theme 'rgb(152, 223, 37)'
```