# Additional features

The following markup elements are not supported by default, but can be added using [markdown-it plugins](https://www.npmjs.com/search?q=keywords:markdown-it-plugin).

For more information about how to add additional plugins, see the  [instructions](../plugins/import.md).

## Subscript {#sub}

**Plugin:** [markdown-it-sub](https://www.npmjs.com/package/markdown-it-sub)

To output a character in subscript, add `~` on both sides.

```markdown
H~2~O
```

You can vote to include subscript support in YFM by default in [GitHub issues](https://github.com/yandex-cloud/yfm-transform/issues/70).

## Underlined text {#underline}

**Plugin:** [markdown-it-ins](https://www.npmjs.com/package/markdown-it-ins)

To underline text, add `++` on both sides.

```markdown
++qwerty++
```

You can vote to include underlined text support in YFM by default in [GitHub issues](https://github.com/yandex-cloud/yfm-transform/issues/71).

## Footnotes {#footnotes}

**Plugin:** [markdown-it-footnote](https://www.npmjs.com/package/markdown-it-footnote)

Use footnotes for additional information without complicating the text. Footnotes have two parts connected with tags:

* The link in the document text, which is displayed as superscript.
* A block of additional information. It's usually placed at the end of the document.

```markdown
Here's a simple footnote,[^1] and here's a longer one.[^bignote]

[^1]: This is the first footnote.

[^bignote]: Here's one with multiple paragraphs and code.
```

You can vote to include footnote support in YFM by default in [GitHub issues](https://github.com/yandex-cloud/yfm-transform/issues/72).

## Task lists {#tasks-list}

Import plugin from package like so:
```
const checkbox = require('@diplodoc/transform/lib/plugins/checkbox');
```

The task list is a list of checkboxes. A normal item is represented by the `- [ ]` symbol, a checked one by `- [x]`. You can use [line formatting](./base.md#line) in the task description.

```markdown
- [x] ~~Write the press release~~
- [ ] Update the website
- [ ] Contact the media
```

You can vote to include task list support in YFM by default in [GitHub issues](https://github.com/yandex-cloud/yfm-transform/issues/73).

## Formulas {#formulas}

**Plugin:** [markdown-it-katex](https://www.npmjs.com/package/markdown-it-katex) (see [other versions](https://www.npmjs.com/search?q=markdown-it-katex))

The plugin uses the KaTeX library to display mathematical symbols. Example of a formula:

```markdown
$\sqrt{3x-1}+(1+x)^2$
```
