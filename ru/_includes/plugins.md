#|
|| Название плагина | Описание | Параметры | Подключен по умолчанию |
|| **Anchors**| Автоматическое генерирование [якорей для заголовков](../syntax/base.md#headers) | `extractTitle`: учитывать заголовок первого уровня</br> Тип: `bool`, По умолчанию: `false` </br></br>`supportGithubAnchors`: генерировать дополнительные якоря, совместимые с GitHub</br> Тип: `bool`, По умолчанию: `false` </br></br>`disableCommonAnchors`: отключить формирование якорей заголовков</br> Тип: `bool`, По умолчанию: `false` | + ||
|| **Code**| Отображение кнопки копирования в [блоках кода](../syntax/code.md#block) | - | + ||
|| **Cut** | Поддержка разметки [катов](../syntax/interactive-elements/cuts.md) | - | + ||
|| **Deflist**| Поддержка разметки [списка определений](../syntax/lists.md#terms) | - | + ||
|| **File** | Поддержка разметки [объектов файлов](../syntax/links.md#files) | `fileExtraAttrs`: дополнительные атрибуты для ссылки | + ||
|| **Tasks list** | Добавление [списка задач](../syntax/additional.md#tasks-list) | `divClass`: classname для `div`, который оборачивает чекбокс</br> Тип: `string`, По умолчанию: `checkbox` </br></br> `idPrefix`: перфикс для id чекбокса</br> Тип: `string`, По умолчанию: `checkbox` | - ||
|| **Images** | Добавление [изображений](../syntax/media.md#images) | `assetsPublicPath`: путь до иконок</br> Тип: `string`, По умолчанию: / | - ||
|| **Imsize** | Задание размера изображений | - | - ||
|| **Includes** | Переиспользование контента в документе | `getVarsPerFile`: функция, которая по пути к файлу возвращает вычисленные переменные</br> Тип: `function`, По умолчанию: -  | - ||
|| **Links** | Расширение [синтаксиса ссылок](../syntax/links.md) | - | - ||
|| **Monospace** | [Моноширинный шрифт](../syntax/base.md) | - | + ||
|| **Meta** | Добавление [метаданных](../syntax/meta.md#meta) в начало файлов | - | + ||
|| **Notes** | Поддержка разметки [заметок](../syntax/notes.md) | `lang`: язык для отображения типа заметки</br> Тип: `string`, По умолчанию: ru | + ||
|| **Sup** | Вывод текста в [верхнем регистре](../syntax/base.md#line) | - | + ||
|| **Table** | Поддержка [многострочных таблиц](../syntax/tables/multiline.md) | - | + ||
|| **Tabs** | Поддержка разметки [табов](../syntax/interactive-elements/tabs.md) | - | + ||
|| **Video** | Добавление [видео](../syntax/media.md#video) | - | + ||
|#