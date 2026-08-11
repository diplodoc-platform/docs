---
noindex: true
---

# Changelog

## December 2022

### yfm-docs

#### 2.0.0

- [New interface for includers](./project/toc.md#includers).
- [Generic includer](./project/toc.md#includers-generic).
- [Open API includer](./project/toc.md#includers-open-api).
- [Unarchive includer](./project/toc.md#includers-unarchive).
- [Source Docs includer](./project/toc.md#includers-source-docs).

## November 2022

### yfm-docs

#### 1.31.0

- Added support for [definitions](./syntax/term.md).

### yfm-transform

#### 2.16.0

- Added support for inline markup in [task lists](./syntax/additional.md#tasks-list).

#### 2.15.0

- Added the `linkifyTlds` option, which allows you to configure the TLD for the linkify plugin.

## September 2022

### yfm-docs

#### 1.26.0

- services/leading: added support for [substitutions and conditional operators](./project/leading-page.md#subtitudes) in the title and description of the leading page.
- services/tocs: added support for [substitutions and conditional operators](./project/toc.md#subtitudes) in the document title.

#### 1.24.0

- includers/openapi: added the ability to [auto-generate documentation from an Open API specification](./project/toc.md#open-api) and include it in the main documentation.

### yfm-transform

#### 2.14.0

- Added sanitization of generated HTML. The default value is disabled. Parameter to enable: `needToSanitizeHtml: true`. You can override the default settings via the `sanitizeOptions` parameter.

#### 2.13.0

- Added syntax for [definitions](./syntax/term.md).

#### 2.12.0

- The ability to [set the image size](./syntax/media.md) is enabled by default.

## August 2022

### yfm-transform

#### 2.11.0

- Support for inline formatting in cut and note headings.

#### 2.10.0

- Added the `needFlatListHeadings?: boolean;` parameter, which allows you to generate a flat list of all document headings in `transform().result.headings`. The default value is `false`.

## July 2022

### yfm-docs

#### 1.23.0

- include/includers: the ability to integrate third-party formats into documentation.
- include/includers/sourcedocs: the ability to integrate sourcedocs documentation into yfm documentation.
  [Includers](./project/toc.md#includers)

## June 2022

### yfm-transform

#### 2.9.0

- Added a plugin for [file links](./syntax/links.md#files).

#### 2.8.0

- Whitespace inside inline conditions is no longer removed.

#### 2.7.0

- Removed the single-page logic from plugins (the change was temporarily reverted in version 2.8.2).

## May 2022

### yfm-transform

#### 2.6.0

- Added a plugin for the [task list syntax](./syntax/additional.md#tasks-list).

## April 2022

### yfm-docs

#### 1.22.0

- Added filtering of the page title and page title in meta information on the landing page (index.yaml).
- Added filtering of the page title in the table of contents (toc.yaml).

#### 1.21.0

- Added support for symlinks with a relative path.

## March 2022

### yfm-docs

#### 1.20.0

- Added filtering of the description on the landing page (index.yaml).

#### 1.19.0

- The linter runs in parallel with the build.
- Added support for the `--link-disabled`, `--build-disabled`, and `--add-map-file` arguments, which default to `false`.
  [For more details](tools/docs/settings.md).

### yfm-transform

#### 2.5.0

- Rewritten in TypeScript.

## December 2021

### yfm-docs

#### 1.18.0

Updated the YFM version to 2.4. Added support for [monospaced font](./syntax/base.md) and [multiline tables](./syntax/tables/multiline.md).

#### 1.17.0

- After building documentation in preprocessing mode (with output-format=md), we no longer remove not_var from syntax that resembles variables.
  [Variable substitutions](./syntax/vars.md#subtitudes).

#### 1.16.0

- Added table of contents inclusion modes: `root_merge`, `merge`, `link`. [For more details](./project/toc.md#include-mode).

- When including the table of contents in the `root_merge` and `merge` modes, the original path to the sources will be added
to the `sourcePath` field of the meta information.

### yfm-transform

#### 2.4.0

- Support for [multiline tables](./syntax/tables/multiline.md) is enabled by default.

#### 2.3.0

- Added support for [monospaced font](./syntax/base.md).

## November 2021

### yfm-docs

#### 1.15.0

- Added the ability to include `toc.yaml` with its elements added to the same level of the table of contents. [For more details](./project/toc.md#include-as-pages).

#### 1.14.0

- Added the ability to [configure the linter](./project/lint.md).

### yfm-transform

#### 2.2.0

- Added the ability to override delimiters in the [markdown-it-attrs](https://www.npmjs.com/package/markdown-it-attrs) plugin.

## October 2021

### yfm-transform

#### 2.1.0

- Added experimental support for multiline tables.

## September 2021

### yfm-docs

#### 1.13.0

- YFM2 is used.

### yfm-transform

#### 2.0

- YFM can be used on the client.
- The plugin connection scheme has been changed.
- The [markdown-it-attrs](https://www.npmjs.com/package/markdown-it-attrs) plugin is always enabled.
- The [highlight.js](https://www.npmjs.com/package/highlight.js) package must be installed separately.

## July 2021

### yfm-docs

#### 1.12.0

- Disabled the use of the experimental YFM linter.

### yfm-transform

#### 1.9.0

- Added the ability to enable support for GitHub-compatible (GFM) anchors.

## June 2021

### yfm-docs

#### 1.11.0

- Enabled the use of the experimental YFM linter.

#### 1.10.0

- Added the ability to configure redirects using a special file. Static builds do not support it.

#### 1.9.0

- Added support for sections available only via a direct link.

### yfm-transform

#### 1.8.0

- Added experimental linter support.

## April 2021

### yfm-docs

#### 1.8.0

- Added the ability to collect file contributors into metadata. Only GitHub is supported out of the box. It is not displayed visually, but can be used by a custom viewer.

## March 2021

### yfm-docs

#### 1.7.0

- Added full variable disabling: conditions are not evaluated, values are not substituted.

### yfm-transform

#### 1.7.0

- Added full variable disabling: conditions are not evaluated, values are not substituted.

## January 2021

### yfm-docs

#### 1.6.0

- You can now build a document as a single HTML file.

#### 1.5.0

- Refactoring and bug fixes.

#### 1.4.0

- Added the ability to disable evaluation of conditions with variables.

### yfm-transform

#### 1.6.0

- Added support for loops, filters, and functions.

#### 1.5.0

- Added the ability to use the `not_var` flag for variables that should not be substituted with values. For example, `not_var{{ variable_name }}`.

## October 2020

### yfm-docs

#### 1.3.0

- Added the ability to deploy built files to S3.

## August 2020

### yfm-docs

#### 1.2.0

- Added the ability for users to change the font size in the documentation interface, enable dark theme, and hide tables of contents.

### yfm-transform

#### 1.4.0

- Added the ability to use '|' in variables.

## July 2020

### yfm-transform

#### 1.3.0

- Updated styles for base elements.

#### 1.2.0

- Added support for video embedding.

#### 1.1.0

- Added support for multiple custom anchors per heading.

## June 2020

### yfm-docs

#### 1.1.0

- Added a quiet mode without build logs output.
