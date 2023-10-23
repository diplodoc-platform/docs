| Plugin name  | Description | Parameters | Added</br>by default |
|--------------| --- | --- | --- |
| **Anchors**  | Automatically generate [anchors for headers](../syntax/base.md#headers) | `extractTitle`: Consider the first level header</br>(type: bool, default value: false)</br></br>`supportGithubAnchors`: Generate additional anchors compatible with GitHub</br>(type: bool, default value: false) | + |
| **code**     | Display the copy button in [code blocks](../syntax/code.md#block) | - | + |
| **Cut**      | Support for the [cut](../syntax/cuts-tabs.md#cuts) markup | - | + |
| **Deflist**   | Support for the [definition list](../syntax/lists.md#terms) markup | - | + |
| **File**     | Support for the [file objects](../syntax/links.md#files) markup | `fileExtraAttrs`: additional attributes for the link | + |
| **Tasks list**     | Support for the [tasks list](../syntax/additional.md#tasks-list)              | `divClass`: classname for div wrapping the checkbox</br>(type: string, default value: checkbox)</br></br> `idPrefix`: prefix for checkbox id</br>(type: string, default value: checkbox) | - |
| **Images**   | Add [images](../syntax/media.md#images) | `assetsPublicPath`: Path to icons</br>(type: string, default value: /) | - |
| **Imsize**   | Set the image size | - | - |
| **Includes** | Reuse content in a document | `getVarsPerFile`: A function that returns calculated variables using the path to the file</br>(type: function, default value: -) | - |
| **Links**    | Expand [link syntax](../syntax/links.md) | - | - |
| **Meta**     | Add [metadata](../syntax/meta.md#meta) to the beginning of files | - | + |
| **Notes**    | Support for the [note](../syntax/notes.md) markup | `lang`: A language for displaying the note type</br>(type: string, default: ru) | + |
| **Sup**      | Output text as [superscript](../syntax/base.md#line) | - | + |
| **Table**    | Support for [multiline tables](../syntax/tables/multiline.md) | - | + |
| **Tabs**     | Support for the [tab](../syntax/cuts-tabs.md#tabs) markup | - | + |
| **Video**    | Add a [video](../syntax/media.md#video) | - | + |

