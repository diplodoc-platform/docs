# Documentation project

YFM supports creating and maintaining documentation projects of any size.

**Example**: [Yandex.Cloud documentation](https://github.com/yandex-cloud/docs).

## Project structure

In the most basic case, a project consists of a [table of contents file](./toc.md) and files with content.

To optimize the documenting process and improve the appearance of pages, you can additionally include:

* [A leading page](./leading-page.md) for quick navigation.
* [Variable presets](./presets.md) to support multiple versions of documentation from the same source files.
* [A configuration file](./config.md) with project settings.
* Folders for [reusing content](./includes.md) and storing [images](../syntax/media.md#images).

## Example

```
input-folder
|-- .yfm (Configuration file)
|-- toc.yaml (Table of contents)
|-- presets.yaml (Variable presets)
|-- index.yaml (Leading page)
|-- pages (Content files)
    |-- faq.md
    |-- how-to.md
|-- _assets (Folder with images)
    |-- image1.png
    |-- image2.png
|--_includes (Folder with files to be reused)
    |-- faq_shared_block.md
```

