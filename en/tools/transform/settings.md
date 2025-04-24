# Transformation settings

The transformation settings are listed below. You can configure them and [standard YFM settings](../../settings.md) in one of the following ways:

* When invoking the `transform` function.
* In a [configuration file](../../project/config.md).

| Name | Description | Type | Default value |
| --- | --- | --- | --- |
| `plugins` | Added plugins | `function[]` | See the [Plugins](../../plugins/index.md) page |
| `highlightLangs` | Additional languages for [code highlighting](highlight.md) | `{'lang': function}` | `{}` |
| `extractTitle` | Return the first first-level header as the title of the entire document | `bool` | `false` |
| `needTitle` | Return the first first-level header without removing it from the document text | `bool` | `false` |
|`needFlatListHeadings` | Generate a flat list of all headers in a document | `bool` | `false` |
| `disableCommonAnchors` | Disable generation of heading anchors | `bool` | `false` |

