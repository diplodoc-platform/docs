---
meta:
  tags: ['translate', 'xliff', 'cat', 'i18n', 'l10n', 'localization', 'internationalization']
---
# Локализация

Для перевода документации на разные языки используется команда `{{PROGRAM}} translate`, которая обеспечивает быстрые [автоматические переводы](#auto).

Подкоманды `extract` и `compose` этой команды позволяют работать с системами [машинного перевода](#cat) (Computer Assisted Translation, или CAT), обмениваясь с ними `*.xliff` файлами.

Поддерживается перевод как `*.md` файлов так и `*.json` (в том числе `*.yaml`) файлов по [описанным схемам](#json-schemas).

## Автоматический перевод {#auto}

```bash
{{PROGRAM}} translate --source {{translate.source}} --target {{translate.target}}
```

Автоматический перевод может быть выполнен с использованием таких сервисов, как [Yandex Translate](https://cloud.yandex.ru/docs/translate/){% if translate.google-support == true %} или [Cloud Translate](https://cloud.google.com/translate/docs){% endif %}.

Эти системы имеют определенные [ограничения](https://cloud.yandex.ru/ru/docs/translate/concepts/limits) по объему документов, которые могут быть переведены, а также по качеству перевода. Однако они значительно выигрывают с точки зрения скорости.

С целью уменьшения объема текста, подлежащего переводу, документ разбивается на более короткие сегменты, такие как предложения или заголовки. Повторяющиеся сегменты затем удаляются.

Так же для уменьшения объема переводов поддерживаются `include` и `exclude` фильтры.

Параметр запуска `--dry-run` может быть использован для определения объема текста, готового к переводу.

Если лимиты превышены, команда завершится с ошибкой `TRANSLATE_LIMIT_EXCEED`.

### Использование

* Перевести проект в текущей директории с `{{translate.source-lang}}` на `{{translate.target-lang}}`:

  ```
  {{PROGRAM}} translate --source {{translate.source-lang}} --target {{translate.target-lang}}
  ```

* Не переводить скрытые файлы в проекте:

  ```
  {{PROGRAM}} translate --exclude {{translate.source-lang}}/**/_*.* --source {{translate.source-lang}} --target {{translate.target-lang}}
  ```

### Параметры вызова

##### Основные

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

##### Система переводов

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

### Файл фильтр

Если необходимо ограничить переводимые тексты фиксированным набором файлов, механизм гибких фильтров `include/exclude` может не подойти.
В таком случае можно сформировать файл с расширением `*.list`. Например `translate.list`.

```
# Файл поддерживает комментарии и пустые строки

# Пути до файлов должны быть сформированы относительно самого файла translate.list.
./some/path/to/translated/file-1.md
./some/path/to/translated/file-2.md

# Пути до файлов не должны находиться выше чем translate.list.
# Пример неправильного пути:
../some/path/to/translated/file.md
```

Пример вызова команды с файлом фильтром

```bash
{{PROGRAM}} translate --input ./translate.list --source {{translate.source-lang}} --target {{translate.target-lang}}
```