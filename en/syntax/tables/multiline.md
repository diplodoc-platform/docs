# Multiline tables

Tables with support inside cells for more than just simple content. Example, [lists](../lists.md), [code snippets](../code.md) and other tables.

### Syntax {#syntax}

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

### Multiline content {#multirow}

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
