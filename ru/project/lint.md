# Файл конфигурации линтера

В корне проекта можно разместить файл конфигурации линтера `.yfmlint` для управления проверками сборки документации.

Значения настроек по умолчанию:

```yaml
log-levels:
  MD001: 'disabled' # Heading levels should only increment by one level at a time
  MD002: 'disabled' # First heading should be a top-level heading~~
  MD003: 'disabled' # Heading style
  MD004: 'disabled' # Unordered list style
  MD005: 'disabled' # Inconsistent indentation for list items at the same level
  MD006: 'disabled' # Consider starting bulleted lists at the beginning of the line~~
  MD007: 'disabled' # Unordered list indentation
  MD009: 'disabled' # Trailing spaces
  MD010: 'disabled' # Hard tabs
  MD011: 'disabled' # Reversed link syntax
  MD012: 'disabled' # Multiple consecutive blank lines
  MD013: 'disabled' # Line length
  MD014: 'disabled' # Dollar signs used before commands without showing output
  MD018: 'error'    # No space after hash on atx style heading
  MD019: 'disabled' # Multiple spaces after hash on atx style heading
  MD020: 'disabled' # No space inside hashes on closed atx style heading
  MD021: 'disabled' # Multiple spaces inside hashes on closed atx style heading
  MD022: 'disabled' # Headings should be surrounded by blank lines
  MD023: 'disabled' # Headings must start at the beginning of the line
  MD024: 'disabled' # Multiple headings with the same content
  MD025: 'disabled' # Multiple top-level headings in the same document
  MD026: 'disabled' # Trailing punctuation in heading
  MD027: 'disabled' # Multiple spaces after blockquote symbol
  MD028: 'disabled' # Blank line inside blockquote
  MD029: 'disabled' # Ordered list item prefix
  MD030: 'disabled' # Spaces after list markers
  MD031: 'disabled' # Fenced code blocks should be surrounded by blank lines
  MD032: 'disabled' # Lists should be surrounded by blank lines
  MD033: 'disabled' # Inline HTML
  MD034: 'disabled' # Bare URL used
  MD035: 'disabled' # Horizontal rule style
  MD036: 'disabled' # Emphasis used instead of a heading
  MD037: 'disabled' # Spaces inside emphasis markers
  MD038: 'disabled' # Spaces inside code span elements
  MD039: 'disabled' # Spaces inside link text
  MD040: 'disabled' # Fenced code blocks should have a language specified
  MD041: 'disabled' # First line in a file should be a top-level heading
  MD042: 'disabled' # No empty links
  MD043: 'disabled' # Required heading structure
  MD044: 'disabled' # Proper names should have the correct capitalization
  MD045: 'disabled' # Images should have alternate text (alt text)
  MD046: 'disabled' # Code block style
  MD047: 'disabled' # Files should end with a single newline character
  MD048: 'disabled' # Code fence style
  
  YFM001: 'warn'    # Inline code length
  YFM002: 'warn'    # No header found in the file for the link text
  YFM003: 'error'   # Link is unreachable
  YFM004: 'error'   # Table not closed
  YFM005: 'warn'    # Tab list, cut, note not opened or closed
  YFM006: 'warn'    # Term definition duplicated
  YFM007: 'warn'    # Term used without definition
  YFM008: 'warn'    # Term inside definition not allowed
  YFM009: 'error'   # Term definition used not at the end of file
  YFM010: 'warn'    # Autotitle anchor is missed
  YFM011: 'warn'    # Max svg size
  YFM012: 'error'   # Max output html size
  YFM013: 'error'   # Max single asset size
  YFM014: 'warn'    # Anchor cannot be used as file path
  YFM015: 'warn'    # Anchor not found in file
  YFM016: 'error'   # The file is included in itself
  YFM017: 'error'   # Invalid front matter format: duplicated mapping key
  YFM018: 'info'    # Term definition from include
  YFM020: 'warn'    # Invalid yfm directive
  YFM021: 'warn'    # Empty automatic heading anchor
  YFM022: 'info'    # llms-full.txt max size reached
  YFM025: 'warn'    # Local link anchor is missing in the target document


# Inline code length
YFM001:
  maximum: 100
```

Правила с префиксом `MD` предоставляются библиотекой [markdownlint](https://github.com/DavidAnson/markdownlint).
Подробное описание всех правил с префиксом `MD` можно найти [по ссылке](https://github.com/DavidAnson/markdownlint/blob/main/doc/Rules.md).
Подробное описание всех правил с префиксом `YFM` можно найти [по ссылке](https://github.com/diplodoc-platform/yfmlint/blob/master/README.md).

YFM021 сообщает о заголовках с пустым автоматическим якорем. Правило использует плагин anchors из `@diplodoc/transform`; Diplodoc CLI и расширение для VS Code подключают его по умолчанию.

Вы можете переопределить уровень логирования в файле `.yfmlint` в секции `log-levels` отдельно для каждого правила: `error`, `warn`, `disabled`.

{% note warning %}

Нельзя переопределить ошибки `YFM014`, `YFM015`, `YFM016` и `YFM017`.

{% endnote %}

В корневой секции можно настроить значения, передаваемые правилам. Например:

```yaml
# Inline code length
YFM001:
  level: warn
  maximum: 100

# Supported yfm directives
YFM020:
  level: warn
  customDirectives:
    - diagram       # skip warning on {% diagram %} directive

# Line length
MD013:
  line_length: 100 # default: 80 characters
  code_blocks: false # exclude this rule for code_blocks
  tables: false # exclude this rule for tables
  headings: false # exclude this rule for headings

# Inline HTML
MD033:
  allowed_elements: [ "span", "br", "p" ]


# Section for defining log levels
log-levels:
```

Исходные значения для правил с префиксом `MD` указаны [по ссылке](https://github.com/DavidAnson/markdownlint/blob/main/schema/.markdownlint.yaml).
Исходные значения для правил с префиксом `YFM` указаны [по ссылке](https://github.com/diplodoc-platform/yfmlint/blob/master/src/config.ts).

Правила можно включить, выключить, настроить для всего файла или абзаца в файле.
Примеры можно посмотреть [по ссылке](https://github.com/DavidAnson/markdownlint/blob/a852407c887ec60949aa5365ed964bab833f962f/README.md#configuration).

> Смотри также: [Ajv схема файлов конфигурации линтера .yfmlint](https://raw.githubusercontent.com/diplodoc-platform/ajv/refs/heads/master/src/json/yfmlint-schema.json)

## Предупреждения директивы code {#code-directive-warnings}

При [включении кода из файла](../syntax/code.md#include-code) сборщик [Diplodoc CLI](../tools/docs/build.md) — инструмент сборки документации — выводит предупреждения с префиксом `Code directive:`, если маркер фрагмента не найден или конечный маркер расположен раньше начального. Этот префикс также используется для предупреждений о проигнорированных неизвестных атрибутах, лишних аргументах или повторяющихся атрибутах директивы.

Уровень сообщения — `warn`. У этих сообщений нет отдельного кода `MD` или `YFM`. Диагностику выдаёт сборщик при обработке директивы, поэтому её нельзя настроить через `log-levels` в `.yfmlint`; она выводится и при отключённом линтере. Точные тексты сообщений и поведение сборщика приведены в [описании директивы](../syntax/code.md#include-code).

## Где выполняются проверки {#check-implementation}

[Diplodoc CLI](../tools/docs/build.md) выполняет проверки проекта и готовит данные о страницах, включениях и ресурсах. [@diplodoc/transform](https://github.com/diplodoc-platform/transform) обрабатывает разметку, а [@diplodoc/yfmlint](https://github.com/diplodoc-platform/yfmlint) формирует сообщения по правилам проверки.

### Сообщения сборщика

| Коды | Проверка | Роль сборщика |
| --- | --- | --- |
| `YFM012` | Размер HTML страницы | Проверяет размер результата по заданному лимиту |
| `YFM013` | Размер ресурсов | Проверяет размер файлов проекта по заданному лимиту |
| `YFM014`, `YFM015` | Путь и якорь в `include` | Проверяет путь к подключаемому файлу и якорь фрагмента; пропускает некорректное включение |
| `YFM016` | Включение файла в самого себя | Проверяет зависимости при загрузке исходников |
| `YFM017` | Повторяющийся ключ в метаданных | Проверяет метаданные страницы при загрузке исходников |
| `YFM022` | Лимит `llms-full.txt` | Останавливает добавление материалов перед превышением лимита |
| `YAML001` | Локальные ссылки в YAML-страницах | Проверяет существование файлов; уровень задаётся через `log-levels.YAML001`, значение `disabled` отключает проверку |

Исходники: [обработка исходников](https://github.com/diplodoc-platform/cli/tree/master/src/core/markdown/loader), [проверки при выводе HTML](https://github.com/diplodoc-platform/cli/tree/master/src/commands/build/features/output-html), [генерация полного текста](https://github.com/diplodoc-platform/cli/blob/master/src/commands/build/features/llms/index.ts).

### Совместные проверки

Для этих правил сборщик подготавливает данные, которые используют плагины и линтер.

| Коды | Проверка | Роль сборщика |
| --- | --- | --- |
| `YFM003` | Доступность ссылок | Проверяет локальные файлы и наличие страниц в оглавлении |
| `YFM010` | Автоподстановка заголовков ссылок | Собирает заголовки целевых страниц |
| `YFM011` | Размер встраиваемого SVG | Передаёт содержимое файлов и лимит размера |
| `YFM009`, `YFM018` | Определения терминов во включениях | Загружает включения и сохраняет сведения о происхождении определений |
| `YFM025` | Якоря локальных ссылок | Собирает якоря целевых страниц для проверки ссылок |

Исходник: [подготовка данных для проверок](https://github.com/diplodoc-platform/cli/blob/master/src/commands/build/run.ts).

## YFM025 — отсутствующий якорь локальной ссылки

При сборке HTML [Diplodoc CLI](../tools/docs/build.md) — инструмент сборки документации — проверяет, что якорь после `#` в локальной ссылке существует на целевой странице. Проверяются ссылки на текущую страницу (`#section`) и на другие страницы проекта (`guide.md#section`). Учитываются автоматически созданные и явно заданные якоря, в том числе из включённых файлов.

Например, ссылка `[Раздел](guide.md#installation)` вызывает `YFM025 / missing-local-anchor`, если страница `guide.md` доступна, но якоря `installation` на ней нет. Исправьте фрагмент ссылки или добавьте соответствующий якорь на целевой странице. Если недоступна сама страница, сборщик сообщает `YFM003`.

По умолчанию `YFM025` имеет уровень `warn`, независимо от настройки `YFM002`. Для изменения уровня добавьте в `.yfmlint`:

```yaml
log-levels:
  YFM025: error # warn — предупреждение, disabled — отключить проверку
```
