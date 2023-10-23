# Basic markup

## Line formatting {#line}

Use the markup methods below to format a text fragment in a line.

| Markup                   | Result |
|--------------------------| ----- |
| `**Bold text**`          | **Bold text** |
| `_Italic_`               | _Italic_ |
| `**_Bold italic_**`      | **_Bold italic_** |
| `_**Also bold italic**_` | _**Also bold italic**_ |
| `~~Strikethrough text~~` | ~~Strikethrough text~~ |
| `Super^script^`          | Super^script^ |
| `##Monospaced text##`    | ##Monospaced text##

To use subscript or underlined text, you need to add additional plugins. For more information, see [Additional features](./additional.md).

## Headers {#headers}

There are 4 levels of headers:

* The first level (h1) is for the page header (title).
* The second (h2), third (h3), and fourth (h4) levels are for subsection headers.

```markdown
# h1 header
## h2 header
### h3 header
#### h4 header
```

During the build, an anchor is created for each header. Anchors allow you to create [links](./links.md) to document sections.

By default, the anchor in YFM is the header text written in Latin letters. You can set the anchor manually by specifying it after the header:

```markdown
## h2 header {#anchor}
```

To simultaneously generate anchors following GitHub rules with the YFM anchors, in the [settings](../settings.md), set `supportGithubAnchors: true`.

## Paragraphs {#sections}

To create a paragraph, separate one block of text from another with an empty line.

```markdown
Paragraph.

Next paragraph.
```

**Result**

Paragraph.

Next paragraph.

## Line breaks {#breaks}

To move a line, move the carriage.

```markdown
Line.
Next line.
```

**Result**

Line.
Next line.

To use two spaces at the end of the line instead of a carriage return, in the [settings](../settings.md), set `breaks: false`.

## Quotes {#quotes}

```markdown
> Quote
```

**Result**

> Quote

```markdown
> Quote
>> Nested quotes
```

**Result**

> Quote

>> Nested quotes

## Escaping {#escaping}

To prevent a markup syntax symbol from being interpreted, escape it with the `\` symbol.

```markdown
Super^script^
Super\^script^
```

**Result**

Super^script^
Super\^script^

## Using HTML {#html}

By default, YFM escapes HTML. To disable escaping, in the [settings](../settings.md), set `allowHTML: true`.

