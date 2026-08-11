# Multiple tables of contents

You can split a documentation project into parts by grouping articles into multiple tables of contents and linking them with cross-references.

## How to group articles {#multitoc}

If you create a table of contents file `toc.yaml` in a project folder, all articles in that folder and its subfolders will display the table of contents from that file.

For example, in the following structure:

```
input-folder
|-- toc.yaml # корневое оглавление
|-- article1.md
|-- article2.md
|-- folder1
    |-- article3.md
|-- folder2
    |-- toc.yaml # оглавление подраздела
    |-- article4.md
    |-- article5.md
    |-- folder3
        |-- article6.md
```

* the files `article1.md`, `article2.md`, `article3.md` will use the table of contents from the root `toc.yaml`,
* the files `article4.md`, `article5.md`, `article6.md` will use the table of contents from `folder2/toc.yaml`.

You can create cross-references between tables of contents by including items from another table of contents in `toc.yaml` or by using the project's [extended navigation](./navigation.md).

Possible contents of the table of contents files from the example:

#|
||

##toc.yaml##

|

##folder2/toc.yaml##

||
||

```yaml
items:
  - name: Article 1
    href: article1.md
  - name: Article 2
    href: article2.md
  - name: Article 3
    href: folder1/article3.md
  - name: Article 4
    href: folder2/article4.md # ссылка на подраздел
```

|

```yaml
items:
  - name: Article 4
    href: article4.md
  - name: Article 5
    href: article5.md
  - name: Article 6
    href: folder3/article6.md
  - name: Back to Article 1
    href: ../article1.md # ссылка в корневое оглавление
```

||
|#
