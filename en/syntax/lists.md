# Lists

The following types of lists are available:

* Numbered: For describing a sequence of actions.
* Bulleted: For listing elements when the order isn't important.
* Definition: For creating glossaries.

Each list type can contain any markup elements and nested items.

## Numbered list {#numbered}

To make a numbered list, use numbers with the `.` or `)` symbol. Numbering is performed dynamically during building, so the order of the numbers is not important.

```markdown
1. First item.
1. Second item.
1. Third item.
```

**Result**

1. First item.
1. Second item.
1. Third item.

## Bulleted list {#marked}

To make a bulleted list, use the `*`, `-`, or `+` symbols.

For example:

```markdown
* List item.
* List item.
* List item.
```

**Result**

* List item.
* List item.
* List item.

## Definition list {#terms}

To make a definition list, use the `:` symbol.

```markdown
Term 1

: Definition 1

Term 2

: Definition 2
```

**Result**

Term 1

: Definition 1

Term 2

: Definition 2

## Nested lists {#sublist}

To create a nested list, add an indent (from two to five spaces) before the elements of the child list. The recommended indentation is four spaces.

```markdown
1. First item.
    1. Nested item.
    1. Nested item.
1. Second item.
```

**Result**

1. First item.
    1. Nested item.
    1. Nested item.
1. Second item.

```markdown
* List item.
    * Nested item.
    * Nested item.
* List item.
```

**Result**

* List item.
    * Nested item.
    * Nested item.
* List item.

```
Term 1

: Definition 1
    
    Term 1.1

    : Definition 1.1

Term 2

: Definition 2
```

**Result**

Term 1

: Definition 1

    Term 1.1
    
    : Definition 1.1

Term 2

: Definition 2

