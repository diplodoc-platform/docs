# Yandex Flavored Markdown

**Yandex Flavored Markdown (YFM)** — диалект Markdown с дополнительным набором инструментов для трансформации Markdown в HTML и [сборки](./tools/docs/index.md) документационных проектов.

Особенности:

* Совместимость со стандартом [CommonMark Spec](https://spec.commonmark.org/).
* Включает набор [плагинов](./plugins/index.md) с дополнительными элементами разметки.
* Возможность [подключения](./plugins/external.md) сторонних плагинов markdown-it и [создания собственных](https://github.com/markdown-it/markdown-it/tree/master/docs).
* Безопасность: HTML экранируется по умолчанию.
* Динамическая валидация.
* Сборка документационного проекта.

## Синтаксис {#syntax}

Синтаксис Yandex Flavored Markdown основан на [CommonMark Spec](https://spec.commonmark.org/) и дополнен элементами из других языков разметки и шаблонизаторов:

* [заметки](./syntax/notes.md);
* [каты, табы и радиобаттоны](./syntax/interactive-elements/index.md);
* [всплывающие окна](./syntax/term.md);
* [видео](./syntax/media.md#video);
* [переменные](./syntax/vars.md);
* [переиспользование контента](./syntax/includes.md).

Подробнее в разделе [Синтаксис](./syntax/index.md).

## Создание документационных проектов {#project}

[Builder](./tools/docs/index.md) позволяет собирать документационные проекты с навигацией и поддержкой YFM.

Собранный проект представляет собой набор статических HTML, которые можно просмотреть локально или разместить на хостинге, в GitHub Pages или [S3](./tools/docs/publish-s3.md). Он может включать:

* [Оглавление документа](./project/toc.md).
* [Разводящие страницы](./project/leading-page.md) для навигации.
* [Пресеты переменных](./project/presets.md) для поддержки разных версий документации из одних и тех же исходных файлов.
* [Переиспользование контента](./syntax/includes.md).
* Пользовательские настройки отображения:
    * широкий формат;
    * навигация по текущей статье;
    * темная тема;
    * размер текста.

  Чтобы изменить настройки, нажмите ![settings-icon](./_images/user-settings.svg) в верхнем правом углу.

Кроме стандартной сборки всех файлов в HTML доступна [сборка в YFM](./tools/docs/build.md#yfm).
