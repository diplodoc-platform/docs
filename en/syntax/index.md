# Syntax

Diplodoc uses **Yandex Flavored Markdown (YFM)** syntax — a Markdown dialect with an additional set of tools for transforming Markdown into HTML and building documentation projects.

Features:

* Compatibility with the [CommonMark Spec](https://spec.commonmark.org/) standard.
* The ability to [connect](../plugins/external.md) third-party markdown-it plugins.
* Security: HTML is escaped by default.
* Dynamic validation.
* Building a documentation project.

The following are used for formatting:
* [basic markup](./base.md);
* [links](./links.md);
* [lists](./lists.md);
* [simple](./tables/gfm.md) and [multiline tables](./tables/multiline.md);
* [notes](./notes.md);
* [cuts, tabs, and radio buttons](./interactive-elements/index.md);
* [images and videos](./media.md);
* [code fragments](./code.md);
* [tooltips](./term.md);
* [variables](./vars.md).

In addition to the elements included in the package, you can connect [additional features](./additional.md) via markdown-it plugins. 
