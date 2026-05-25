# Multiline tables

Tables with support inside cells for more than just simple content. Example, [lists](../lists.md), [code snippets](../code.md) and other tables.

## Syntax {#syntax}

* a table starts with `#|` and ends with `|#`;
* lines start and end with `||`;
* the cells are separated by a symbol `|`.

{% note tip "Headers of table" %}

Multiline tables do not contain headers, but they can be done by applying formatting to the content of the cells of the first row. For example, highlighting them in bold.

You can also use the `header-rows` table attribute for semantic header rows. See the [Header rows](#header-rows) section for details.

{% endnote %}

```markdown
#|
|| **Header1** | **Header2** ||
|| Text | Text ||
|#
```

**Result**

#|
|| **Header1** | **Header2** ||
|| Text | Text ||
|#

## Multiline content {#multirow}

Any multiline content can be placed in a table cell. For example, lists.

```markdown
#|
||Text
on two lines
|
- Potatoes
- Carrot
- Onion
- Cucumber||
|#
```

**Result**

#|
||Text
on two lines
|
- Potatoes
- Carrot
- Onion
- Cucumber||
|#

or even other table:

```markdown
#|
|| 1
|

Text before other table

#|
|| 5
| 6||
|| 7
| 8||
|#

Text after other table||
|| 3
| 4||
|#
```

**Result**

#|
|| 1
|

Text before other table

#|
|| 5
| 6||
|| 7
| 8||
|#

Text after other table||
|| 3
| 4||
|#


## Table attributes {#attributes}

A table can have attributes at three levels: for the entire table, for an individual row, and for an individual cell.

| Level | Syntax          | Where it goes                                                                                     |
| ----- | --------------- | ------------------------------------------------------------------------------------------------- |
| Table | `\|:{ ... }`    | On a dedicated line between `#\|` and the first `\|\|` row                                        |
| Row   | `\|\|:{ ... }`  | On the same line as `\|\|`, immediately after it                                                  |
| Cell  | `::{ ... }`     | At the start of the cell content, right after `\|` (or after `\|\|:{ ... }` for the first cell of a row) |

Example of a table with attributes at all three levels:

```markdown
#|
|:{header-rows="1"}
||:{class="row"} ::{align="center"} Header1 | Header2 | Header3 ||
||::{align="top-left"} Text | Text |::{align="top-right"} Text ||
|| Text | Text | Text ||
|#
```

{% note tip "Formatting rules" %}

- Each attribute block must be on the same line as its delimiter: a line break between `||` / `|` and the attribute block disables it, and the text becomes part of the cell content.
- No whitespace is allowed between `||` and `:{` (row attributes).
- No whitespace is allowed between `|` and `::{` (cell attributes, except for the first cell of a row).
- After `||:{...}`, whitespace and tabs are allowed before `::{...}` of the first cell on the same line.
- A table-attribute line (`|:{ ... }`) may appear multiple times between `#|` and the first `||` row; when keys match, later values override earlier ones.

{% endnote %}

### Table attributes {#table-attributes}

Attributes for the whole table are placed on a dedicated line between `#|` and the first `||` row:

```markdown
#|
|:{header-rows="1"}
|| **Header1** | **Header2** ||
|| Text | Text ||
|#
```

### Row attributes {#row-attributes}

Row attributes are placed right after the opening `||`:

```markdown
#|
||:{class="header"} **Header1** | **Header2** ||
|| Text | Text ||
|#
```

### Cell attributes {#cell-attributes}

Cell attributes are placed at the start of the cell content. For the first cell of a row — right after `||` (or after row attributes, if any); for other cells — right after `|`:

```markdown
#|
||::{align="center"} **Header1** | **Header2** ||
|| Text |::{align="top-right"} Text ||
|#
```

See [Text Alignment in Cells](#cell-align) for the available cell attributes.

## Header rows {#header-rows}

To mark the first N rows of a table as header rows, use the table attribute `header-rows="N"`. Header rows are rendered as `<th scope="col">` instead of `<td>`.

The value `N` must be a positive integer.

```markdown
#|
|:{header-rows="1"}
|| Header1 | Header2 | Header3 ||
|| Text | Text | Text ||
|| Text | Text | Text ||
|#
```

**Result**

#|
|:{header-rows="1"}
|| Header1 | Header2 | Header3 ||
|| Text | Text | Text ||
|| Text | Text | Text ||
|#

## Cell Merging {#span}

Cells can be merged vertically using the "^" symbol:

```markdown
#|
|| Header1                | Header2      ||
|| Text spanning two rows | Another text ||
|| ^                      | More text    ||
|#
```

**Result**

#|
|| Header1                | Header2      ||
|| Text spanning two rows | Another text ||
|| ^                      | More text    ||
|#


Horizontal merging is supported with the ">" symbol:

```markdown
#|
|| Header1                   | Header2     ||
|| Text spanning two columns | >           ||
|| Another text              | More text   ||
|#
```

**Result**

#|
|| Header1                   | Header2     ||
|| Text spanning two columns | >           ||
|| Another text              | More text   ||
|#

Merging symbols can be used together:

```markdown
#|
|| Header1                                | Header2     | Header3    || 
|| Text spanning two columns and two rows | >           | Text       ||
|| ^                                      | >           | More text  ||
|#
```

**Result**

#|
|| Header1                                | Header2     | Header3     ||
|| Text spanning two columns and two rows | >           | Text        ||
|| ^                                      | >           | More text   ||
|#

### Text Alignment in Cells {#cell-align}

To control the alignment of content within a cell, use the cell attribute `align`:

```markdown
#|
|| Header1                                | Header2 | Header3   ||
||::{align="center"} Text spanning two columns and two rows | > | Text      ||
|| ^                                      | >       | More text ||
|#
```

**Result**

#|
|| Header1                                | Header2 | Header3   ||
||::{align="center"} Text spanning two columns and two rows | > | Text      ||
|| ^                                      | >       | More text ||
|#

The following values are available:

- `top-left`
- `top-center`
- `top-right`
- `center`
- `bottom-left`
- `bottom-center`
- `bottom-right`

#### Legacy syntax {#cell-align-legacy}

{% note warning %}

Previously, alignment was set using the class syntax `{.cell-align-*}` inside the cell content. It still works for backward compatibility but is considered deprecated — use the `::{align="..."}` attribute instead.

{% endnote %}

```markdown
#|
|| Header1                                                     | Header2 | Header3   ||
|| Text spanning two columns and two rows {.cell-align-center} | >       | Text      ||
|| ^                                                           | >       | More text ||
|#
```

Deprecated values:

- `cell-align-top-left`
- `cell-align-top-center`
- `cell-align-top-right`
- `cell-align-center`
- `cell-align-bottom-left`
- `cell-align-bottom-center`
- `cell-align-bottom-right`

### Escaping Cell Merging Symbols

To include a merging symbol as plain text in a cell, use escaping with "",
i.e., "\^" and "\>".

```markdown
#|
|| Header1                 | Header2 | Header3 || 
|| Text in one cell        | \>      | Text    ||
|| \^                      | \>      | More text ||
|#
```

**Result**

#|
|| Header1                 | Header2 | Header3 ||
|| Text in one cell        | \>      | Text    ||
|| \^                      | \>      | More text ||
|#

## Adding "sticky header" to a table

For multi-line tables, just like for simple ones, you can add a "sticky header". To do this, you need to add the `{sticky-header}` attribute after the table.

```markdown
#|
|| Header1                          | Header2    | Header3        ||
|| Text in a single cell            | \>         | Text           ||
|| \^                               | \>         | More text      ||
|| Text in a single cell            | \>         | Text           ||
...
|| \^                               | \>         | More text      ||
|| Text in a single cell            | \>         | Text           ||
|| \^                               | \>         | **More text**  ||
|#

{sticky-header}
```

#|
|| Header1                           | Header2.   | Header3        ||
|| Text in a single cell             | \>         | Text           ||
|| \^                                | \>         | More text      ||
|| Text in a single cell             | \>         | Text           ||
|| \^                                | \>         | **More text**  ||
|| Text in a single cell             | \>         | Text           ||
|| \^                                | \>         | More text      ||
|| Text in a single cell             | \>         | Text           ||
|| \^                                | \>         | **More text**  ||
|| Text in a single cell             | \>         | Text           ||
|| \^                                | \>         | More text      ||
|| Text in a single cell             | \>         | Text           ||
|| \^                                | \>         | **More text**  ||
|| Text in a single cell             | \>         | Text           ||
|| \^                                | \>         | More text      ||
|| Text in a single cell             | \>         | Text           ||
|| \^                                | \>         | **More text**  ||
|| Text in a single cell             | \>         | Text           ||
|| \^                                | \>         | More text.     ||
|| Text in a single cell             | \>         | Text           ||
|| \^                                | \>         | **More text**  ||
|| Text in a single cell             | \>         | Text           ||
|| \^                                | \>         | More text      ||
|| Text in a single cell             | \>         | Text           ||
|| \^                                | \>         | **More text**  ||
|#

{sticky-header}
