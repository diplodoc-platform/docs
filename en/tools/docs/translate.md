---
keywords: ['translate', 'xliff', 'cat', 'i18n', 'l10n', 'localization', 'internationalization']
---
# Localization

To translate documentation into different languages, the `{{PROGRAM}} translate` command is used, which provides fast [automatic translations](#auto).

In addition to translation via [Yandex Translate](#auto), [AI translation](translate-ai.md) using large language models is supported (providers `yandexgpt`, `openai`, `openrouter` and `anthropic`).

The `extract` and `compose` subcommands of this command allow working with [machine translation](#cat) systems (Computer Assisted Translation, or CAT), exchanging `*.xliff` files with them.

Translation is supported for both `*.md` files and `*.json` (including `*.yaml`) files according to the [described schemas](#json-schemas).

## Parameters for invoking the extract subcommand

#|
|| Parameter             | Path
|| `--schema not_var{{optional}}` | 
Путь до одного или нескольких файлов, содержащих кастомные схемы для перевода.
\
`{{PROGRAM}} translate extract --schema ./some/path/to/file.yaml ./some/path/toAnother/file.yaml`
|#

## Automatic translation {#auto}

```bash
{{PROGRAM}} translate --source not_var{{translate.source}} --target not_var{{translate.target}}
```

Automatic translation can be performed using services such as [Yandex Translate](https://cloud.yandex.ru/docs/translate/){% if translate.google-support == true %} or [Cloud Translate](https://cloud.google.com/translate/docs){% endif %}.

This mode is enabled by default: without the `--provider` option the `yandex` value is used, so the option is omitted in the examples below.

These systems have [limits](https://cloud.yandex.ru/ru/docs/translate/concepts/limits) on the volume of translated documents and translation quality. However, they are characterized by high processing speed.

To reduce the volume of text for translation, the document is split into shorter segments, such as sentences or headings. Repeated segments are then removed.

To further reduce the volume of translations, `include` and `exclude` filters are supported.

The `--dry-run` launch parameter can be used to determine the volume of text ready for translation.

If limits are exceeded, the command will terminate with the error `TRANSLATE_LIMIT_EXCEED`.

### Usage

* Translate a project in the current directory from `not_var{{translate.source-lang}}` to `not_var{{translate.target-lang}}`:

  ```bash
  {{PROGRAM}} translate --source not_var{{translate.source-lang}} --target not_var{{translate.target-lang}}
  ```

* Do not translate hidden files in the project:

  ```bash
  {{PROGRAM}} translate --exclude not_var{{translate.source-lang}}/**/_*.* --source not_var{{translate.source-lang}} --target not_var{{translate.target-lang}}
  ```

### Call parameters

#### Main

#|
|| Parameter             | Format    | Description ||
|| `--source`{{required}}| {{fmt.locale}} |
Language code of the original document in ISO 639-1 format
\
`{{PROGRAM}} translate --source {{translate.source}}`
||
|| `--target`{{required}}| {{fmt.locale}} |
Language code of the translated document in ISO 639-1 format
\
`{{PROGRAM}} translate --target {{translate.target}}`
||
|| `--provider`           | `yandex` \| `yandexgpt` \| `openai` \| `openrouter` \| `anthropic` |
Translation system. The default value is `yandex` - machine translation via [Yandex Translate](#auto).
\
The other values enable [AI translation](translate-ai.md) using large language models.
\
`{{PROGRAM}} translate --provider yandex`
||
|| `--input`              | Path      |
Path to the **root** of the project being translated or a specific file in the project. If not specified, the directory from which the command is launched is used.
\
You do not need to specify the language directory in the path — it is added automatically.
\
`{{PROGRAM}} translate -i ./docs`
\
`{{PROGRAM}} translate -i ./docs/index.md`
\
You can also specify a [filter file](#filter) as the path.
\
`{{PROGRAM}} translate -i translate.list` 
||
|| `--output`             | Path      |
Path to the **root** of the project where the translation should be saved. If not specified, the `input` directory is used.
||
|| `--include`            | {{fmt.glob}} |
A set of rules for filtering files sent for translation. By default, `{lang}/**/*.@(md\|yaml\|json)`.
\
Can be passed multiple times.
\
Ignored if a [filter file](#filter) is used.
\
`{{PROGRAM}} translate --include {{translate.source-lang}}/**/*.md`
||
|| `--exclude`            | {{fmt.glob}} |
A set of rules that prohibit sending files for translation. Applied after `include`.
\
Can be passed multiple times.
\
`{{PROGRAM}} translate --exclude {{translate.source-lang}}/_no-translate/**/*.md`
||
|| `--include-vcs-diff`   | Ref |
Adds files changed in the git or arc working copy to the translation. The `input` directory must be inside a repository.
\
The optional value is the ref against which the diff is computed (`HEAD` by default). Git-style ranges (`a..b`, `a...b`) work for both systems. Untracked files are always included.
\
Combines with `--include`: files from both sets are translated. If there are no changes, the command finishes successfully without translation.
\
`{{PROGRAM}} translate --include-vcs-diff`
\
`{{PROGRAM}} translate --include-vcs-diff origin/main`
||
|#

#### Translation system

The set of additional options depends on the `--provider` value. Options for AI providers (`yandexgpt`, `openai`, `openrouter`, `anthropic`) are described in the [AI translation](translate-ai.md#options) article.

{% list tabs %}

- Yandex Translation

  #|
  || Parameter             | Format         | Description ||
  ||

  `--auth`{{required}} 
  
  |
  
  Path
  {{fmt.iam-token}}
  {{fmt.api-key}}

  |
  Authorization token. Can be passed in several ways:
  \
  {{fmt.iam-token}} as a command-line parameter
  \
    `{{PROGRAM}} translate --auth <token>`
  \
  Path to a file that stores the {{fmt.iam-token}}
  \
  `{{PROGRAM}} translate --auth path/to/.auth`
  \
  Path to a file that stores the {{fmt.api-key}} of the service account.
  \
  `{{PROGRAM}} translate --auth path/to/.api-key`

  ||
  ||
  
  `--folder`{{required}} 
  
  |
  
  Id
  
  |
  [Identifier of the folder](https://cloud.yandex.ru/ru/docs/resource-manager/operations/folder/get-id) for which your account has the role `ai.translate.user` or higher.
  ||
  ||
  
  `--timeout` 
  
  |
  
  Number
  
  |

  Translation wait time in milliseconds, default value is 5000 (5 seconds).

  ||
  |#
  
{% endlist %}

### File filtering {#file-filter}

If you need to limit the translated texts to a fixed set of files, the flexible `include/exclude` filter mechanism may not be suitable.
In this case, you can create a file with the `*.list` extension. For example, `translate.list`.

```
# Файл поддерживает комментарии и пустые строки

# Пути до файлов должны быть сформированы относительно самого файла translate.list.
./some/path/to/translated/file-1.md
./some/path/to/translated/file-2.md

# Пути до файлов не должны находиться выше, чем translate.list.
# Пример неправильного пути:
../some/path/to/translated/file.md
```

Example of calling the command with a filter file

```bash
{{PROGRAM}} translate --input ./translate.list --source not_var{{translate.source-lang}} --target not_var{{translate.target-lang}}
```

### Filtering page content {#content-filter}

To exclude parts of content from translation, the platform provides the following syntactic constructs.

* `translate=no` for code blocks:
  ````
  ```sql translate=no
  // этот блок не уйдёт на перевод
  SELECT * FROM posts WHERE id=123 LIMIT 1
  ```
  ````

* `:no-translate` for string fragments (works in yaml and md files):
  ```
  Формат даты: :no—translate[ISO 8601] со смещением относительно :no—translate[UTC].
  ```

* `:::no-translate` for content blocks:
  ```
  :::no–translate
  // весь этот блок не уйдёт на перевод
  Inconsistent indentation for list items at the same level:
    * One
  * Two
  * Three
  :::
  ```
