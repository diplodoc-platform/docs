
# Yandex Flavored Markdown
**Yandex Flavored Markdown (YFM)** is a Markdown dialect and a set of tools for transforming Markdown to HTML in real time and [building](./tools/docs/index.md) complete documentation projects.

* Corresponds to [CommonMark Spec](https://spec.commonmark.org/).
* Includes its own [set of plugins](./plugins/index.md) with additional features and markup elements.
* [Fast](https://www.npmjs.com/package/markdown-it#benchmark).
* Expandable: you can [add](./plugins/import.md) any plugin for markdown-it or [write your own](https://github.com/markdown-it/markdown-it/tree/master/docs).
* Safe: HTML is escaped by default.
* Uses dynamic validation.
* Allows you to build a documentation project.

## Syntax {#syntax}

The Yandex Flavored Markdown syntax is based on [CommonMark Spec](https://spec.commonmark.org/) and has been supplemented with unique elements from other markup languages and template engines.

In particular:

* [Notes](./syntax/notes.md)
* [Cuts and tabs](./syntax/cuts-tabs.md)
* [Video](./syntax/media.md#video)
* [Variables](./syntax/vars.md)
* [Reusable content](./project/includes.md)

For more information about all markup elements, see [Syntax](./syntax/index.md).

## Creating documentation projects {#project}

[Builder](./tools/docs/index.md) allows you to build a complete documentation project: with navigation, internal links, and full support for Yandex Flavored Markdown.

A built project is a set of static HTML files that can be viewed locally or on a host, in GitHub Pages, or in [S3](./tools/docs/publish-s3.md). It may include:

* [Table of contents](./project/toc.md).

* [Leading pages](./project/leading-page.md) for quick navigation.

* [Variable presets](./project/presets.md) to support multiple versions of documentation from the same source files.

* [Reusable content](./project/includes.md).

* Custom display settings:
    * Wide format.
    * Current article navigation.
    * Dark theme.
    * Text size.

  You can try changing the settings right now: click ![settings-icon](./_images/user-settings.png) in the upper-right corner.

In addition to building all files in HTML, you can build to a [single-page](./tools/docs/singlepage.md) and in [YFM](./tools/docs/build.md#yfm).

## Under development {#future-releases}

Future YFM releases are expected to include the following features:

* Static linter.
* YFM generators from proto, OpenAPI, auto-generated Java, Python, C++, and Go documentation.
* Customer satisfaction score (CSAT) on documentation pages.
* Automatic local rebuild when changes are made.
* Displaying contributors on pages.
* Free hosting for open-source documentation projects.
