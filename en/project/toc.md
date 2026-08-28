# Document table of contents

The document structure is described in the file `toc.yaml`. Based on this file, the table of contents is generated and the document is assembled.

{% note warning %}

Files not listed in `toc.yaml` are not processed during assembly.

{% endnote %}

## Structure {#structure}

The standard structure of the `toc.yaml` file is as follows:

```yaml
title: Имя документа
href: index.yaml
items:
  - name: Имя раздела
    href: path/to/file.md
  - name: Имя группы разделов
    items:
      - name: Имя раздела
        href: path/to/file.md
      - name: Имя раздела
        href: path/to/file.md
  - name: Имя раздела
    href: path/to/file.md
```

At the root:

* `title` — the document title. It is displayed in the table of contents above the list of all sections. You can hide it using the ##interface: toc-header## setting in the [.yfm file](../settings.md#toc-header).
* `href` — the relative path to the file.
* `items` — table of contents items.
* `navigation` — a settings section for [extended navigation](./navigation.md).

Each table of contents item contains the following fields:

* `name` — the name of a section or group of sections.
* `href` — the relative path to the file.
* `items` — a list of nested items.

All relative paths are calculated from the _location_ of the `toc.yaml` file in which they are specified.

You can group parts of the documentation into [multiple separate tables of contents](./toc-multiple.md).

To simplify working with large tables of contents and reuse blocks, [inserting tables of contents](./toc-includes.md) is supported.

> See also: [Ajv schema for toc.yaml table of contents files](https://raw.githubusercontent.com/diplodoc-platform/ajv/refs/heads/master/src/json/toc-schema.json)

## Opening links in a new tab {#target}

By default, all relative links in the table of contents open in the current browser tab, and all absolute links open in a new tab. This behavior can be changed using the `target` parameter:

* `_self` — a link from the table of contents will open in the current tab,
* `_blank` — a link from the table of contents will open in a new tab.

```yaml
- name: Абсолютная ссылка
  href: https://github.com
  target: _self
```

## Section visibility conditions {#when}

Individual sections can be included or excluded from the document depending on the values of [variables](../syntax/vars.md). The `when` parameter is used to describe visibility conditions.

Available comparison operators: `==`, `!=`, `<`, `>`, `<=`, `>=`.

```yaml
- name: Раздел с условным вхождением
  href: path/to/conditional/file.md
  when: version == 12
```

## Substitutions and conditional operators {#subtitudes}

The document title supports [substitutions](../syntax/vars#subtitudes) and [conditional operators](../syntax/vars#conditions).

```yaml
title: "not_var{{ title }}"
```

{% note warning %}

If a value starts with a substitution, always enclose it in quotes. Without them, the value is treated as JSON embedded in YAML, which can lead to build errors, for example `TypeError: str.replace is not a function`.

{% endnote %}

## Configuring section expansion { #expanded }

By default, all sections of the table of contents are collapsed. To keep important sections and pages always visible in the table of contents, you can use the `expanded` parameter:

```yaml
title: Yandex Cloud Marketplace
items:
  - name: Начало работы
    href: index.md
  - name: Основы
    expanded: true
    items:
      - name: Создание виртуальной машины
        href: create.md
  - name: Первичная настройка программного обеспечения
    href: setup.md
  - name: Работа с виртуальной машиной
    href: operate.md
  - name: Справочник API
    href: guide.md
```

{% note warning %}

The `expanded` parameter can only be used for first-level sections; specifying `expanded` in lower-level sections is ignored.

{% endnote %}

## Labeled sections in navigation {#labeled}

Special headings that visually group individual items in the table of contents.

In the `toc.yaml` file, specify the `labeled: true` attribute for the corresponding menu item:

```yaml
title: Имя документа
href: index.yaml
items:
  - name: Имя раздела
    labeled: true
    href: path/to/file.md
  - name: Имя группы разделов
    labeled: true
    items:
      - name: Имя раздела
        href: path/to/file.md
      - name: Имя раздела
        href: path/to/file.md
  - name: Имя раздела
    labeled: true
    href: path/to/file.md
```

### Hidden sections {#hidden}

To make a section accessible only via a direct link and exclude it from the table of contents, specify the `hidden` parameter.

```yaml
- title: Секретный документ
  href: secret.md
  hidden: true
```

To completely exclude hidden sections from the build, use the [build key](../tools/docs/settings.md) `--remove-hidden-toc-items=true`.

The `hidden` parameter controls navigation visibility and, together with `--remove-hidden-toc-items`, removal from the build. It does not prohibit indexing. Hidden pages are omitted from `llms.txt` and `llms-full.txt`, but use [`noIndex: true`](#no-index) as well to exclude them from other indexes.

## Disabling indexing {#no-index}

To exclude pages from search indexes and from `llms.txt` and `llms-full.txt`, add `noIndex: true`. You can set it at the `toc.yaml` root, on an individual page, or on a section.

Disable indexing for all documentation in this TOC:

```yaml
title: Internal documentation
href: index.md
noIndex: true
items:
  - name: Getting started
    href: start.md
```

Disable indexing for an individual page and a section:

```yaml
items:
  - name: Draft
    href: draft.md
    noIndex: true
  - name: Internal section
    href: internal/index.md
    noIndex: true
    items:
      - name: Details
        href: internal/details.md
```

For a section, the restriction applies to its own `href` page and every descendant. A root `noIndex` from an included TOC also applies to the inserted pages.

The `true` value is cumulative: `noIndex: false` on a nested page does not cancel a restriction from its parent section, the TOC root, or [page metadata](./meta.md#no-index). The global [`.yfm` `docs-viewer.no-index`](../settings.md#no-index) setting cannot be canceled locally either.

To both hide a page from navigation and disable its indexing, specify both independent parameters:

```yaml
- name: Service page
  href: service.md
  hidden: true
  noIndex: true
```

## Auto-generation of the table of contents

To automatically build a table of contents from a list of md files in a folder, you can use the [generic includer](../guides/generic.md).
