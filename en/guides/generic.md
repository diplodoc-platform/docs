# Generic

Generic is a built-in [includer](*includer) for including Markdown files into the documentation structure without manually listing each heading in `toc.yaml`.

## Usage example {#example}

The documentation is located in the directory `doc_root`. The generated content should be placed in the directory `doc_root/gen_docs`.

Add the generic includer to `doc_root/toc.yaml`.

```yaml
# doc_root/toc.yaml
title: documentation
href: index.yaml
items:
  - name: docs
    include:
      path: gen_docs # путь к директории с .md файлами для сгененированного контента
      includers: # подключение generic-инклюдер
        - name: generic
          autotitle: true
      mode: link
```

Specify the generated page on the [landing page](*Разводящая_страница) in `doc_root/index.yaml`.

```yaml
# doc_root/index.yaml
title: documentation
links:
  - title: docs # название файла
    href: gen_docs/ # путь к директории с .md файлами для сгененированного контента
```

## Parameters {#settings}

| Parameter | Type | Default value | Description |
| --- | --- | --- | --- |
| `autotitle` | `boolean` | `true` | When `true` — headings from files are displayed in the navigation; when `false` — file names are displayed. |
| `linkIndex` | `boolean` | `false` | When `true` — `index.md` files in subdirectories are used as the link of the parent navigation item. The section becomes clickable and opens `index.md`, while `index.md` is not duplicated in child items. |
| `orderBy` | `string` | not set | The [sorting method for items](#sorting): `natural` (numbers in names are compared as numbers) or `filename` (strict lexicographic order). Without this parameter, the order depends on the file system. |
| `order` | `string` | `asc` | The [sorting direction](#sorting): `asc` or `desc`. Works only together with `orderBy`. |

## Clickable sections with `linkIndex` {#link-index}

By default, the generic includer creates sections based on directory names. A section item is only expandable — clicking it collapses or expands the list of child pages, while `index.md` becomes a regular child item.

With the `linkIndex: true` option, the behavior changes: the `index.md` file inside a subdirectory becomes the link (`href`) of the parent navigation item. Clicking a section opens `index.md`, and the list of child pages expands using the arrow.

```yaml
# doc_root/toc.yaml
title: documentation
href: index.yaml
items:
  - name: docs
    include:
      path: gen_docs
      includers:
        - name: generic
          linkIndex: true
      mode: link
```

### Example

Directory structure:

```
gen_docs/
  section-a/
    index.md
    page1.md
    page2.md
  section-b/
    index.md
    page1.md
```

Without `linkIndex` (by default):

```yaml
- name: section-a        # не кликабельный, только раскрывается
  items:
    - name: index
      href: section-a/index.md
    - name: page1
      href: section-a/page1.md
    - name: page2
      href: section-a/page2.md
```

With `linkIndex: true`:

```yaml
- name: section-a        # кликабельный, открывает index.md
  href: section-a/index.md
  items:
    - name: page1
      href: section-a/page1.md
    - name: page2
      href: section-a/page2.md
```

## Sorting items {#sorting}

By default, the generic includer preserves the order in which files are received from the file system. This means that for documents with numeric names (`1.md`, `2.md`, `3.md`, …, `10.md`, …, `100.md`) the order may be unpredictable.

To get a deterministic order, set the `orderBy` parameter:

- `natural` — "natural" sorting: each sequence of digits in a name is compared as a number. Works correctly for purely numeric names (`1`, `2`, `3`, …, `9`, `10`, `11`, …, `99`, `100`), names with a numeric prefix (`1-intro`, `2-setup`, `10-deep`), and for multiple groups of digits (`chapter-1-1`, `chapter-1-2`, `chapter-1-10`).
- `filename` — strict lexicographic order. For example: `1`, `10`, `100`, `11`, `2`, `20`, `9`.

The `order` parameter sets the direction: `asc` (ascending, default) or `desc` (descending). Works only if `orderBy` is set.

Sorting is applied recursively to all levels of the table of contents.

### Example: natural sorting of numeric files

Structure:

```
gen_docs/
  1.md
  2.md
  10.md
  20.md
  100.md
```

Configuration:

```yaml
includers:
  - name: generic
    orderBy: natural
```

Resulting order: `1`, `2`, `10`, `20`, `100`.

### Example: sorting nested directories

Structure:

```
gen_docs/
  chapter-1/
    intro.md
    section-1.md
    section-2.md
    section-10.md
  chapter-2/
    intro.md
  chapter-10/
    intro.md
```

Configuration:

```yaml
includers:
  - name: generic
    orderBy: natural
```

Resulting order at the top level: `chapter-1`, `chapter-2`, `chapter-10`. Inside `chapter-1`: `intro`, `section-1`, `section-2`, `section-10`.

### Example: numeric prefix and multiple groups of digits

Structure:

```
gen_docs/
  1-intro.md
  2-setup.md
  10-advanced.md
  chapter-1-1.md
  chapter-1-2.md
  chapter-1-10.md
```

Configuration:

```yaml
includers:
  - name: generic
    orderBy: natural
```

Resulting order: `1-intro`, `2-setup`, `10-advanced`, `chapter-1-1`, `chapter-1-2`, `chapter-1-10`. Each sequence of digits in a name is compared as a number — therefore `chapter-1-10` comes after `chapter-1-2`, not between `chapter-1-1` and `chapter-1-2`.

[*Разводящая_страница]: Root page of a section with navigation to subsections (nested pages). [Details](../project/leading-page.md)

[*includer]: File inclusion mechanism.