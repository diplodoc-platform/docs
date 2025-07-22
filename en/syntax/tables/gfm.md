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
| --------- | --------- |
| Text      | Text      |
| Text      | Text      |
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
| Align left     | Align center    | Align right    |
| :---           |      :----:     |           ---: |
| Text           | Text            | Text           |
| Text           | Text            | Text           |
```

**Result**

| Left-aligned | Centered | Right-aligned |
| :--- | :----: | ---: |
| Text | Text | Text |
| Text | Text | Text |


## Opening wide tables in a modal window

It is convenient to open wide tables in a modal window. In simple tables, this is implemented using the attribute `{wide-content title="table name"}`. The attribute must be added after the table, leaving one empty row between them.

```markdown
| Header 1  | Header 2  |
| --------- | --------  |
| Текст     | Текст     |
| Текст     | Текст     |

{wide-content title="Table name"}
```

**Result**

| Header 1  | Header 2  |
| --------- | --------  |
| Текст     | Текст     |
| Текст     | Текст     |

{wide-content title="Table name"}

## Adding a "floating header" to the table

You can add a "floating header" for tables. To do this, add the `{sticky-header}` attribute after the table.

```markdown
| Header 1  | Header 2  |
| --------- | --------- |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
...
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |

{sticky-header}
```

**Результат**

| Header 1  | Header 2  |
| --------- | --------- |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |
| Text      | Text      |

{sticky-header}