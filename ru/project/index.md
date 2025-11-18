# Документационный проект

YFM позволяет создавать и поддерживать документационные проекты.

**Пример**: [документация Yandex.Cloud](https://github.com/yandex-cloud/docs).

## Структура проекта

Базовый проект включает:
- [Файл оглавления](./toc.md)
- Файлы с контентом

Рекомендуемые дополнительные элементы:
- [Разводящая страница](./leading-page.md)
- Каталоги для [изображений](../syntax/media.md#images)
- Каталоги для [переиспользования контента](../syntax/includes.md)
- [Файл конфигурации](../settings.md#config)
- [Пресеты переменных](./presets.md)

**Пример структуры проекта**

```
input-folder
|-- .yfm
|-- toc.yaml
|-- presets.yaml
|-- index.yaml
|-- pages
    |-- faq.md
    |-- how-to.md
|-- _assets
    |-- image1.png
    |-- image2.png
|-- _includes
    |-- faq_shared_block.md
```
