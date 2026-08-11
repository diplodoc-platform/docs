# Additional features

Below are the markup elements that are not supported by default but can be enabled using [markdown-it plugins](https://www.npmjs.com/search?q=keywords:markdown-it-plugin).

For instructions on how to enable an additional plugin, see the [guide](../plugins/index.md).

## Subscript {#sub}

**Plugin:** [markdown-it-sub](https://www.npmjs.com/package/markdown-it-sub)

To render a character in subscript, wrap it with `~` on both sides.

```markdown
H~2~O
```

You can vote for subscript support in YFM by default in [GitHub issues](https://github.com/yandex-cloud/yfm-transform/issues/70).

## Underlined text {#underline}

**Plugin:** [markdown-it-ins](https://www.npmjs.com/package/markdown-it-ins)

To underline text, wrap it with `++` on both sides.

```markdown
++qwerty++
```

You can vote for underlined text support in YFM by default in [GitHub issues](https://github.com/yandex-cloud/yfm-transform/issues/71).

## Footnotes {#footnotes}

**Plugin:** [markdown-it-footnote](https://www.npmjs.com/package/markdown-it-footnote)

Use footnotes when you need to provide additional information without complicating the text. Footnotes consist of two parts linked by labels:

* a reference in the document text, displayed as a superscript;
* a block of additional information. Usually placed at the end of the document.

```markdown
Here's a simple footnote,[^1] and here's a longer one.[^bignote]

[^1]: This is the first footnote.

[^bignote]: Here's one with multiple paragraphs and code.
```

You can vote for footnote support in YFM by default in [GitHub issues](https://github.com/yandex-cloud/yfm-transform/issues/72).

## Task lists {#tasks-list}

A task list is a list of checkboxes. An unchecked item corresponds to the symbol `- [ ]` , and a checked one to `- [x]`. You can use [inline formatting](./base.md#line) in the task description.

[Example of enabling](../plugins/installed.md#example)

You can vote for task list support in YFM by default in [GitHub issues](https://github.com/yandex-cloud/yfm-transform/issues/73).

## Formulas {#formulas}

**Plugin:** [markdown-it-katex](https://www.npmjs.com/package/markdown-it-katex) (see [other versions](https://www.npmjs.com/search?q=markdown-it-katex))

The plugin uses the KaTeX library to render mathematical notation.

[Example of enabling](../plugins/external.md#example)
