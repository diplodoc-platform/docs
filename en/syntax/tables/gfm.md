# GFM Tables

Tables with syntax similar to tables in GitHub Flavored Markdown. Suitable for simple tables with single-line content in cells.

{% note tip %}

To quickly create tables, you can use online generators. For example, [Tables Generator](https://www.tablesgenerator.com/markdown_tables).

{% endnote %}

A table consists of:

* A header row.
* A separator row.
* Rows with data.

The header row is separated from table cells by three or more `-` characters. Columns are separated by `|`.

```markdown
| Header 1  | Header 2  |
| ----------- | ----------- |
| Text       | Text       |
| Text       | Text       |
```

**Result**

| Header 1 | Header 2 |
| ----------- | ----------- |
| Text | Text |
| Text | Text |

In the table cells, you can use [line formatting](../base.md#line), [links](../links.md), [single-line code snippets](../code.md#inline), and [images](../media.md#images).

## Text alignment

Use the `:` symbol in the separator row to align the text in the columns to the left, right, or center.

```markdown
| Align left  | Align center        | Align right |
| :---            |      :----:      |            ---: |
| Text           | Text            | Text           |
| Text           | Text            | Text           |
```

**Result**

| Left-aligned | Centered | Right-aligned |
| :--- | :----: | ---: |
| Text | Text | Text |
| Text | Text | Text |

