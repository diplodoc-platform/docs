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

## Auto-generation of the table of contents

To automatically build a table of contents from a list of md files in a folder, you can use the [generic includer](../guides/generic.md).
