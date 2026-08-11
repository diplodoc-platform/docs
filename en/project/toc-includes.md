# Inserting tables of contents

You can split a table of contents into multiple files and include one table of contents inside another. When this is useful:
* You have table of contents blocks that are used in multiple documents.
* You have a large document that is easier to assemble from several smaller blocks.

## Including a table of contents as a section {#as-section}

```yaml
- name: Имя заимствованного блока
  include:
    path: another/toc.yaml
```

By default, the `path` specifies the path relative to the documentation root. The name of the imported file can be anything, not necessarily `toc.yaml`:

```yaml
- name: Инструкции для Android
  include:
    path: another/toc_android.yaml
```

## Including a table of contents without creating a section {#as-pages}

You can include `toc.yaml` with its items added at the same level of the table of contents.

`toc.yaml`:

```yaml
items:
  - name: Name1
    href: file1.md

  # Отсутствие поля name у элемента означает, что элементы включаемого оглавления стоит
  # добавлять на тот же уровень оглавления, а не как новый раздел
  - include: { path: path/to/toc.yaml }

  - name: NameX
    href: fileX.md
```
`path/to/toc.yaml`:

```yaml
items:
  - name: NameA
    href: fileA.md
  - name: NameB
    href: fileB.md
```
Result in the table of contents:

```
- Name1
- NameA
- NameB
- NameX
```


## Table of contents insertion modes {#include-mode}

There are several modes that are set in the `mode` property:

* `root_merge` — this mode is enabled by default. In this mode, all used files and directories are copied along with the table of contents. Suppose you import content from folder A into content located in folder B. Then, during the build, all files from folder A will be copied to folder B. Note that copying occurs with file overwriting.

  Since the project structure changes during copying, `sourcePath` with the path to the source file is added to the metadata of new files. This field is used for the page editing link.

* `merge` — similar to `root_merge`, but the path to the table of contents file is specified relative to the current file in which you use `include`.
* `link` — the project structure is not changed. All links of the included table of contents are changed to links relative to the table of contents into which the inclusion occurs.

**Example:**
You need to specify the relative path to `path` to the table of contents being imported:

```yaml
items:
  - include: { mode: merge, path: ../relative/path/to/toc.yaml }
```

## Inserting arbitrary content {#includers}

Using the `includers` parameter, you can insert [arbitrary content](../guides/includers.md) into the documentation.