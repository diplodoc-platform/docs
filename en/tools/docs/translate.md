---
keywords: ['translate', 'xliff', 'cat', 'i18n', 'l10n', 'localization', 'internationalization']
---
# Localization

The `{{PROGRAM}} translate` command translates project documentation from one language into others. Text is extracted from the markup, translated using the selected method, and assembled back into files - the project structure, markup, and code are preserved.

In a multilingual project, each language version lives in its own language folder (`ru/`, `en/`, and so on) with its own `toc.yaml` and content files.

## Translation methods {#methods}

### Machine translation {#auto}

Translation via [Yandex Translate](https://yandex.cloud/en/services/translate) - the default method, used when the `--provider` option is omitted. The fastest option, but the result usually needs proofreading. For details, see [Machine translation](translate-yandex.md).

### AI translation {#ai}

Translation with large language models: the `yandexgpt`, `openai`, `openrouter`, and `anthropic` providers. Supports glossaries, prompts, a translation cache, and quality evaluation by a second model. For details, see [AI translation](translate-ai.md).

### XLIFF exchange with CAT tools {#cat}

If translation is done by people in a Computer Assisted Translation (CAT) tool, the `extract` subcommand exports the project text into `*.xliff` files, and `compose` assembles the translated files back into documentation. For details, see [XLIFF exchange with CAT tools](translate-xliff.md).

## How translation works {#pipeline}

Each document is split into segments - sentences, headings, table cells. YFM markup, HTML tags, code, and Liquid constructs are not sent for translation: they stay in the document "skeleton", and after translation the segments are put back in place. Repeated segments are translated once.

Files of each language live in their own language folder: sources, for example, in `ru/`, and the translation result in the target language folder, for example `en/`. You don't need to specify the language folder in paths - it is added automatically based on the `--source` and `--target` values.

## What is translated {#scope}

By default, translation covers files matching `{lang}/**/*.@(md|yaml|json)`:

* `*.md` - YFM markup text;
* `*.yaml` and `*.json` - only the fields described in a translation schema.

### Translation schemas for YAML and JSON {#json-schemas}

A schema defines which fields of a structured file contain translatable text. Built-in schemas exist for:

* `toc.yaml` tables of contents;
* [leading pages](../../project/leading-page.md) `index.yaml`;
* [variable presets](../../project/presets.md) `presets.yaml`;
* [Page constructor](../../project/page-constructor.md) pages.

Custom schemas can be plugged in with the `--schema` option of the [extract](translate-xliff.md#extract) subcommand.

## Common parameters {#options}

These parameters work the same in all translation methods. Method-specific parameters are described in the articles on [machine translation](translate-yandex.md#options), [AI translation](translate-ai.md#options), and [XLIFF exchange](translate-xliff.md).

#|
|| **Parameter** | **Description** ||
|| `--source`, `-sl` |
Source document language in ISO 639-1 format: `ru` or `ru-RU`. Required
||
|| `--target`, `-tl` |
Target language: `en` or `en-US`. Can be passed multiple times - translation is performed into each language
||
|| `--input`, `-i` |
Path to the project **root** or to a specific file in the project. Defaults to the directory the command is run from
||
|| `--output`, `-o` |
Path to the project **root** where the translation should be saved. Defaults to `input`
||
|| `--files` |
Paths to files to translate (relative to `input`) or a path to a [list file](#file-filter). Can be repeated. When set, `--include` and `--exclude` are ignored
||
|| `--include` |
Rule for selecting files: a path, a glob pattern, or a [list file](#file-filter). Can be repeated. The rules you pass replace the default rule; to restore it, add a separate `--include ...` rule
||
|| `--exclude` |
Rule for excluding files: a path or a glob pattern. Applied after `--include`. Can be repeated
||
|| `--config`, `-c` |
Path to the configuration file. Defaults to `.yfm` in the project root
||
|#

### Provider translation parameters {#provider-options}

These work when translating via [Yandex Translate](translate-yandex.md) and [AI providers](translate-ai.md), but not in the `extract` and `compose` subcommands.

#|
|| **Parameter** | **Description** ||
|| `--provider` |
Translation system: `yandex` (default), `yandexgpt`, `openai`, `openrouter`, or `anthropic`
||
|| `--include-vcs-diff` |
Adds files changed in the git or arc working copy to the translation. The `input` directory must be inside a repository.
\
The optional value is the ref to compute the diff against (defaults to `HEAD`). Git-syntax ranges (`a..b`, `a...b`) work for both systems. Untracked files are always included.
\
Combines with `--include`: files from both sets are translated. If there are no changes, the command finishes successfully without translation
||
|| `--vars`, `-v` |
Build variables in JSON format. The `translate` command ignores `presets.yaml` - variables are passed only via this option
||
|| `--dry-run` |
Do not translate, only estimate the amount of text and the number of provider requests
||
|| `--copy-assets` |
Copy non-translatable files (images and other assets) from the source language folder to the target language folders, so the translated version builds on its own
||
|| `--timeout` |
Timeout for a single translation API request, in milliseconds. Defaults to `5000`
||
|#

### Fixed file list {#file-filter}

If you need to limit translation to a known set of files, a list file - for example, `translate.list` - is more convenient than glob patterns. Pass it to the `--files` or `--include` parameter:

```bash
{{PROGRAM}} translate --files ./translate.list --source ru --target en
```

```text
# The file supports comments and empty lines

# Paths are resolved relative to the translate.list file itself
./some/path/to/translated/file-1.md
./some/path/to/translated/file-2.md

# Paths must not point above translate.list
# Example of an invalid path:
../some/path/to/translated/file.md
```

## Excluding content from translation {#content-filter}

Parts of the content can be excluded from translation right in the markup.

* `translate=no` - for code blocks:

  ````
  ```sql translate=no
  SELECT * FROM posts WHERE id=123 LIMIT 1
  ```
  ````

* `:no-translate[]` - for inline fragments (works in md and yaml files):

  ```
  Date format: :no-translate[ISO 8601] with an offset from :no-translate[UTC].
  ```

* `:::no-translate` - for content blocks:

  ```
  :::no-translate
  This entire block will not be sent for translation.
  :::
  ```
