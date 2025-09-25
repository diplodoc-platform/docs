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

## Параметры {#parameters}

### Корневая секция {#root-settings}

#|
|| **Параметр** | **Описание** | **Тип и значение по умолчанию** ||
|| `allowCustomResources` | Разрешить загрузки пользовательских ресурсов в статически сгенерированные страницы. | `bool`

`false` ||
|| `allowHtml` | Разрешить [использование html-элементов](syntax/base.md#html) в разметке. | `bool`

`false` ||
|| `applyPresets` | Применять ли пресеты переменных.
[Подробнее о пресетах](project/presets.md). | `bool`

`false` ||
|| `authors` | Включить отображение автора статьи.

Работает при включенном параметре `vcs`. | `bool` или `object`

`false`
Параметры объекта:
`enabled` - `bool` - 
Включить отображение автора статьи.
`ignore` - `string[]` - 
Игнорировать авторов по паттернам перечисленным в списке.

Пример:

```
authors:
  enabled: true
  ignore:
    - robot-*
    - noreply@company.com
```
||
|| `breaks` | [Переносить строки](syntax/base.md#breaks) по символу перевода каретки. | `bool`

`true` ||
|| `contributors` | Включить отображение контрибьюторов в статье.

Работает при включенном параметре `vcs`.


| `bool` или `object`

`false`
Параметры объекта:
`enabled` - `bool` - 
Включить отображение автора статьи.
`ignore` - `string[]` - 
Игнорировать авторов по паттернам перечисленным в списке.

Пример:

```
authors:
  enabled: true
  ignore:
    - robot-*
    - noreply@company.com
```
||
|| `langs` | Массив языков, участвующих в сборке. | —

— ||
|| `linkify` | Преобразовывать ссылкоподобные строки в ссылки.
Пример ссылки: _https://diplodoc.com/ru_ или _diplodoc.com/ru_. | `bool`

`false` ||
|| `lint` | Подключить [файл линтера](./project/lint.md). | `bool`

`false` ||
|| `mtimes` | Включить отображение даты изменения статьи.

Работает при включенном параметре `vcs`. | `bool`

`false` ||
|| `outputFormat` | Формат файлов итоговой сборки. | `string` (`html` или `md`)

`html` ||
|| `pdf` | При значении `pdf: true` для документа будет собираться pdf-версия. Чтобы сборка прошла корректно, обязательно должен быть указан параметр `singlePage: true`. После завершения сборки в левом нижнем углу документа отображается значок собранного PDF-файла, который можно скачать.

{% note warning %}

Параметр поддерживается **только в серверной версии**. Для генерации pdf-версии документации локально необходимо использовать сервис `@diplodoc/pdf-generator` согласно [инструкции](https://github.com/diplodoc-platform/pdf-generator).

{% endnote %}

| `bool`

`false` ||
|| `removeHiddenTocItems` | Убрать из оглавления все объекты, отмеченные атрибутом `hidden: true`. | `bool`

`false` ||
|| `sanitizeHtml` | Включает очистку HTML-разметки от потенциально опасных элементов в `.md`-файлах с помощью HTML-санитайзера. Определяет разрешенные и запрещенные теги, атрибуты, стили и другие элементы при очистке HTML-контента. | `bool`

`true` ||
||
`singlePage`
|
Собирать [одностраничную сборку](tools/docs/singlepage.md). Будет создан файл `single-page.html`, который объединит содержимое всех файлов проекта. 

{% include [single-page-ex](./_includes/settings-single-page-ex.md) %}
|
`bool`

`false`
||
|| `staticContent` | Разрешить использовать статический контент (например, файлов изображений, CSS или JS). | `bool`

`false` ||
|| `strict` | Cтрогий режим сборки, все предупреждения YFM отображаются как ошибки. | `bool`

`false` ||
|| `supportGithubAnchors` | Генерировать дополнительные [якоря](syntax/base.md#headers), совместимые с GitHub. | `bool`

`false` ||
|| `varsPreset` | Имя пресета переменных, который необходимо использовать при сборке. | `string`

— ||
|| `vcs` | Настройка подключения к vcs системе.

Её включение позволяет включать фичи `mtimes`, `authors` и `contributors`. | `boolean` или `object`

`undefined` ||
|| [analytics](#analytics) | Конфигурация для модуля аналитки. | `Object`

`undefined` ||
|| [resources](#resources) | Список разрешенных ресурсов. | `Object`

`undefined` ||
|| [template](#template) | Конфигурация синтаксиса шаблонизации. | `Object`

`undefined` ||
|#

### Секция template {#template}

#|
|| **Параметр** | **Описание** | **Тип и значение по умолчанию** ||
|| `enabled` | Включает обработку синтаксиса шаблонов в документации. Если не указан, шаблонизация считается включенной. | `bool`

`true` ||
|| `scopes` | > | > ||
|| `scopes.code` | Включает обработку синтаксиса [условных операторов](syntax/vars#conditions) в блоках кода. | `bool`

`false` ||
|| `scopes.text` | Включает обработку синтаксиса [условных операторов](syntax/vars#conditions) в тексте документа. | `bool`

`true` ||
|| `features` | > | > ||
|| `features.cicles` | Включает обработку синтаксиса [циклов](syntax/vars#cycles). | `bool`

`true` ||
|| `features.conditions` | Включает обработку синтаксиса [условных операторов](syntax/vars#conditions). | `bool`

`true` ||
|| `features.substitutions` | Включает обработку синтаксиса [переменных](syntax/vars#substitutions). | `bool`

`true` ||
|#

### Секция analytics {#analytics}

#|
|| **Название** | **Описание** | **Тип и значение по умолчанию** ||
|| `gtm` | Настройки аналитики Google Tag Manager. | `Object`

`undefined` ||
|| `gtm.id` | Идентификатор Google Tag Manager в формате GTM. | `string`

`undefined` ||
|| `gtm.mode` | Тип уведомления перед отправкой событий `base` или `notification`. | `string`

`base` ||
|#

### Секция `interface` {#interface}

#|
|| **Название** | **Описание** | **Тип и значение по умолчанию** ||
|| `favicon-src` | Иконка во вкладке браузера.
Можно использовать любую ссылку на изображение, подходящее под стандартные требования к фавиконкам. | `string`

— ||
|| `toc` | Скрывает оглавление (Table of contents, ToC). Если не указан, ToC считается включенным. | `bool`

`true` ||
|| `toc-header` | Скрывает заголовок в ToC. Если не указан, заголовок считается включенным. | `bool`

`true` ||
|| `feedback` | Скрывает фидбэк в конце страницы. Если не указан, фидбэк включенным. | `bool`

`true` ||
|| `search` | Скрывает поиск. Если не указан, поиск считается включенным. | `bool`

`true` ||

|#

### Секция `resources` {#resources}

#|
|| **Название** | **Описание** | **Тип и значение по умолчанию** ||
|| `script` | Добавление пользовательских скриптов на страницу. | —

— ||
|| `style` | Добавление пользовательских стилей на страницу. | —

— ||
|| `csp` | Управление [Content Security Policy](./guides/csp.md) (CSP).

{% cut "Пример структуры" %}

```yaml
csp:
	- "script-src":
    	- "self"
        - "domain1.com"
        - "domain2.com"
        "*.domain3.com"
    - "style-src":
    	- "self"
    ...
    ...
    ...
    
```
Данная конфигурация преобразуется в HTML-тег вида:

```html
<meta http-equiv="content-security-policy" content="script-src 'self' domain1.com domain2.com *.domain3.com; style-src 'self' ... ... ...">
```

Ключи объекта соответствуют поддерживаемым директивам CSP. Система не проверяет корректность указанных значений — они берутся из `.yfm`-файла и автоматически включаются в мета-тег.

{% endcut %}

| `object`

— ||
|#

### Секция `docs-viewer` {#docs-viewer}

#|
|| **Название** | **Описание** | **Тип и значение по умолчанию** ||
|| `favicon-src` | Иконка во вкладке браузера.
Можно использовать любую ссылку на изображение, подходящее под стандартные требования к фавиконкам. | `string`

— ||
|| `lang` | Язык по умолчанию для локализации.
Для [следующих языков](https://github.com/diplodoc-platform/client/blob/34a5139620874627cfdebe9be74902cf9d3961b1/src/constants.ts#L15) контент будет отображаться в формате RTL (right-to-left). | `string`

`ru` ||
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

{% cut "Полный список поддерживаемых языков" %}

#|
|| **Код языка (ISO 639-1)** | **Язык** ||
|| `am` | Амхарский  ||
|| `ar` | Арабский   ||
|| `az` | Азербайджанский ||
|| `be` | Белорусский ||
|| `bg` | Болгарский ||
|| `el` | Греческий  ||
|| `en` | Английский ||
|| `es` | Испанский  ||
|| `et` | Эстонский  ||
|| `fi` | Финский    ||
|| `fr` | Французский ||
|| `he` | Иврит      ||
|| `hu` | Венгерский ||
|| `hy` | Армянский  ||
|| `ka` | Грузинский ||
|| `kk` | Казахский  ||
|| `km` | Кхмер      ||
|| `ky` | Киргизский ||
|| `lt` | Литовский  ||
|| `lv` | Латышский / Латвийский ||
|| `ne` | Непальский ||
|| `no` | Норвежский ||
|| `pl` | Польский   ||
|| `pt` | Португальский  ||
|| `ro` | Румынский / Молдавский ||
|| `ru` | Русский    ||
|| `sr` | Сербский   ||
|| `tg` | Таджикский ||
|| `tr` | Турецкий   ||
|| `uk` | Украинский ||
|| `ur` | Урду       ||
|| `uz` | Узбекский  ||
|| `vi` | Вьетнамский ||
|| `zh` | Китайский  ||
|#

{% endcut %}


{% note warning %}

Языки, не включенные в список, отображаться не будут.

Если структура проекта содержит языковые папки, то указывать параметр обязательно, даже если в проекте используется только один язык.

{% endnote %} 

| `string[]`

— ||
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

| —

— ||
|| `metrika` | Номер счетчика [Яндекс Метрики](https://metrika.yandex.ru/).

Можно подключить несколько счетчиков:

```yaml
docs-viewer:
  metrika: [21930706, 96924079]
```
| `string` \| `string[]`

`undefined` ||
|| `no-index` | Запрет на индексирование внешними роботами.

Рекомендуется использовать до публичных запусков, чтобы документ не отображался в поисковиках. |  `bool`

`false` ||
|| `project-name` | Формирует URL-адрес проекта. Требования:

- только нижний регистр;
- только латиница, цифры, дефис и нижнее подчеркивание;
- максимальная длина — 63 символа.

{% note warning %}

Есть три зарезервированных имени, которые нельзя указывать в качестве значения `project-name`:

- `build`;
- `docs-assets`;
- `api`.

{% endnote %}
| `string`

— ||
|| `themes` | Выбор темы оформления: светлая или темная. По умолчанию доступны обе. Можно отключить одну из них, указав используемую по умолчанию, например:

```yaml
themes: ['dark']
```

{% note warning %}

Параметр поддерживается **только в серверной версии**.

{% endnote %}

| `string[]`
`['light', 'dark']` ||
|#

### Секция `search` {#search}

Чтобы добавить поиск в документацию, явно пропишите секцию `search` в файле `.yfm`.  
Diplodoc поддерживает в режиме статической сборки документации два типа интеграции поиска:

- [локальный поиск на клиенте (на базе Lunr.js)](./project/lunr.md);
- [облачный поиск на базе платформы Algolia](./project/algolia.md).

По умолчанию поиск **отключен**, для его появления настройте секцию `search`.

#### Общие параметры {#search-common}

#|
|| **Название** | **Описание** | **Тип и значение по умолчанию** ||
|| `provider` | Выбор поисковой системы.
Варианты:
- `local` — локальный поиск (Lunr.js);
- `algolia` — облачный поиск на базе Algolia. | `string`

— (поиск не подключен) ||
|#

#### Параметры для локального поиска (`provider: local`) {#search-local}

#|
|| **Название** | **Описание** | **Тип и значение по умолчанию** ||
|| `tolerance`  | Глубина расширения совпадений:
- 0 — только полное совпадение слова;
- 1 — совпадение по префиксу (`word*`);
- 2 — совпадение по любой подстроке слова (`*word*`). | `number`

`2` ||
|| `confidense` | Режим ранжирования результатов:
- `phrased` — выше ранжируются результаты по длине найденной фразы;
- `sparsed` — выше ранжируются результаты по количеству найденных слов. | `string`

`phrased` ||
|#

#### Параметры для поиска через Algolia (`provider: algolia`) {#search-algolia}

#|
|| **Название** | **Описание** | **Тип и значение по умолчанию** ||
|| `appId` | Algolia App ID.
Обязательный параметр для облачного поиска. | `string`

— ||
|| `apiKey` | **Секретный** Admin API Key для индексации.
Рекомендуется передавать через переменные среды или CLI. | `string`

— ||
|| `indexName` | Имя индекса в Algolia. | `string`

`docs` ||
|| `index` | Если `true`, индекс будет автоматически загружаться в Algolia после сборки.
Если `false`, только создается локальный индекс. | `bool`

`false` ||
|| `searchApiKey`  | Search API Key.
Клиентский ключ для поиска на фронте. Без него облачный поиск не работает на клиенте. | `string`

`search-api-key` ||
|| `api` | Путь к js-API поиска на клиенте. | `string`

`_search/api.js` ||
|| `indexSettings` | [Настройки индекса Algolia](https://www.algolia.com/doc/api-reference/settings-api-parameters/). | `object`

— ||
|| `querySettings` | [Настройки параметров поиска Algolia](https://www.algolia.com/doc/api-reference/api-parameters/). | `object`

— ||
|#

#### Примеры настройки поиска

**Локальный поиск:**

```yaml
search:
  provider: local
  tolerance: 2
  confidense: phrased
```

**Поиск через Algolia:**

```yaml
search:
  provider: algolia
  appId: <ВАШ_APP_ID>
  indexName: docs
  index: true
  searchApiKey: <ВАШ_SEARCH_API_KEY>
  indexSettings:
    searchableAttributes:
      - title
      - content
      - headings
  querySettings:
    hitsPerPage: 10
    attributesToRetrieve:
      - title
      - content
      - url
```

{% note info %}

- Для активации поиска обязательно добавьте секцию `search` и укажите `provider`.
- Для больших проектов рекомендуется облачный поиск Algolia.
- Не публикуйте `apiKey` от Algolia в публичных репозиториях или продакшн-конфигурациях — используйте переменные среды либо CLI-параметры.

{% endnote %}

## Пример файла `.yfm `{#yfm}

```yaml
# Корневая секция параметров
strict: true
breaks: false
singlePage: true
apply-presets: true
varsPreset: 'external'
needToSanitizeHtml: true
langs: ['en', 'ru']

# Секция параметров вьюера (docs-viewer)
docs-viewer:
  project-name: project-name
  no-index: true
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

# Секция ресурсов
resources:
  csp:
    - "frame-src":
        - "https://test.site"

```
