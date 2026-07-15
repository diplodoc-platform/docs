# Настройки YFM-проекта

В зависимости от используемого инструмента вы можете задать стандартные настройки YFM-проекта одним из способов:

* в [файле конфигурации](#config);
* через [ключи запуска команды](./tools/docs/settings.md) `yfm`.

## Файл конфигурации {#config}

По умолчанию используется файл `.yfm` в корне документа. При сборке можно указать путь до другого файла с помощью [ключа запуска](tools/docs/settings.md) `--config`.

Файл конфигурации содержит список всех параметров в формате YAML:

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
|| `allowCustomResources` {#allow-custom-resources} | Разрешить загрузки пользовательских ресурсов в статически сгенерированные страницы. | `boolean`

`false` ||
|| `allowHtml` | Разрешить [использование html-элементов](syntax/base.md#html) в разметке. | `boolean`

`false` ||
|| `applyPresets` | Применять ли пресеты переменных.
[Подробнее о пресетах](project/presets.md). | `boolean`

`false` ||
|| `authors` {#vcs-authors} | Включить отображение автора статьи.

Пример:

```yaml
authors:
  enabled: true
  ignore:
    - robot-*
    - noreply@company.com
```

Параметры:
- `enabled` — `boolean` — включить отображение автора статьи,
- `ignore` — `string[]` — игнорировать авторов по паттернам, перечисленным в списке.

Значение `authors: true` аналогично `authors: enabled: true`.

Работает при **включенном** параметре [##vcs##](#vcs). | `boolean` \| `object`

`false`

||
|| `breaks` | [Переносить строки](syntax/base.md#breaks) по символу перевода каретки. | `boolean`

`true` ||
|| `contributors` {#vcs-contributors} | Включить отображение контрибьюторов в статье.

Пример:

```yaml
authors:
  enabled: true
  ignore:
    - robot-*
    - noreply@company.com
```

Параметры:
- `enabled` — `boolean` — включить отображение контрибьюторов в статье,
- `ignore` — `string[]` — игнорировать контрибьюторов по паттернам, перечисленным в списке.

Значение `contributors: true` аналогично `contributors: enabled: true`.

Работает при **включенном** параметре [##vcs##](#vcs).

| `boolean` \| `object`

`false`

||
|| `disableCsp` {#disable-csp} | Отключить добавление мета-тега [Content-Security-Policy](./guides/csp.md#disable-csp) в сгенерированные HTML-страницы.

Используйте, когда CSP управляется внешним образом (например, через HTTP-заголовки сервера).| `boolean`

`false` ||
|| `extensions` {#extensions} | Список [расширений Diplodoc](extensions/index.md), используемых для сборки проекта.

Объекты в списке должны содержать параметр `name` с названием расширения, а также параметры работы, уникальные для каждого расширения.

```yaml
extensions:
  - name: my-extension
    option1: true
    option2: true
    ...
```

Строками в списке можно в упрощенном формате задавать названия расширений:

```yaml
extensions:
  - algolia
  - some-author/my-extension
  - /my-local-extension
```

| `(string\|object)[]`

— ||
|| `langs` | Массив языков, участвующих в сборке. | —

— ||
|| `linkify` | Преобразовывать ссылкоподобные строки в ссылки.

Примеры строк:
- _https://diplodoc.com/ru_
- _diplodoc.com/ru_
| `boolean`

`false` ||
|| `lint` | Подключить [файл линтера](./project/lint.md). | `boolean`

`false` ||
|| `llms` {#llms} |

Настройки генерации [файлов llms.txt и llms-full.txt](./guides/llms.md) для проекта:

```yaml wrap
llms:
  enabled: true
  description: описание проекта
```

Значение опционального поля `description` добавляется в начало файлов ##llms*.txt##.

| `object`

— ||
|| `mtimes` {#vcs-mtimes} | Включить отображение даты изменения статьи, которая берётся из данных VCS.

Работает при включенном параметре [##vcs##](#vcs).

Также, дата изменения автоматически добавляется в метаданные страницы ##last-modified## и ##article:modified_time##.

| `boolean`

`false` ||
|| `outputFormat` | Формат файлов итоговой сборки: `html` или `md`. | `string`

`html` ||
|| `removeHiddenTocItems` | Убрать из сборки все файлы, отмеченные в `toc.yaml` атрибутом `hidden: true`. | `boolean`

`false` ||
|| `sanitizeHtml` | Включает очистку HTML-разметки от потенциально опасных элементов в `.md`-файлах с помощью HTML-санитайзера. Определяет разрешенные и запрещенные теги, атрибуты, стили и другие элементы при очистке HTML-контента. | `boolean`

`true` ||
||
`singlePage`
|
Собирать [одностраничную сборку](tools/docs/singlepage.md). Будет создан файл `single-page.html`, который объединит содержимое всех файлов проекта. 

{% include [single-page-ex](./_includes/settings-single-page-ex.md) %}
|
`boolean`

`false`
||
|| `staticContent` | Собирать html-контент статьи как часть вёрстки. По умолчанию, он находится в js-объекте и вставляется в страницу на этапе отрисовки в браузере. | `boolean`

`false` ||
|| `strict` | Строгий режим сборки, все предупреждения YFM отображаются как ошибки.

С полным списком правил YFM можно ознакомиться [здесь](./project/lint.md).
| `boolean`

`false` ||
|| `supportGithubAnchors` | Генерировать дополнительные [якоря](syntax/base.md#headers), совместимые с GitHub. | `boolean`

`false` ||
|| `theme` | Настройка для базового цвета в темизаторе. Переопределяет base-brand в основной секции конфигурационного файла theme.yaml. [Подробнее о темизаторе](style/theme.md). | По умолчанию базовый цвет не меняется.

||
|| `varsPreset` | Имя пресета переменных, который необходимо использовать при сборке. | `string`

— ||
|| `vcs` {#vcs} | Настройка подключения к vcs системе. Её включение позволяет использовать функциональности [##mtimes##](#vcs-mtimes), [##authors##](#vcs-authors) и [##contributors##](#vcs-contributors).

Требует [подключения встроенного расширения](#extensions) `github-vcs`.

| `boolean` \| `object`

`false` ||
|#

### Секция `analytics` {#analytics}

#|
|| **Название** | **Описание** | **Тип и значение по умолчанию** ||
|| `gtm` | Настройки аналитики Google Tag Manager.

Параметры:
- `id` — `string` — идентификатор Google Tag Manager в формате GTM,
- `mode` — `string` — тип уведомления перед отправкой событий `base` (по умолчанию) или `notification`.

| `object`

— ||
|| `metrika` {#analytics-metrika} |

Подключение счётчиков [Яндекс Метрики](https://metrika.yandex.ru/).

Каждый элемент списка — объект с обязательным полем `id` (номер счётчика) и опциональным полем `params` для передачи [параметров инициализации счётчика](https://yandex.ru/support/metrica/ru/code/counter-initialize#parametry-inicializacii-schetchika).

Минимальная конфигурация:
```yaml
analytics:
  metrika:
    - id: 123456
```

{% cut "Пример с несколькими счётчиками" %}

```yaml
analytics:
  metrika:
    - id: 123456
      params:
        clickmap: true
    - id: 456789
      params:
        clickmap: true
        webvisor: true
```

{% endcut %}

В подключенные счётчики из интерфейса документации [отправляются цели](./project/analytics/ym.md).

| `object[]`

—
||
|#

### Секция `content` {#content}

Управление обработкой и проверками контента статей.

#|
|| **Название** | **Описание** | **Тип и значение по умолчанию** ||
|| `maxAssetSize` | Максимально допустимый размер ассета в проекте. В случае превышения сборка завершится с ошибкой.

Принимает числа и строки: ##1024##, ##512K##, ##8M##.
 
Если указать ##0##, то проверка размера ассетов выполняться не будет. |  `number` \| `string`

`64M` ||
|| `maxHtmlSize` | Максимально допустимый размер html-контента статьи после сборки. В случае превышения сборка завершится с ошибкой.

Принимает числа и строки: ##1024##, ##512K##, ##8M##.
 
Максимальное значение — ##96M##. |  `number` \| `string`

`42M` ||
|| `maxInlineSvgSize` | Максимально допустимый размер svg-изображения, при котором оно [инлайнится в контент статьи](./syntax/media.md#img-inline) автоматически. В случае превышения размера svg-изображение вставляется через тег ##\<img\>##.

Принимает числа и строки: ##1024##, ##512K##, ##2M##.
 
Если указать ##0##, то svg-изображения не будут инлайниться при сборке.

Максимальное значение — ##16M##. |  `number` \| `string`

`2M` ||
|| `maxOpenapiIncludeSize` {#max-openapi-include-size} | Максимально допустимый размер json-схемы в тексте оглавления собранной [OpenAPI-спецификации](./guides/openapi.md#leadingpage). В случае превышения размера, json-схема не добавляется на страницу напрямую, а вставляется ссылкой для загрузки (режим `link`).

Принимает числа и строки вида: ##1024##, ##512K##, ##2M##.
 
Если указать ##0##, режим вставки json-схем `inline` всегда заменяется на `link`. |  `number` \| `string`

`100K` ||
|| `multilineTermDefinitions` |

Могут ли всплывающие подсказки содержать контент с множественными переносами строк:

* ##true## — подсказки могут содержать контент с множественными переносами строк.

* ##false## — подсказки могут содержать только одиночные переносы строк, все определения терминов должны располагаться в конце файла (при нарушении этого условия сборка завершится с [ошибкой `YFM009`](./project/lint.md)).

|  `boolean`

`true` ||
|#

### Секция `interface` {#interface}

Настройки отображения интерфейса. Все настройки из секции можно переопределять для отдельных статей, указывая их значения в [метаданных](./project/meta.md#interface) страниц.

#|
|| **Название** | **Описание** | **Тип и значение по умолчанию** ||
|| `favicon-src` | Иконка во вкладке браузера.
Можно использовать любую ссылку на изображение, подходящее под стандартные требования к фавиконкам. | `string`

— ||
|| `toc` | Скрывает оглавление (Table of contents, ToC). Если не указан, ToC считается включенным. | `boolean`

`true` ||
|| `toc-header` {#toc-header} | Скрывает заголовок в ToC. Если не указан, заголовок считается включенным. | `boolean`

`true` ||
|| `feedback` | Скрывает фидбэк в конце страницы. Если не указан, фидбэк включенным. | `boolean`

`true` ||
|| `search` | Скрывает поиск. Если не указан, поиск считается включенным. | `boolean`

`true` ||

|#

### Секция `pdf` {#pdf}

Содержит параметры предобработки данных для [генерации pdf-версии](guides/generate-pdf.md) документации.

#|
|| **Название** | **Описание** | **Тип и значение по умолчанию** ||
|| `enabled` | Включить предобработку данных для сервиса `@diplodoc/pdf-generator`. | `boolean`

`false` ||
|| `hiddenPolicy` | При значении ##true## скрытые параметром `hidden` страницы будут убраны из pdf-версии документации.

При значении ##false## скрытые страницы будут отображаться в pdf-версии документации. | `boolean`

`true` ||
|#

### Секция `resources` {#resources}

Управление подключаемыми к проекту ресурсами.

#|
|| **Название** | **Описание** | **Тип и значение по умолчанию** ||

|| `csp` {#resources-csp} | Управление [Content Security Policy](./guides/csp.md) (CSP).

{% cut "Пример структуры" %}

```yaml
resources:
  csp:
    - "script-src":
        - "self"
        - "domain1.com"
        - "domain2.com"
        "*.domain3.com"
    - "style-src":
    	- "self"
```
Данная конфигурация преобразуется в HTML-тег вида:

```html
<meta http-equiv="content-security-policy" content="script-src 'self' domain1.com domain2.com *.domain3.com; style-src 'self'">
```

Ключи объекта соответствуют поддерживаемым директивам CSP. Система не проверяет корректность указанных значений — они берутся из `.yfm`-файла и автоматически включаются в мета-тег.

{% endcut %}

| `object`

— ||
|| `script` | Список подключаемых ко всем страницам проекта javascript-файлов.

```yaml
resources:
  script:
    - _assets/scripts/custom.js
    - _assets/scripts/some.js
```

Для подключения скриптов должен быть установлен параметр ##[allowCustomResources](#allow-custom-resources): true##.

| `string[]`

— ||
|| `style` | Список подключаемых ко всем страницам проекта css-файлов.

```yaml
resources:
  style:
    - _assets/style/custom.css
    - _assets/style/my.css
```

Для подключения стилей должен быть установлен параметр ##[allowCustomResources](#allow-custom-resources): true##.

| `string[]`

— ||
|#

### Секция `template` {#template}

Управление поддерживаемыми конструкциями [синтаксиса шаблонов](./syntax/vars.md).

#|
|| **Параметр** | **Описание** | **Тип и значение по умолчанию** ||
|| `enabled` | Включает обработку синтаксиса шаблонов в документации. Если не указан, шаблонизация считается включенной. | `boolean`

`true` ||
|| `scopes` | > | > ||
|| `scopes.code` | Включает обработку синтаксиса [условных операторов](syntax/vars#conditions) в блоках кода. | `boolean`

`false` ||
|| `scopes.text` | Включает обработку синтаксиса [условных операторов](syntax/vars#conditions) в тексте документа. | `boolean`

`true` ||
|| `features` | > | > ||
|| `features.cicles` | Включает обработку синтаксиса [циклов](syntax/vars#cycles). | `boolean`

`true` ||
|| `features.conditions` | Включает обработку синтаксиса [условных операторов](syntax/vars#conditions). | `boolean`

`true` ||
|| `features.substitutions` | Включает обработку синтаксиса [переменных](syntax/vars#substitutions). | `boolean`

`true` ||
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
|| `no-index` | Запрет на индексирование внешними роботами.

Рекомендуется использовать до публичных запусков, чтобы документ не отображался в поисковиках. |  `boolean`

`false` ||
|| `project-name` | Формирует URL-адрес проекта. Требования:

- только нижний регистр;
- только латиница, цифры, дефис и нижнее подчеркивание;
- максимальная длина — 63 символа.

{% note warning %}

Есть три зарезервированных имени, которые нельзя указывать в качестве значения `project-name`:

* `build`;
* `docs-assets`;
* `api`.

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

* [локальный поиск на клиенте (на базе Lunr.js)](./project/lunr.md);
* [облачный поиск на базе платформы Algolia](./project/algolia.md).

По умолчанию поиск **отключен**, для его появления настройте секцию `search`.

#### Общие параметры {#search-common}

#|
|| **Название** | **Описание** | **Тип и значение по умолчанию** ||
|| `provider` | Выбор поисковой системы.
Варианты:

* `local` — локальный поиск (Lunr.js);
* `algolia` — облачный поиск на базе Algolia. | `string`

— (поиск не подключен) ||
|#

#### Параметры для локального поиска (`provider: local`) {#search-local}

#|
|| **Название** | **Описание** | **Тип и значение по умолчанию** ||
|| `tolerance`  | Глубина расширения совпадений:

* 0 — только полное совпадение слова;
* 1 — совпадение по префиксу (`word*`);
* 2 — совпадение по любой подстроке слова (`*word*`). | `number`

`2` ||
|| `confidense` | Режим ранжирования результатов:

* `phrased` — выше ранжируются результаты по длине найденной фразы;
* `sparsed` — выше ранжируются результаты по количеству найденных слов. | `string`

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
Если `false`, только создается локальный индекс. | `boolean`

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

* Для активации поиска обязательно добавьте секцию `search` и укажите `provider`.
* Для больших проектов рекомендуется облачный поиск Algolia.
* Не публикуйте `apiKey` от Algolia в публичных репозиториях или продакшн-конфигурациях — используйте переменные среды либо CLI-параметры.

{% endnote %}

## Пример файла `.yfm` {#yfm}

```yaml
# Корневая секция параметров
strict: true
breaks: false
apply-presets: true
varsPreset: 'external'
needToSanitizeHtml: true
langs: ['en', 'ru']

# Настройки интерфейса документации
interface:
  favicon-src: https://raw.githubusercontent.com/yandex-cloud/yfm-documentation/master/_images/logo_blue_32x32.png

# Секция параметров вьюера (docs-viewer)
docs-viewer:
  project-name: project-name
  no-index: true
  langs: ['en', 'ru']
  metrika: 678489

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
