#|
|| Plugin name | Description | Parameters | Enabled by default |
|| **Anchors**| Automatic generation of [anchors for headings](../syntax/base.md#headers) | `extractTitle`: consider the first-level heading</br> Type: `bool`, Default: `false` </br></br>`supportGithubAnchors`: generate additional GitHub-compatible anchors</br> Type: `bool`, Default: `false` </br></br>`disableCommonAnchors`: disable generation of heading anchors</br> Type: `bool`, Default: `false` | + ||
|| **Code**| Displaying a copy button in [code blocks](../syntax/code.md#block) | - | + ||
|| **Cut** | Support for [cut markup](../syntax/interactive-elements/cuts.md) | - | + ||
|| **Deflist**| Support for [definition list markup](../syntax/lists.md#terms) | - | + ||
|| **File** | Support for [file object markup](../syntax/links.md#files) | `fileExtraAttrs`: additional attributes for the link | + ||
|| **Tasks list** | Adding [task lists](../syntax/additional.md#tasks-list) | `divClass`: classname for the `div` that wraps the checkbox</br> Type: `string`, Default: `checkbox` </br></br> `idPrefix`: prefix for the checkbox id</br> Type: `string`, Default: `checkbox` | - ||
|| **Images** | Adding [images](../syntax/media.md#images) | `assetsPublicPath`: path to icons</br> Type: `string`, Default: / | - ||
|| **Imsize** | Setting image sizes | - | - ||
|| **Includes** | Reusing content within a document | `getVarsPerFile`: a function that returns computed variables based on the file path</br> Type: `function`, Default: -  | - ||
|| **Links** | Extending [link syntax](../syntax/links.md) | - | - ||
|| **Monospace** | [Monospaced font](../syntax/base.md) | - | + ||
|| **Meta** | Adding [metadata](../project/meta.md) to the beginning of files | - | + ||
|| **Notes** | Support for [note markup](../syntax/notes.md) | `lang`: language for displaying the note type</br> Type: `string`, Default: ru | + ||
|| **Sup** | Outputting text in [uppercase](../syntax/base.md#line) | - | + ||
|| **Table** | Support for [multiline tables](../syntax/tables/multiline.md) | - | + ||
|| **Tabs** | Support for [tab markup](../syntax/interactive-elements/tabs.md) | - | + ||
|| **Video** | Adding [videos](../syntax/media.md#video) | - | + ||
|#