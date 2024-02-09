# Code snippets

You can add a code snippet to the text of a paragraph or make it a separate block.

## In the text {#inline}

To add a code snippet to the text, use the ` symbol.

```markdown
`Code snippet` in the text.
```

**Result**

`Code snippet` in the text.

{% note tip %}

We recommend using no more than 100 characters, because the text in these fragments doesn't wrap. For a larger number of characters, make the code a separate block.

{% endnote %}

## Separate block {#block}

To make a code snippet a separate block, separate it from the rest of the text on both sides with the characters ```.

To highlight the syntax, specify the language in which the code is written in the initial line. For example:

````markdown
```sql
  price= '2000'
  size= '24'
  color= 'primary'
  variant= 'detailed'
```
````

The list of available languages can be found on [Github](https://github.com/highlightjs/highlight.js/tree/master/src/languages). For information on how to transfer an additional set of languages, see [Connecting an additional language](../tools/transform/highlight.md#add).

