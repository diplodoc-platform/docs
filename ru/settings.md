# Настройки YFM-проекта

В зависимости от используемого инструмента вы можете задать стандартные настройки YFM-проекта одним из способов:
* в [файле конфигурации](#config);
* в качестве параметра функции ([Transformer](./tools/transform/settings.md));
* через ключи запуска ([Builder](./tools/docs/settings.md)).

## Файл конфигурации {#config}

В файле конфигурации можно задать:

* [параметры сборки YFM](#build);
* [параметры отображения в интерфейсе](#docs-viewer);
* [настройки трансформации YFM в HTML](tools/transform/settings.md).

По умолчанию используется файл `.yfm` в корне документа. При сборке можно указать путь до другого файла с помощью [ключа запуска](tools/docs/settings.md) `--config`. 

### Структура

Файл конфигурации `.yfm` содержит список всех параметров в формате YAML:

```yaml
parameter: value
parameter: value
```
* `parameter` — имя задаваемой настройки;
* `value` — значение настройки.

{% cut "Пример файла `.yfm`" %}

```yaml
# Параметры сборки
strict: true
breaks: false

singlePage: true

apply-presets: true
varsPreset: 'external'

langs: ['en', 'ru']

# Параметры отображения в интерфейсе
docs-viewer:

  project-name: project-name
  is-new-external: true

  no-index: true

  github-url-prefix: https://github.com/yandex-cloud/yfm-documentation/blob/master

  langs: ['en', 'ru']
  metrika: 678489

  themes: [light]

  favicon-src: https://raw.githubusercontent.com/yandex-cloud/yfm-documentation/master/_images/logo_blue_32x32.png

  # Настройки логотипа
  logo-options:
    url: https://diplodoc.com/docs/{lang}/

    src: https://storage.yandexcloud.net/docs-external/yfm-documentation/_images/logo.svg
    src-dark: https://storage.yandexcloud.net/docs-external/yfm-documentation/_images/logo.svg

    src-mobile: https://storage.yandexcloud.net/docs-external/yfm-documentation/_images/logo.svg
    src-mobile-dark: https://storage.yandexcloud.net/docs-external/yfm-documentation/_images/logo.svg

    src-preview: https://storage.yandexcloud.net/docs-external/yfm-documentation/_images/share-logo-dark.svg

    # Если логотипа нет, то вместо него можно задать текст
    title: Yandex Flavored Markdown
```

{% endcut %}

{% note info %}

Обязательные параметры:

{% list tabs %}

- yandex.ru/dev

  ```
  docs-viewer:
    project-name: dev-<project-name>
    is-external: true
    internal-s3: true
  ```

- yandex.ru/support2

  ```
  docs-viewer:
    project-name: support-<project-name>
    is-new-external: true
  ```

{% endlist %}

{% endnote %}

## Параметры сборки {#build}

#|
|| **Параметр** | **Описание** | **Тип** | **Значение по умолчанию** ||
|| `add-map-file` | Создает json-файл со всеми путями проекта. | `bool` | `false` ||
|| `add-system-meta` | Добавлять метаданные с системными переменными из пресетов в файлы документации.
В файле [presets.yaml](project/presets) можно задать секцию `system`, содержимое которой будет добавлено в meta-данные каждой страницы.
Отображается при генерации файлов в формате md.
 | `bool` | `false` ||
|| `allowHTML` | Разрешить [использование html-элементов](syntax/base.md#html) в разметке. | `bool` | `false` ||
|| `apply-presets` | Применять ли пресеты переменных. 

[Подробнее о пресетах](project/presets.md). | `bool` | `false` ||
|| `breaks` | [Переносить строки](syntax/base.md#breaks) по символу перевода каретки. | `bool` | `true` ||
|| `conditionsInCode` | Разрешить блоки кода с условиями с помощью [операторов](syntax/vars#conditions). | `bool` | `false` ||
|| `langs` | Массив языков, участвующих в сборке. | ||
|| `lint` | Подключить [файл линтера](./project/lint.md). | `bool` | `false` ||
|| `merge-includes` | Параметр, который отвечает за корректную обработку включений [инклюдов](./project/includes.md) при сборке документов в формате `md`. Позволяет объединять содержимое инклюдов в единый документ.

{% note warning %}

Работает только вместе с параметром `output-format: md`.

{% endnote %} 

| `bool` | `false` ||
|| `needToSanitizeHtml` | Определяет разрешенные и запрещенные HTML-теги, атрибуты, стили и другие элементы при очистке HTML-контента. Работает в связке с параметром `needToSanitizeHtml`. | `bool` | `false` ||
|| `output-format` | Формат файлов итоговой сборки. | `string` (`html` или `md`) | `html` ||
|| `pdf` | При значении `pdf: true` для документа будет собираться pdf-версия. Чтобы сборка прошла корректно, обязательно должен быть указан параметр `singlePage: true`. После завершения сборки в левом нижнем углу документа отображается значок собранного PDF-файла, который можно скачать. | `bool` | `false` ||
|| `remove-hidden-toc-items` | Убрать из оглавления все объекты, отмеченные атрибутом `hidden: true`. | `bool` | `false` ||
|| `singlePage` | Собирать [одностраничную сборку](tools/docs/singlepage.md) из всех файлов проекта. | `bool` | `false` ||
|| `strict` | Cтрогий режим сборки, все предупреждения YFM отображаются как ошибки. | `bool` | `false` ||
|| `varsPreset` | Имя пресета переменных, который необходимо использовать при сборке. | `string` | ||
|# {wide-content}

## Параметры отображения в интерфейсе {#docs-viewer}

#|
|| **Название** | **Описание** | **Тип** | **Значение по умолчанию** ||
|| `analytics` | Конфигурация для модуля аналитки. | `Object` | `undefined`  ||
|| `analytics.gtm` | Настройки аналитики Google Tag Manager. | `Object` | `undefined` ||
|| `analytics.gtm.id` | Идентификатор Google Tag Manager в формате GTM. | `string` | `undefined` ||
|| `analytics.gtm.mode` | Тип уведомления перед отправкой событий `base` или `notification`. | `string` | `base` ||
|| `disableLiquid` | Отключить использование [переменных](syntax/vars.md). | `bool` | `false` ||
|| `favicon-src` | Иконка во вкладке браузера.

Можно использовать любую ссылку на изображение, подходящее под стандартные требования к фавиконкам. |  |  ||
|| `github-url-prefix` | Github-префикс до директории корня документации, если она хранится на Github.

Если параметр не задан, внешним пользователям не будет отображаться ссылка на редактирование страницы (иконка карандаша в правом верхнем углу). | | ||
|| `is-external` /  `is-new-external` |
Проект будет доступен внешним пользователям, если установлено значение параметра `true`.

Параметр `is-external` используется для проектов на yandex.ru/dev или yandex.ru/legal. Для проектов на yandex.ru/support2 используется параметр `is-new-external`. | `bool` | `true` ||
|| `lang` | Язык по умолчанию для локализации. 
Для [следующих языков](https://github.com/diplodoc-platform/client/blob/34a5139620874627cfdebe9be74902cf9d3961b1/src/constants.ts#L15) контент будет отображаться в формате RTL (right-to-left). | `string` | `ru` ||
|| `langs` | Массив языков, отображаемых в интерфейсе документации. Язык по умолчанию при открытии страницы — первый элемент в массиве.

{% cut "Пример структуры проекта с несколькими языками" %}

```
input-folder
|-- .yfm
|-- ru
    |-- toc.yaml
    |-- index.md
|-- en
    |-- toc.yaml
    |-- index.md
```

{% endcut %}

{% note warning %}

Если структура проекта содержит языковые папки, то указывать параметр обязательно, даже если в проекте используется только один язык.

{% endnote %}

|
`string` ||
|| `linkify` | Преобразовывать ссылкоподобные строки в ссылки.

Пример ссылки: https://diplodoc.com/ru или diplodoc.com/ru.
| `bool` | `false` ||
|| `linkifyTlds` | Настройка tld для плагина linkify. | `string \| string[]` | `undefined` ||
|| `logo-options` |
Настройки логотипа:

* `src` — ссылка на изображение для светлой темы;

* `src-dark` — ссылка на изображение для темной темы;

* `src-mobile` — ссылка на изображение для светлой темы на мобильных;

* `src-mobile-dark` — ссылка на изображение для темной темы на мобильных;

* `src-preview` — логотип для превью ссылки при шеринге на внешних ресурсах, применяется стандарт [OpenGraph](https://ogp.me/);

* `url` — ссылка, на которую перенаправляет при нажатии на логотип. Можно задать шаблон ссылки с параметром `{lang}`, чтобы он заменился на текущий язык документации при переходе. Например, ссылка `https://diplodoc.com/docs/{lang}/` при переходе из документации на русском языке будет вести на `https://diplodoc.com/docs/ru/`;

* `title` — текст, который показывается вместо логотипа, если он не задан. 

Если логотип для темной темы не указан, используется изображение для светлой темы.

Для указанных выше параметров можно настроить определенные логотипы для разных языков документации.

{% cut "Примеры" %}

Один логотип для всех языков:

```text
src: logo
```
Отличающиеся логотипы для разных языков:

```text
src:
  ru: logo1
  en: logo2
  default: logo3
```

В этом примере при переходах по ссылкам с указанием языкового каталога будут отображаться `logo1` и `logo2` для языков `ru` и `en` соответственно. Если языковой каталог не указан, отобразится logo3.

Примеры ссылок и отображаемых логотипов:

- https://diplodoc.com/docs/ru — `logo1`
- https://diplodoc.com/docs/en — `logo2`
- https://diplodoc.com/docs — `logo3`

{% endcut %}

|  ||
|| `metrika` | Номер счетчика [Яндекс Метрики](https://metrika.yandex.ru/).

Можно подключить несколько счетчиков:

```yaml
docs-viewer:
  metrika: [21930706, 96924079, 96924106]
```
| `string \| string[]` | `undefined` ||
|| `no-index` | Запрет на индексирование внешними роботами.

Рекомендуется использовать до публичных запусков, чтобы документ не отображался в поисковиках. |  `bool` | `false` ||
|| `project-name` | Формирует URL-адрес проекта. Требования:

- только нижний регистр;
- только латиница, цифры, дефис и нижнее подчеркивание;
- максимальная длина — 63 символа.

{% note warning %}

1. Чтобы проверить уникальность вашего `project-name`, воспользуйтесь поиском по вхождению `project-name: <project-name>` в репозитории с установленным флагом **Ignore case**.

2. Есть три зарезервированных имени, которые нельзя указывать в качестве значения `project-name`:

    * `build`;
    * `docs-assets`;
    * `api`.

3. Для проектов на доменах dev/support2 значение `project-name` должно начинаться с префикса `dev-`/`support-`.

    Например, `project-name: support-project-name`.

{% endnote %}
| `string` | ||
|| `sanitizeOptions` | Объект настроек, который определяет, какие HTML-теги, атрибуты, стили и другие элементы будут разрешены или запрещены при очистке HTML-контента. | `Object` | `undefined` ||
|| `supportGithubAnchors` | Генерировать дополнительные [якоря](syntax/base.md#headers), совместимые с GitHub. | `bool` | `false` ||
|| `support-widget` | Виджет Яндекс Мессенджера с чатом поддержки. |  | ||
|| `themes` | Выбор темы оформления: светлая или темная. По умолчанию доступны обе. Можно отключить одну из них, указав используемую по умолчанию, например:

```yaml
themes: ['light']
```

| `string` | `light` ||
|# {wide-content}


## Ресурсы {#resources}

#|
|| **Название** | **Описание** | **Тип** | **Значение по умолчанию** ||
||
`allow-custom-resources`

`static-content`

`resources <value...>`
| Разрешить загрузку ресурсов в статически сгенерированные страницы. | `bool` | `false` ||
|| `csp` | Управление [Content Security Policy](./guides/csp.md) (CSP). | `string` | - ||
|#
