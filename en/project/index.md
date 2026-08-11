# Project structure

The basic project includes a [table of contents file](./toc.md) and content files.

Recommended additional elements:

- [Landing page](./leading-page.md)
- Directories for [images](../syntax/media.md#images)
- Directories for [content reuse](../syntax/includes.md)
- [Configuration file](../settings.md)
- [Variable presets](./presets.md)

**Example of project structure**

```
input-folder
|-- .yfm # файл конфигурации
|-- toc.yaml # оглавление
|-- presets.yaml # пресеты переменных
|-- index.yaml # разводящая страница
|-- pages # файлы с контентом
    |-- faq.md
    |-- how-to.md
|-- _assets # каталог с изображениями
    |-- image1.png
    |-- image2.png
|-- _includes # каталог с файлами для переиспользования
    |-- faq_shared_block.md
```

## Supported file types {#file-types}

When building the project, files of the following types are copied to the build results:

- images `svg`, `png`, `gif` , `jpeg`/`jpg`, `bmp`, `webp`, `ico`
- documents `pdf`, `docx`, `xlsx`, `csv`, `vsd`, `pptx`
- files `txt` and `yml`/`yaml`
