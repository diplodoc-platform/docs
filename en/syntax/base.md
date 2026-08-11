# Basic markup

## Inline formatting {#line}

Use the markup methods below to format text fragments within a line.

Markup | Result
----- | -----
`**Bold text**` | **Bold text**
`_Italic_` | _Italic_
`**_Bold italic_**` | **_Bold italic_** 
`_**Also bold italic**_` | _**Also bold italic**_
`~~Strikethrough text~~` | ~~Strikethrough text~~
`Superscript^text^` | Superscript^text^
`##Monospaced text##` | ##Monospaced text##
`{red}(Colored text)` | {red}(Colored text)

To use subscript or underlined text, you need to enable additional plugins. For more details, see the section [Additional features](./additional.md).

## Paragraphs {#sections}

To create a paragraph, separate one block of text from another with a blank line.

```markdown
Параграф.

Следующий параграф.
```

**Result:**

Paragraph.

Next paragraph.

## Line breaks {#breaks}

To break a line, move the caret to a new line.
```markdown
Строка.
Следующая строка.
```

**Result:**

Line.
Next line.

To use two spaces at the end of a line instead of a caret break, set the value `breaks: false` in the [settings](../settings.md). 

## Headings {#headers}

The following heading levels are distinguished:
* first level (h1) for the page title;
* second (h2), third (h3), fourth (h4), etc. levels for subsection headings.

```markdown
# Заголовок h1
## Заголовок h2
### Заголовок h3
#### Заголовок h4
```

During the build, an anchor is generated for each heading. Anchors allow you to create [links](./links.md) that lead to document sections.

By default, an anchor in YFM is the heading text written in Latin transliteration. You can set an anchor manually by specifying it after the heading:

```markdown
## Заголовок h2 {#anchor-example}
```

To also generate anchors according to GitHub rules along with YFM-style anchors, set the value `supportGithubAnchors: true` in the [settings](../settings.md).

{% note warning %}

First-level headings are used only as page titles.
They have limitations: they do not work with anchors and are not displayed in the _page table of contents_.

{% endnote %}


## Quotes {#quotes}

To display a quote, use the following markup:

```markdown
> Цитирование
```

**Result:**

> Quoting

```markdown
> Цитирование
>> Вложенное цитирование
```

**Result:**

> Quoting
>> Nested quoting

## Escaping {#escaping}

To prevent a markup special character from being interpreted, escape it with the character `\`.

```markdown
Верхний^регистр^
Верхний\^регистр^
```
**Result:**

Superscript^text^
Superscript\^text^

## Comments {#comments}

Comments are markup elements that are not displayed in the built file. They are used to store information for SEO or document authors in the source text.

To add a comment, use the following markup. Make sure there is a blank line before the comment.

```markdown
[//]: # (Комментарий)
```

## Using HTML {#html}

By default, YFM escapes HTML. To disable escaping, set the value `allowHtml: true` in the [settings](../settings.md).
