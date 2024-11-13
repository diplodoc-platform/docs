# Settings

Standard YFM settings are listed below. Depending on the tool you use, you can configure them in one of the following ways:

* In a [configuration file](./project/config.md).
* As a function parameter ([Transformer](./tools/transform/settings.md)).
* Via startup keys ([Builder](./tools/docs/settings.md)).

| Name | Description | Type | Default value |
| :--- | :--- | :--- | :--- |
| `vars` | [Variables](./syntax/vars.md) | `Object` | `{}` |
| `allowHTML` | Allow HTML in markup | `bool` | `false` |
| `linkify` | Convert link-like strings to links | `bool` | `false` |
| `breaks` | Use the carriage return character for a line break | `bool` | `true` |
| `conditionsInCode` | Meet conditions in code blocks | `bool` | `false` |
| `disableLiquid` | Disable the use of variables | `bool` | `false` |
| `supportGithubAnchors` | Generate additional [anchors](./syntax/base.md#headers) that are compatible with GitHub | `bool` | `false` |
| `lang` | Localization language of default texts | `string` | `ru` |
`needToSanitizeHtml` | Need to sanitize the generated HTML | `bool` | `true`
`sanitizeOptions` | Sanitizer configuration | `Object` | `undefined`
`linkifyTlds` | Allow set tld for the linkify plugin | `string \| string[]` | `undefined`
`analytics` | Analytics module configuration | `Object` | `undefined`
`analytics.gtm` | Options for Google Tag Manager analytics | `Object` | `undefined`
`analytics.gtm.id` | ID of Google Tag Manager at format GTM-* | `string` | `undefined`
`analytics.gtm.mode` | Notification type before analytics events start being sent `base` or `notification`  | `string` | `base`
