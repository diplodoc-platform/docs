# Article metadata

Metadata is markup elements used to store settings for a specific article, SEO information, or document author details in the source text. They are not displayed in the assembled article but can affect its assembly.

In md files, metadata is added in YAML format at the beginning of the file (this part of the file is called ##frontmatter##).

In yaml files with [Page constructor pages](./page-constructor.md) and [leading pages](./leading-page.md) — directly into the root object.

Example:

```yaml
---
title: Заголовок
description: Описание
---

# Заголовок статьи

Текст статьи ......
```

Supported parameters:

#|
|| **Name** | **Description** | **Type and default value** ||
|| `alternate` | Links to other language versions of the page.

Each link is specified in `<link rel="alternate" hreflang="..." href="..."/>`.

During the assembly stage, the array is automatically supplemented with matching links from other documentation languages.
 | `string[]`

— ||
|| `canonical` | Canonical link for page indexing.

Specified in `<link rel="canonical" href="..."/>`.

If not explicitly specified, the path to the page is automatically added during the assembly stage.
 | `string`

— ||
|| `copyright` | Indicates the owner of the page content.

Specified in `<meta name="copyright" content="..."/>`. | `string`

— ||
|| `description` {#description} | Meta description of the page.

Specified in `<meta name="description" content="..."/>` and in [##llms.txt##](../guides/llms.md). | `string`

— ||
|| `keywords` | List of page keywords for search engines.

Specified in `<meta name="keywords" content="key1,key2,..."/>`. | `string[]`

— ||
|| `interface` {#interface} | Section with interface display settings. Overrides the settings from the [same-named section of .yfm](../settings.md#interface) for the current page.

{% cut "Example with disabling the table of contents on the page" %}

```yaml
---
interface:
  toc: false
---
```

{% endcut %}

| `object`

— ||
|| `metadata` | List describing arbitrary meta fields of the article.

The list contains objects of the form:

```yaml
metadata:
  - name: name 1
    content: content 1
  - http-equiv: http-equiv 2
    content: content 2
  - property: property 3
    content: content 3
...
```

based on which a set of tags is generated:

```html
<meta name="name 1" content="content 1"/>
<meta http-equiv="http-equiv 2" content="content 2">
<meta property="property 3" content="content 3">
```

Examples of fields and their possible values can be found in the article on [organizing content analytics](../guides/content-analytics.md#meta-information-example).

| `object[]`

— ||
|| `resources` | Section for managing page resources.

Overrides the ##resources## settings from the [resources section of .yfm](../settings.md#resources).

{% note warning %}

Only extending the list of values in [##csp##](../settings.md#resources-csp) is supported.

{% endnote %}

| `object`

— ||
|| `tags` | List of page tags. After the build, tags are displayed below the article and added to the HTML as separate `<meta property="article:tag" content="...">` elements.

If [search](./search.md) is configured for the project, each tag links to related articles. On the search page, you can select several tags; the results include articles that have at least one of them.

During processing, tags are converted to lowercase, surrounding whitespace is removed, and duplicate values are merged. A tag can contain up to 32 characters.

{% cut "Example" %}

```yaml
---
title: Working with tables
tags:
  - Markdown
  - Tables
---
```

{% endcut %}

| `string[]`

— ||
|| `title` | Meta title of the page.

Specified in `<meta name="title" content="..."/>`. | `string`

— ||

|#

> See also: [Ajv schema of article metadata](https://raw.githubusercontent.com/diplodoc-platform/ajv/refs/heads/master/src/json/frontmatter-schema.json)
