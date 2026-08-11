# YFM project settings

Project settings are specified in the yaml file `.yfm` in the document root. During build, you can specify a path to another file using the [launch key `--config`](tools/docs/settings.md#config).

Some parameters can also be set via the [launch keys of the `yfm build` command](./tools/docs/settings.md).

{% cut "Example of the .yfm file" %}{#yfm}

```yaml wrap
# Корневая секция параметров
allowHtml: false

# Настройки интерфейса документации
interface:
  favicon-src: https://raw.githubusercontent.com/yandex-cloud/yfm-documentation/master/_images/logo_blue_32x32.png

# Секция параметров вьюера (docs-viewer)
docs-viewer:
  # Настройки логотипа
  logo-options:
    url: https://diplodoc.com/docs/{lang}/
    src: https://storage.yandexcloud.net/docs-external/yfm-documentation/_images/logo.svg
    src-dark: https://storage.yandexcloud.net/docs-external/yfm-documentation/_images/logo.svg
    src-mobile: https://storage.yandexcloud.net/docs-external/yfm-documentation/_images/logo.svg
    src-mobile-dark: https://storage.yandexcloud.net/docs-external/yfm-documentation/_images/logo.svg
    src-preview: https://storage.yandexcloud.net/docs-external/yfm-documentation/_images/share-logo-dark.svg
    # Если логотипа нет, то вместо него можно задать текст
    title: Yandex Flavored Markdown

```

{% endcut %}

## Root section of .yfm {#root-settings}

#|
|| **Parameter** | **Description** | **Type and default value** ||
|| `allowCustomResources` {#allow-custom-resources} | Allow loading custom resources into statically generated pages. | `boolean`

`false` ||
|| `allowHtml` | Allow [using HTML elements](syntax/base.md#html) in markup. | `boolean`

`false` ||
|| `applyPresets` | Whether to apply variable presets.
[For more details about presets, see](project/presets.md). | `boolean`

`false` ||
|| `authors` {#vcs-authors} | Enable displaying the article author.

Example:

```yaml
authors:
  enabled: true
  ignore:
    - robot-*
    - noreply@company.com
```

Parameters:
- `enabled` — `boolean` — enable displaying the article author,
- `ignore` — `string[]` — ignore authors by patterns listed in the array.

The value `authors: true` is equivalent to `authors: enabled: true`.

Works when the [##vcs##](#vcs) parameter is **enabled**. | `boolean` \| `object`

`false`

||
|| `breaks` | [Wrap lines](syntax/base.md#breaks) at the carriage return character. | `boolean`

`true` ||
|| `contributors` {#vcs-contributors} | Enable displaying contributors in the article.

Example:

```yaml
authors:
  enabled: true
  ignore:
    - robot-*
    - noreply@company.com
```

Parameters:
- `enabled` — `boolean` — enable displaying contributors in the article,
- `ignore` — `string[]` — ignore contributors by patterns listed in the array.

The value `contributors: true` is equivalent to `contributors: enabled: true`.

Works when the [##vcs##](#vcs) parameter is **enabled**.

| `boolean` \| `object`

`false`

||
|| `disableCsp` {#disable-csp} | Disable adding the [Content-Security-Policy](./guides/csp.md#disable-csp) meta tag to generated HTML pages.

Use this when CSP is managed externally (for example, via server HTTP headers).| `boolean`

`false` ||
|| `extensions` {#extensions} | List of [Diplodoc extensions](extensions/index.md) used for building the project.

Objects in the list must contain the `name` parameter with the extension name, as well as operation parameters unique to each extension.

```yaml
extensions:
  - name: my-extension
    option1: true
    option2: true
    ...
```

Strings in the list can specify extension names in a simplified format:

```yaml
extensions:
  - algolia
  - some-author/my-extension
  - /my-local-extension
```

| `(string\|object)[]`

— ||
|| `langs` | An array of languages involved in the build. | —

— ||
|| `linkify` | Convert link-like strings into links.

Examples of strings:
- _https://diplodoc.com/ru_
- _diplodoc.com/ru_
| `boolean`

`false` ||
|| `lint` | Enable the [linter file](./project/lint.md). | `boolean`

`false` ||
|| `llms` {#llms} |

Settings for generating [llms.txt and llms-full.txt files](./guides/llms.md) for the project:

```yaml wrap
llms:
  enabled: true
  description: описание проекта
  llmsFullMaxSize: 8M
  url: https://example.com/llms.txt
```

Parameters:
- `description` – `string` — a string with the project description, added to the beginning of the ##llms*.txt## files;
- `llmsFullMaxSize` — `number`\|`string` — the maximum size of the ##llms-full.txt## file, accepts numbers and strings like ##1024##, ##512K##, ##8M##;
- `url` – `string` — a link to the external ##llms.txt## file, which will be written into documentation articles.

| `object`

— ||
|| `mtimes` {#vcs-mtimes} | Enable displaying the article modification date, which is taken from VCS data.

Works when the [##vcs##](#vcs) parameter is enabled.

Also, the modification date is automatically added to the page metadata ##last-modified## and ##article:modified_time##.

| `boolean`

`false` ||
|| `outputFormat` | The format of the final build files: `html` or `md`. | `string`

`html` ||
|| `removeHiddenTocItems` | Remove from the build all files marked in `toc.yaml` with the attribute `hidden: true`. | `boolean`

`false` ||
|| `sanitizeHtml` | Enables cleaning HTML markup from potentially dangerous elements in `.md` files using an HTML sanitizer. Defines allowed and forbidden tags, attributes, styles, and other elements when cleaning HTML content. | `boolean`

`true` ||
||
`singlePage`
|
Build a [single-page build](tools/docs/singlepage.md). A file `single-page.html` will be created, which will combine the contents of all project files. 

{% include [single-page-ex](./_includes/settings-single-page-ex.md) %}
|
`boolean`

`false`
||
|| `staticContent` | Build the article's HTML content as part of the layout. By default, it is in a JS object and is inserted into the page during rendering in the browser. | `boolean`

`false` ||
|| `strict` | Strict build mode, all YFM warnings are displayed as errors.

You can find the full list of YFM rules [here](./project/lint.md).
| `boolean`

`false` ||
|| `supportGithubAnchors` | Generate additional [anchors](syntax/base.md#headers) compatible with GitHub. | `boolean`

`false` ||
|| `theme` | Setting for the base color in the themizer. Overrides base-brand in the main section of the theme.yaml configuration file. [Learn more about the themizer](style/theme.md). | By default, the base color does not change.

||
|| `varsPreset` | The name of the variables preset to use during the build. | `string`

— ||
|| `vcs` {#vcs} | Setting for connecting to a VCS system. Enabling it allows using the [##mtimes##](#vcs-mtimes), [##authors##](#vcs-authors), and [##contributors##](#vcs-contributors) features.

Requires [connecting the built-in extension](#extensions) `github-vcs`.

| `boolean` \| `object`

`false` ||
|#

## Section `analytics` {#analytics}

#|
|| **Name** | **Description** | **Type and default value** ||
|| `gtm` | Google Tag Manager analytics settings.

Parameters:
- `id` — `string` — Google Tag Manager identifier in GTM format,
- `mode` — `string` — notification type before sending events `base` (default) or `notification`.

| `object`

— ||
|| `metrika` {#analytics-metrika} |

Connecting [Yandex Metrica](https://metrika.yandex.ru/) counters.

Each list item is an object with a required field `id` (counter number) and an optional field `params` for passing [counter initialization parameters](https://yandex.ru/support/metrica/ru/code/counter-initialize#parametry-inicializacii-schetchika).

Minimal configuration:
```yaml
analytics:
  metrika:
    - id: 123456
```

{% cut "Example with multiple counters" %}

```yaml
analytics:
  metrika:
    - id: 123456
      params:
        clickmap: true
    - id: 456789
      params:
        clickmap: true
        webvisor: true
```

{% endcut %}

Goals are [sent](./project/analytics/ym.md) to the connected counters from the documentation interface.

| `object[]`

—
||
|#

## Section `content` {#content}

Managing article content processing and checks.

#|
|| **Name** | **Description** | **Type and default value** ||
|| `maxAssetSize` | Maximum allowed asset size in the project. If exceeded, the build will fail with an error.

Accepts numbers and strings: ##1024##, ##512K##, ##8M##.
 
If you specify ##0##, asset size checking will not be performed. |  `number` \| `string`

`64M` ||
|| `maxHtmlSize` | Maximum allowed size of the article's HTML content after the build. If exceeded, the build will fail with an error.

Accepts numbers and strings: ##1024##, ##512K##, ##8M##.
 
Maximum value — ##96M##. |  `number` \| `string`

`42M` ||
|| `maxInlineSvgSize` | Maximum allowed size of an SVG image at which it is [inlined into the article content](./syntax/media.md#img-inline) automatically. If the size is exceeded, the SVG image is inserted via the ##\<img\>## tag.

Accepts numbers and strings: ##1024##, ##512K##, ##2M##.
 
If you specify ##0##, SVG images will not be inlined during the build.

Maximum value — ##16M##. |  `number` \| `string`

`2M` ||
|| `maxOpenapiIncludeSize` {#max-openapi-include-size} | Maximum allowed size of the JSON schema in the table of contents text of the built [OpenAPI specification](./guides/openapi.md#leadingpage). If the size is exceeded, the JSON schema is not added to the page directly, but is inserted as a download link (`link` mode).

Accepts numbers and strings like: ##1024##, ##512K##, ##2M##.
 
If you specify ##0##, the `inline` JSON schema insertion mode is always replaced with `link`. |  `number` \| `string`

`100K` ||
|| `multilineTermDefinitions` |

Whether tooltips can contain content with multiple line breaks:

* ##true## — tooltips can contain content with multiple line breaks.

* ##false## — tooltips can contain only single line breaks, and all term definitions must be placed at the end of the file (if this condition is violated, the build will fail with an [`YFM009` error](./project/lint.md)).

|  `boolean`

`true` ||
|#

## Section `interface` {#interface}

Interface display settings. All settings in the section can be overridden for individual articles by specifying their values in the [page metadata](./project/meta.md#interface).

#|
|| **Name** | **Description** | **Type and default value** ||
|| `favicon-src` | Icon in the browser tab.
You can use any image link that meets standard favicon requirements. | `string`

— ||
|| `toc` | Hides the table of contents (ToC). If not specified, the ToC is considered enabled. | `boolean`

`true` ||
|| `toc-header` {#toc-header} | Hides the header in the ToC. If not specified, the header is considered enabled. | `boolean`

`true` ||
|| `feedback` | Hides the feedback at the end of the page. If not specified, feedback is enabled. | `boolean`

`true` ||
|| `search` | Hides search. If not specified, search is considered enabled. | `boolean`

`true` ||

|#

## Section `pdf` {#pdf}

Contains data preprocessing parameters for [generating a PDF version of the documentation](guides/generate-pdf.md).

#|
|| **Name** | **Description** | **Type and default value** ||
|| `enabled` | Enable data preprocessing for the `@diplodoc/pdf-generator` service. | `boolean`

`false` ||
|| `hiddenPolicy` | If set to ##true##, pages hidden by the `hidden` parameter will be removed from the PDF version of the documentation.

If set to ##false##, hidden pages will be displayed in the PDF version of the documentation. | `boolean`

`true` ||
|#

## Section `resources` {#resources}

Managing resources attached to the project.

#|
|| **Name** | **Description** | **Type and default value** ||

|| `csp` {#resources-csp} | Managing [Content Security Policy](./guides/csp.md) (CSP).

{% cut "Example structure" %}

```yaml
resources:
  csp:
    - "script-src":
        - "self"
        - "domain1.com"
        - "domain2.com"
        "*.domain3.com"
    - "style-src":
    	- "self"
```
This configuration is converted into an HTML tag like:

```html
<meta http-equiv="content-security-policy" content="script-src 'self' domain1.com domain2.com *.domain3.com; style-src 'self'">
```

Object keys correspond to supported CSP directives. The system does not validate the correctness of the specified values — they are taken from the `.yfm` file and automatically included in the meta tag.

{% endcut %}

| `object`

— ||
|| `script` | List of JavaScript files attached to all project pages.

```yaml
resources:
  script:
    - _assets/scripts/custom.js
    - _assets/scripts/some.js
```

To connect scripts, the parameter ##[allowCustomResources](#allow-custom-resources): true## must be set.

| `string[]`

— ||
|| `style` | A list of css files to be connected to all pages of the project.

```yaml
resources:
  style:
    - _assets/style/custom.css
    - _assets/style/my.css
```

To connect styles, the parameter ##[allowCustomResources](#allow-custom-resources): true## must be set.

| `string[]`

— ||
|#

## Section `template` {#template}

Managing supported constructs of [template syntax](./syntax/vars.md).

#|
|| **Parameter** | **Description** | **Type and default value** ||
|| `enabled` | Enables processing of template syntax in the documentation. If not specified, templating is considered enabled. | `boolean`

`true` ||
|| `scopes` | > | > ||
|| `scopes.code` | Enables processing of [conditional operators](syntax/vars#conditions) syntax in code blocks. | `boolean`

`false` ||
|| `scopes.text` | Enables processing of [conditional operators](syntax/vars#conditions) syntax in document text. | `boolean`

`true` ||
|| `features` | > | > ||
|| `features.cicles` | Enables processing of [loops](syntax/vars#cycles) syntax. | `boolean`

`true` ||
|| `features.conditions` | Enables processing of [conditional operators](syntax/vars#conditions) syntax. | `boolean`

`true` ||
|| `features.substitutions` | Enables processing of [variables](syntax/vars#substitutions) syntax. | `boolean`

`true` ||
|#

## Section `search` {#search}

To add search to the documentation, explicitly specify the `search` section in the `.yfm` file.  
Diplodoc supports two types of search integration in the static documentation build mode:

* [local client-side search (based on Lunr.js)](./project/lunr.md);
* [cloud search based on the Algolia platform](./project/algolia.md).

By default, search is **disabled**; to enable it, configure the `search` section.

### Common parameters {#search-common}

#|
|| **Name** | **Description** | **Type and default value** ||
|| `provider` | Selection of the search engine.
Options:

* `local` — local search (Lunr.js);
* `algolia` — cloud search based on Algolia. | `string`

— (search not connected) ||
|#

### Parameters for local search (`provider: local`) {#search-local}

#|
|| **Name** | **Description** | **Type and default value** ||
|| `tolerance`  | Depth of match expansion:

* 0 — only exact word match;
* 1 — prefix match (`word*`);
* 2 — match by any substring of the word (`*word*`). | `number`

`2` ||
|| `confidense` | Result ranking mode:

* `phrased` — results are ranked higher by the length of the found phrase;
* `sparsed` — results are ranked higher by the number of found words. | `string`

`phrased` ||
|#

{% cut "Example of local search configuration" %}

```yaml
search:
  provider: local
  tolerance: 2
  confidense: phrased
```

{% endcut %}

### Parameters for search via Algolia (`provider: algolia`) {#search-algolia}

#|
|| **Name** | **Description** | **Type and default value** ||
|| `appId` | Algolia App ID.
Required parameter for cloud search. | `string`

— ||
|| `apiKey` | **Secret** Admin API Key for indexing.
It is recommended to pass them via environment variables or CLI. | `string`

— ||
|| `indexName` | The name of the index in Algolia. | `string`

`docs` ||
|| `index` | If `true`, the index will be automatically uploaded to Algolia after the build.
If `false`, only a local index is created. | `boolean`

`false` ||
|| `searchApiKey`  | Search API Key.
Client-side key for search on the frontend. Without it, cloud search does not work on the client. | `string`

`search-api-key` ||
|| `api` | Path to the client-side search JS API. | `string`

`_search/api.js` ||
|| `indexSettings` | [Algolia index settings](https://www.algolia.com/doc/api-reference/settings-api-parameters/). | `object`

— ||
|| `querySettings` | [Algolia search parameter settings](https://www.algolia.com/doc/api-reference/api-parameters/). | `object`

— ||
|#

{% cut "Example of configuring search via Algolia" %}

```yaml
search:
  provider: algolia
  appId: <YOUR_APP_ID>
  indexName: docs
  index: true
  searchApiKey: <YOUR_SEARCH_API_KEY>
  indexSettings:
    searchableAttributes:
      - title
      - content
      - headings
  querySettings:
    hitsPerPage: 10
    attributesToRetrieve:
      - title
      - content
      - url
```

{% endcut %}

{% note info %}

* To activate search, **be sure** to add the `search` section and specify `provider`.
* For large projects, Algolia cloud search is recommended.
* Do not publish the `apiKey` from Algolia in public repositories or production configurations — use environment variables or CLI parameters.

{% endnote %}

## The `docs-viewer` {#docs-viewer}

#|
|| **Name** | **Description** | **Type and default value** ||
|| `lang` | Default language for localization.
For [the following languages](https://github.com/diplodoc-platform/client/blob/34a5139620874627cfdebe9be74902cf9d3961b1/src/constants.ts#L15), content will be displayed in RTL (right-to-left) format. | `string`

`ru` ||
|| `langs` | Array of languages displayed in the documentation interface. The default language when opening a page is the first element in the array.

{% cut "Example of a project structure with multiple languages" %}

```
input-folder
|-- .yfm
|-- ru
    |-- toc.yaml
    |-- index.md
|-- en
    |-- toc.yaml
    |-- index.md
```

{% endcut %}

{% cut "Full list of supported languages" %}

#|
|| **Language code (ISO 639-1)** | **Language** ||
|| `am` | Amharic  ||
|| `ar` | Arabic   ||
|| `az` | Azerbaijani ||
|| `be` | Belarusian ||
|| `bg` | Bulgarian ||
|| `el` | Greek  ||
|| `en` | English ||
|| `es` | Spanish  ||
|| `et` | Estonian  ||
|| `fi` | Finnish    ||
|| `fr` | French ||
|| `he` | Hebrew      ||
|| `hu` | Hungarian ||
|| `hy` | Armenian  ||
|| `ka` | Georgian ||
|| `kk` | Kazakh  ||
|| `km` | Khmer      ||
|| `ky` | Kyrgyz ||
|| `lt` | Lithuanian  ||
|| `lv` | Latvian ||
|| `ne` | Nepali ||
|| `no` | Norwegian ||
|| `pl` | Polish   ||
|| `pt` | Portuguese  ||
|| `ro` | Romanian / Moldavian ||
|| `ru` | Russian    ||
|| `sr` | Serbian   ||
|| `tg` | Tajik ||
|| `tr` | Turkish   ||
|| `uk` | Ukrainian ||
|| `ur` | Urdu       ||
|| `uz` | Uzbek  ||
|| `vi` | Vietnamese ||
|| `zh` | Chinese  ||
|#

{% endcut %}


{% note warning %}

Languages not included in the list will not be displayed.

If the project structure contains language folders, this parameter must be specified, even if the project uses only one language.

{% endnote %} 

| `string[]`

— ||
|| `logo-options` |
Logo settings:

* `src` — link to the image for the light theme;

* `src-dark` — link to the image for the dark theme;

* `src-mobile` — link to the image for the light theme on mobile;

* `src-mobile-dark` — link to the image for the dark theme on mobile;

* `src-preview` — logo for the link preview when sharing on external resources, uses the standard [OpenGraph](https://ogp.me/);

* `url` — link to which the user is redirected when clicking the logo. You can set a link template with the `{lang}` parameter so that it is replaced with the current documentation language when navigating. For example, the link `https://diplodoc.com/docs/{lang}/` when navigating from the Russian-language documentation will lead to `https://diplodoc.com/docs/ru/`;

* `title` — text that is shown instead of the logo if it is not set. 

If the logo for the dark theme is not specified, the image for the light theme is used.

For the parameters listed above, you can configure specific logos for different documentation languages.

{% cut "Examples" %}

One logo for all languages:

```text
src: logo
```
Different logos for different languages:

```text
src:
  ru: logo1
  en: logo2
  default: logo3
```

In this example, when navigating via links with a language directory specified, `logo1` and `logo2` will be displayed for the languages `ru` and `en` respectively. If the language directory is not specified, logo3 will be displayed.

Examples of links and displayed logos:

- https://diplodoc.com/docs/ru — `logo1`
- https://diplodoc.com/docs/en — `logo2`
- https://diplodoc.com/docs — `logo3`

{% endcut %}

| —

— ||
|| `no-index` | Prohibition on indexing by external robots.

It is recommended to use it before public launches so that the document is not displayed in search engines. |  `boolean`

`false` ||
|| `project-name` | Forms the project URL. Requirements:

- lowercase only;
- only Latin letters, digits, hyphen, and underscore;
- maximum length — 63 characters.

{% note warning %}

There are three reserved names that cannot be used as the value of `project-name`:

* `build`;
* `docs-assets`;
* `api`.

{% endnote %}
| `string`

— ||
|| `themes` | Selecting the design theme: light or dark. Both are available by default. You can disable one of them by specifying the one used by default, for example:

```yaml
themes: ['dark']
```

{% note warning %}

The parameter is supported **only in the server version**.

{% endnote %}

| `string[]`
`['light', 'dark']` ||
|#

> [Ajv schema of Diplodoc configuration files](https://raw.githubusercontent.com/diplodoc-platform/ajv/refs/heads/master/src/json/yfm-schema.json)
