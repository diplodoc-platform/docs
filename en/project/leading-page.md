# Leading page

To quickly navigate the document, you can design a root page in the form of a grid with links to main sections.

**Example**: design of the [Yandex Compute Cloud documentation](https://cloud.yandex.com/docs/compute/) leading page.

![Example of a leading page](../_images/leading.jpg)

## Structure {#structure}

The standard file structure of the `index.yaml` leading page:

```yaml
title: Document name
description: A description of the document
meta:
  title: Metadata
  noIndex: true
links:
- title: First section
  description: A description of the first section
  href: path/to/file.md
- title: Second section
  description: A description of the second section
  href: path/to/file.md
```

* `title`: Document name. It's displayed in the table of contents above the list of all sections.
* `description`: A description of the document.
* `meta`: [Metadata](../syntax/meta.md#meta).
* `links`: Grouping element. The following is set within each section:
    * `title`: Name of the section. Displayed as the name of the link.
    * `description`: Description of the section.
    * `href`: The relative path to the file.

## Element visibility conditions {#when}

Individual sections can be included on or excluded from a leading page, depending on the values of [variables](../syntax/vars.md). To describe visibility conditions, the `when` parameter is used.

Possible comparison operators: `==`, `!=`, `<`, `>`, `<=`, and `>=`.

```yaml
- title: Section with a conditional inclusion.
  description: A description of the section.
  href: path/to/conditional/file.md
  when: version == 12
```

## Substitutions and conditional operators {#subtitudes}

Title and description of document and links support [substitutions](../syntax/vars#subtitudes) and [conditional operators](../syntax/vars#conditions).

```yaml
title: "not_var{{ title }}"
description: "{% if version == 10 %}not_var{{ description_legacy }}{% else %}not_var{{ description }}{% endif %}"
meta:
  title: "not_var{{ meta_title }}"
links:
- title: "not_var{{ link_title }}"
  description: "not_var{{ link_description }}"
  href: path/to/conditional/file.md
```
