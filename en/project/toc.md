# Table of contents

The document structure is described in the file `toc.yaml`. It defines how a table of contents is generated and documentation is built.

{% note warning %}

Files that are not specified in `toc.yaml` are not processed during the build.

{% endnote %}

## Structure {#structure}

The standard `toc.yaml` file structure looks like the following:

```yaml
title: Document title
href: index.yaml
items:
  - name: Section name
    href: path/to/file.md
  - name: Section group name
    items:
      - name: Section name
        href: path/to/file.md
      - name: Section name
        href: path/to/file.md
  - name: Section name
    href: path/to/file.md
```

* `title`: Document name. It's displayed in the table of contents above the list of all sections.
* `name`: The name of a section or group of sections.
* `href`: A relative path to the file.
* `items`: A grouping element.

## Section visibility conditions {#when}

Individual sections can be included in or excluded from the document, depending on the values of [variables](../syntax/vars.md). To describe visibility conditions, the `when` parameter is used.

Possible comparison operators: `==`, `!=`, `<`, `>`, `<=`, `>=`.

```yaml
- name: Section with conditional entry
  href: path/to/conditional/file.md
  when: version == 12
```

## Substitutions and conditional operators {#subtitudes}

Document title supports [substitutions](../syntax/vars#subtitudes) and [conditional operators](../syntax/vars#conditions).

```yaml
title: "{{ title }}"
```

{% note warning %}

Always use quotes if a value starts with a substitution. Without quotes, the value is processed as JSON embedded in YAML, which can lead to build errors such as `TypeError: str.replace is not a function`.

{% endnote %}

## Inserting tables of contents {#includes}

You can split a table of contents into different files and insert one table of contents into another. Use cases:
* You have table of contents blocks in several documents.
* You have a large document, which is easier to build from smaller blocks.

### Example of including a table of contents as a section {#include-as-section}

```yaml
- name: Imported block name
  include:
    path: another/toc.yaml
```

By default, `path` specifies the path from the documentation root. The name of the imported file doesn't have to be `toc.yaml`:

```yaml
- name: Instructions for Android
  include:
    path: another/toc_android.yaml
```

### Example of including a table of contents without creating a section {#include-as-pages}

You can also include `toc.yaml` with its elements in the same level of the table of contents.

`toc.yaml`:

```yaml
items:
  - name: Name1
    href: file1.md

  # If an element doesn't have a name field, it means that elements of the included table of contents must be
  # added to the same table of contents level, not as a new section
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
- Name1
- NameA
- NameB
- NameX


### mode {#include-mode}

Different modes that can be set in the `mode` property:

* `root_merge`: Enabled by default. This copies the table of contents along with all of the files and directories it uses. Let's say that you're importing the contents from folder A into the contents in folder B. All of the files from folder A will be copied to folder B during the build. Note that copying overwrites files.

   The copying process changes the project structure, and `sourcePath` is added to the new files' metadata with the path to the source file. This field is used for the link to edit the page.
* `merge`: Similar to `root_merge`, but the path to the table of contents file is specified relative to the current file where you are using `include`.
* `link`: The project structure doesn't change. All of the included table of contents' links are changed to links relative to the table of contents where it's included.

For example, let's say you want to specify a relative path in `path` to the table of contents you are importing. Do it like this:

```yaml
items:
  - include: { mode: merge, path: ../relative/path/to/toc.yaml }
```

### Includers {#includers}

You can include any content using `includers`, as long as the includer for this type of content is implemented.

Includers are specified as:

- an array of `includer` objects in the `includers` field

- `includer` object in the `includer` field. _in the process of deprecation in favor of the `includers` field_

{% note warning "include requirements" %}

`include` should provide `path` where content is gonna be included

`path` field must be the **path to where content is gonna be included**.

`mode` must be **link or omitted**

{% endnote %}

{% note warning "includers requirements" %}

`includers` must be array of includer objects that are going to be executed
in the order they were provided

{% endnote %}

{% note warning "includer requirements" %}

parameters between includer objects differ but one common parameter is the **name of the includer to execute**

`name` specify name of the includer to run

{% endnote %}

#### Usage example

abstract example of the includers usage

_refer to appropriate includer section for the concrete usage example_

```
# toc.yaml
...
items:
  - name: <item-name>
    include:
      path: <path-where-to-include>
      includers:
        - name: <name-of-the-first-includer>
          <includer-parameter>: <includer-parameter-value>
        - name: <name-of-the-second-includer>
        - name: <name-of-the-third-includer>
      mode: link
...
```

#### List of implemented includers

- [Generic](#includers-generic)
- [Open API](#includers-open-api)
- [Unarchive](#includers-unarchive)
- [Source Docs](#includers-source-docs) _in the process of deprecation in favor of generic includer_

#### Generic {#includers-generic}

You can generate documentation in the **markdown format** with **the tool of your choice** and include it into your main documentation.

Includer will generate table of content for the provided content and include it as it is.

##### Usage example

Let's say we have a documentation project in the `doc_root` folder.

Put markdown content generated with the tool of your choice inside `doc_root/docs` folder.

Then you need to include it inside `doc_root/toc.yaml` with generic `includer`.

Link to the generated leading page inside main `doc_root/index.yaml`.

```yaml
# doc_root/toc.yaml
title: documentation
href: index.yaml
items:
  - name: docs
    include:
      path: docs
      includers:
        - name: generic
          input: docs
      mode: link
```

```yaml
# doc_root/index.yaml
title: documentation
links:
  - title: docs
    href: docs/
```

#### Open API {#includers-open-api}
You can generate documentation from the [Open API](https://www.openapis.org/) specification file and include it into your main document.

{% note warning %}

openapi includer requires you to enable usage of HTML inside documentation

set `allowHTML` to `true` inside `.yfm` config

```
allowHTML: true
```

{% endnote %}

##### Usage example

Let's say we have a documentation project in the `doc_root` folder.

Put specification file into it at `doc_root/openapi.yaml`.

Then you need to include it inside `doc_root/toc.yaml` with the openapi `includer`

Link to the generated leading page inside main `doc_root/index.yaml`

```yaml
# doc_root/toc.yaml
title: documentation
href: index.yaml
items:
  - name: openapi
    include:
      path: openapi
      includers:
        - name: openapi
          input: openapi.yaml
      mode: link
```

```yaml
# doc_root/index.yaml
title: documentation
links:
  - title: openapi
    href: openapi/
```

#### Unarchive {#includers-unarchive}

You can use `unarchive` includer to unpack your tarball before applying other includers e.g `generic` includer.

##### Usage example

As an example you might have `docs.tar` inside root of your documentation project `doc_root/docs.tar`.

`docs.tar` has markdown content inside of it, that you would like to include with `generic` includer.

Then you would apply chain of the includers(`unarchive` -> `generic`) to achive desired results.

```yaml
# doc_root/toc.yaml
title: documentation
href: index.yaml
items:
...
   - name: multiple
     include:
       path: multiple
       mode: link
       includers:
         # run unarchive includer
         - name: unarchive
           # specify tarball you want to unpack as input parameter
           input: docs.tar
           # specify output path where tarball content is going to be unpacked
           output: unpacked
         # run generic includer
         - name: generic
           # specify path from unarchive includers output field as input path
           input: unpacked
```

```yaml
# doc_root/index.yaml
title: documentation
links:
  - title: openapi
    href: openapi/
```

#### Source Docs {#includers-source-docs}

You can generate documentation with [Source Docs](https://github.com/SourceDocs/SourceDocs) and include it into your main documentation.

{% note warning %}

Source Docs includer is getting depricated in the favor of [Generic Includer](#includers-generic)

{% endnote %}

##### Usage example

Let's say we have a documentation project in the `doc_root` folder.

Put the output of the Source Docs into the `doc_root/docs` folder.

Then you need to include it inside `doc_root/toc.yaml` with sourcedocs `includer`.

Link to the generated leading page inside main `doc_root/index.yaml`.

```yaml
# doc_root/toc.yaml
title: documentation
href: index.yaml
items:
  - name: docs
    include:
      path: docs
      includers:
        - name: sourcedocs
          input: docs
      mode: link
```

```yaml
# doc_root/index.yaml
title: documentation
links:
  - title: docs
    href: docs/
```

## Section expansion { #expanded }

By default, all table of contents sections are hidden. You can change it by adding `expanded`:

```yaml
title: Yandex Cloud Marketplace
items:
  - name: Getting started
    href: index.md
  - name: Test topichead
    expanded: true
    items:
      - name: Creating a virtual machine
        href: create.md
  - name: Initial software configuration
    href: setup.md
  - name: Operating a virtual machine
    href: operate.md
  - name: API reference
    href: guide.md
```

You can only use `expanded` for first-level sections. In lower sections, `expanded` will be ignored.
Use it to make important sections and pages in the table of contents always visible.


## Hidden sections {#hidden}

To make a section accessible only by direct link and excluded it from the table of contents, add the `hidden` parameter.

```yaml
- title: Secret document
  href: secret.md
  hidden: true
```

To completely exclude hidden sections from the build, use the [build key](../tools/docs/settings.md) `--remove-hidden-toc-items=true`.
