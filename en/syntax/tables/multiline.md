# Multiline tables

Tables with support inside cells for more than just simple content. Example, [lists](../lists.md), [code snippets](../code.md) and other tables.

## Syntax {#syntax}

* a table starts with `#|` and ends with `|#`;
* lines start and end with `||`;
* the cells are separated by a symbol `|`.

{% note tip "Headers of table" %}

Multiline tables do not contain headers, but they can be done by applying formatting to the content of the cells of the first row. For example, highlighting them in bold.

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

### Text Alignment in Cells

To control the alignment of text in cells, you can use attribute syntax within the cells:

```markdown
#|
|| Header1                                                     | Header2     | Header3    || 
|| Text spanning two columns and two rows {.cell-align-center} | >           | Text      ||
|| ^                                                           | >           | More text  ||
|#
```

**Result**

#|
|| Header1                                           | Header2     | Header3 ||
|| Text spanning two columns and two rows {.cell-align-center} | >        | Text      ||
|| ^                                                | >        | More text  ||
|#

The following alignment options are available:

- cell-align-top-left
- cell-align-top-center
- cell-align-top-right
- cell-align-center
- cell-align-bottom-left
- cell-align-bottom-center
- cell-align-bottom-right

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
