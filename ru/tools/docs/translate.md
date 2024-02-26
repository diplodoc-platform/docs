---
meta:
  tags: ['translate', 'xliff', 'cat']
---
# Локализация

Для перевода документации на разные языки используется команда `{{PROGRAM}} translate`, которая обеспечивает быстрые [автоматические переводы](#auto).

Подкоманды `extract` и `compose` этой команды позволяют работать с системами [машинного перевода](#cat) (Computer Assisted Translation, или CAT), обмениваясь с ними `*.xliff` файлами.

Поддерживается перевод как `*.md` файлов так и `*.json` (в том числе `*.yaml`) файлов по [описанным схемам](#json-schemas).

## Автоматический перевод {#auto}

Автоматический перевод может быть выполнен с использованием таких сервисов, как [Yandex Translate](https://cloud.yandex.ru/docs/translate/){% if translate.google-support == true %} или [Cloud Translate](https://cloud.google.com/translate/docs){% endif %}.

Эти системы имеют определенные [ограничения](https://cloud.yandex.ru/ru/docs/translate/concepts/limits) по объему документов, которые могут быть переведены, а также по качеству перевода. Однако они значительно выигрывают с точки зрения скорости.

С целью уменьшения объема текста, подлежащего переводу, документ разбивается на более короткие сегменты, такие как предложения или заголовки. Повторяющиеся сегменты затем удаляются.

Так же для уменьшения объема переводов поддерживаются `include` и `exclude` фильтры.

Параметр запуска `--dry-run` может быть использован для определения объема текста, готового к переводу.

Если лимиты превышены, команда завершится с ошибкой `TRANSLATE_LIMIT_EXCEED`.

### Параметры вызова

#### Основные

#|
|| Параметр             | Формат    | Описание ||
|| --source {{required}}| {{fmt.locale}} |
Код языка оригинального документа в формате ISO 639-1
\
`{{PROGRAM}} translate --source {{translate.source}}`
||
|| --target {{required}}| {{fmt.locale}} |
Код языка переведенного документа в формате ISO 639-1
\
`{{PROGRAM}} translate --target {{translate.target}}`
||
|| --input              | Path      | 
Путь до **корня** переводимого проекта или конкретного файла в проекте. Если не указан используется директория запуска команды.
\
Директорию языка в пути указывать не надо - она добавляется автоматически. 
\
`{{PROGRAM}} translate -i ./docs`
\
`{{PROGRAM}} translate -i ./docs/index.md`
\
Так же в качестве пути можно указать [файл фильтр](#filter).
\
`{{PROGRAM}} translate -i translate.list` 
||
|| --output             | Path      |
Путь до **корня** проекта, в который нужно сохранить перевод. Если не указан используется `input` директория.
||
|| --include            | {{fmt.glob}} |
Набор правил для фильтрации отправляемых на перевод файлов. По умолчанию `{lang}/**/*.@(md\|yaml\|json)`.
\
Может быть передан несколько раз.
\
Игнорируется, если используется [файл фильтр](#filter).
\
`{{PROGRAM}} translate --include {{translate.source-lang}}/**/*.md`
||
|| --exclude            | {{fmt.glob}} |
Набор правил запрещающих отправлять файлы на перевод. Применяется после `include`.
\
Может быть передан несколько раз.
\
`{{PROGRAM}} translate --exclude {{translate.source-lang}}/_no-translate/**/*.md`
||
|#

#### Система переводов

{% list tabs %}

- Yandex Translation

  #|
  || Параметр             | Формат         | Описание ||
  || --auth {{required}}  | Path<br/>{{fmt.iam-token}}<br/>{{fmt.api-key}} |
  Токен авторизации. Может быть передан несколькими способами:
  \
  {{fmt.iam-token}} как параметр командной строки
  \
    `{{PROGRAM}} translate --auth <token>`
  \
  Путь до файла, в котором хранится {{fmt.iam-token}}
  \
  `{{PROGRAM}} translate --auth path/to/.auth`
  \
  Путь до файла, в котором хранится {{fmt.api-key}} сервисного аккаунта.
  \
  `{{PROGRAM}} translate --auth path/to/.api-key`

  ||
  || --folder {{required}}  | Id |
  [Идентификатор каталога](https://cloud.yandex.ru/ru/docs/resource-manager/operations/folder/get-id), на который у вашего аккаунта есть роль `ai.translate.user` или выше.
  ||
  {% if glossary-support == true %}
  || --glossary | Path |
  TODO
  ||
  {% endif %}
  |#

{% endlist %}
