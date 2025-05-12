# Настройки YFM-проекта

В зависимости от используемого инструмента вы можете задать стандартные настройки YFM-проекта одним из способов:
* в [файле конфигурации](./project/config.md);
* в качестве параметра функции ([Transformer](./tools/transform/settings.md));
* через ключи запуска ([Builder](./tools/docs/settings.md)).

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

- docs.yandex-team.ru

  ```
  docs-viewer:
    project-name: <project-name>
  ```

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
|| `allowHTML` | Разрешить [использование html-элементов](syntax/base.md#html) в разметке. | `bool` | `false` ||
|| `strict` | Cтрогий режим сборки, все предупреждения YFM отображаются как ошибки. | `bool` | `false` ||
|| `breaks` | [Переносить строки](syntax/base.md#breaks) по символу перевода каретки. | `bool` | `true` ||
|| `singlePage` | Собирать [одностраничную сборку](tools/docs/singlepage.md) из всех файлов проекта. | `bool` | `false` ||
|| `pdf` | В случае, если указано значение `pdf: true`, для документа будет собираться pdf-версия. Чтобы сборка прошла корректно обязательно должен быть указан параметр `singlePage: true`. После завершения сборки в левом нижнем углу документа отображается значок собранного PDF-файла, который можно скачать.| `bool` | `false` ||
|| `apply-presets` | Применять ли пресеты переменных. 

[Подробнее о пресетах](project/presets.md). | `bool` | `false` ||
|| `varsPreset` | Имя пресета переменных, который необходимо использовать при сборке. | `string` | ||
|| `needToSanitizeHtml` | Параметр предназначен для очистки и фильтрации HTML-контента. Связанный параметр [sanitizeOptions](#sanitizeOptions) позволяет определить, какие HTML-теги, атрибуты, стили и другие элементы будут разрешены или запрещены в процессе очистки HTML-контента. | `bool` | `false` ||
|| `add-system-meta` | Добавлять метаданные с системными переменными из пресетов в файлы документации.
В файле presets.yaml можно задать секцию `system`, содержимое которой будет добавлено в meta-данные каждой страницы.
Отображается при генерации файлов в формате md.
 | `bool` | `false` ||
|| `remove-hidden-toc-items` | Убрать из оглавления все объекты, отмеченные атрибутом `hidden: true`. | `bool` | `false` ||
|| `add-map-file` | Создает json-файл со всеми путями проекта | `bool` | `false` ||
|| `lint` | Подключить [файл линтера](./project/lint.md). | `bool` | `false` ||
|| `conditionsInCode` | Параметр используется для возможности создания блоков кода с условиями. Выполнение таких условий осуществляется с помощью [условных операторов](syntax/vars#conditions). | `bool` | `false` ||
|| `output-format` | Формат файлов итоговой сборки | `string` (`html` или `md`) | `html` ||
|| `merge-includes` | Параметр, который отвечает за корректную обработку включений [инклюдов](./project/includes.md) при сборке документов в формате `md`. Позволяет объединять содержимое инклюдов в единый документ.

{% note warning %}

Работает только вместе с параметром `output-format: md`.

{% endnote %} 

| `bool` | `false` ||
|| `langs` | Массив языков, участвующих в сборке. | ||
|# {wide-content}

## Параметры отображения в интерфейсе {#docs-viewer}

#|
|| **Название** | **Описание** | **Тип** | **Значение по умолчанию** ||
|| `project-name` | Формирует URL-адрес проекта. Требования:

- только нижний регистр;
- только буквы, цифры, дефис и нижнее подчеркивание;
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
|| `is-external` /  `is-new-external` |
Проект будет доступен внешним пользователям, если установлено значение параметра `true`.

Параметр `is-external` используется для проектов на yandex.ru/dev или yandex.ru/legal. Для проектов на yandex.ru/support2 используется параметр `is-new-external`.

{% note warning %}

Параметр `is-external`, используемый для выкладки внешней документации на yandex.ru/support2 и собственные домены, устарел. Для проектов с этим параметром необходима [миграция](../migrations/new-ci.md).

Для новых проектов используйте параметр `is-new-external`.

{% endnote %}

| `bool` | `true` ||
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

`string` | ||
|| `themes` | Выбор темы оформления: светлая или темная. По умолчанию доступны обе. Можно отключить одну из них, указав используемую по умолчанию, например:

```yaml
themes: ['light']
```

| `string` | `light` ||
|| `no-index` | Запрет на индексирование внешними роботами.

Рекомендуется использовать до публичных запусков, чтобы документ не отображался в поисковиках. |  `bool` | `false` ||
|| `favicon-src` | Иконка во вкладке браузера.

Можно использовать любую ссылку на изображение, подходящее под стандартные требования к фавиконкам. |  |  ||
|| `logo-options` |
Настройки логотипа:

* `src` — ссылка на изображение для светлой темы;

* `src-dark` — ссылка на изображение для темной темы;

* `src-mobile` — ссылка на изображение для светлой темы на мобильных;

* `src-mobile-dark` — ссылка на изображение для темной темы на мобильных;

* `src-preview` — логотип для превью ссылки при шеринге на внешних ресурсах;

* `url` — ссылка, на которую перенаправляет при нажатии на логотип. Можно задать шаблон ссылки с параметром `{lang}`, чтобы он заменился на текущий язык документации при переходе. Например, ссылка `https://diplodoc.com/docs/{lang}/` при переходе из русской документации будет вести на `https://diplodoc.com/docs/ru/`.

* `title` — текст, который показывается вместо логотипа, если он не задан. 

Если логотипы для темной темы не указаны, то при сборке для нее используется логотип для светлой темы.

Для указанных выше параметров можно настроить различное отображение для разных языков собираемой документации.

{% cut "Примеры" %}

Для всех языков документации будет использован один и то же логотип:

```text
src: logo
```
Для разных языков документации будут использованы разные логотипы:

```text
src:
  ru: logo1
  en: logo2
  default: logo3
```
{% endcut %}

* `title` — текст, который можно задать вместо логотипа; |  |  ||
|| `support-widget` | Виджет Яндекс Мессенджера с чатом поддержки. |  |  ||
|| `github-url-prefix` | Github префикс до директории корня документации (если она хранится на Github).

Если значение не задано, то для внешних пользователей не будет указана ссылка на редактирование страницы. | | ||
|| `disableLiquid` | Отключить использование переменных. | `bool` | `false` ||
|| `supportGithubAnchors` | Генерировать дополнительные [якоря](./syntax/base.md#headers), совместимые с GitHub. | `bool` | `false` ||
|| `linkify` | Преобразовывать ссылкоподобные строки в ссылки.  | `bool` | `false` ||
|| `linkifyTlds` | Настройка tld для плагина linkify. | `string \| string[]` | `undefined` ||
|| `lang` | Язык локализации дефолтных текстов. 
Для [следующих языков](https://github.com/diplodoc-platform/client/blob/34a5139620874627cfdebe9be74902cf9d3961b1/src/constants.ts#L15) контент будет отображаться в формате RTL (right-to-left) | `string` | `ru` ||
|| `metrika` | Использовать счётчик Яндекс.Метрики с заданным id.

Можно подключить несколько счетчиков:

```yaml
docs-viewer:
  metrika: [21930706, 96924079, 96924106]
```
| `string \| string[]` | `undefined` ||
|| `sanitizeOptions` | Объект настроек, который определяет, какие HTML-теги, атрибуты, стили и другие элементы будут разрешены или запрещены при очистке HTML-контента. | `Object` | `undefined` || {#sanitizeOptions}
|| `analytics` | Конфигурация для модуля аналитки. | `Object` | `undefined`  ||
|| `analytics.gtm` | Настройки Google Tag Manager аналитики. | `Object` | `undefined` ||
|| `analytics.gtm.id` | Идентификатор Google Tag Manager в формате GTM. | `string` | `undefined` ||
|| `analytics.gtm.mode` | Тип уведомления перед отправкой событий `base` или `notification`. | `string` | `base` ||
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
