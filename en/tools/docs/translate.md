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

Each document is split into segments - sentences, headings, table cells. YFM markup, HTML tags, Liquid constructs, and code (except comments and labels, see [Code and diagrams](#code)) are not sent for translation: they stay in the document "skeleton", and after translation the segments are put back in place. Repeated segments are translated once.

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

`::: page-constructor` blocks inside `.md` files are parsed schema-aware as well: only the text fields of the blocks are sent for translation, while the YAML structure of the block stays in the document skeleton and returns to the file unchanged.

Custom schemas can be plugged in with the `--schema` option of the [extract](translate-xliff.md#extract) subcommand.

### Code and diagrams {#code}

Only the parts of code blocks written for the reader go to translation. How much exactly is set by the `--code` option (the `code` key in the `translate` section of `.yfm`):

#|
|| **Mode** | **What is translated** ||
|| `no` | Nothing, code blocks are copied as they are ||
|| `precise` | Placeholders in angle brackets (`<cluster-name>`) and comments in `bash` and `shell` blocks ||
|| `adaptive` | Also line comments in blocks of any language (`#`, `//`, `--`) and labels of [Mermaid](../../custom-plugins/mermaid.md) diagrams: nodes, edges, notes, titles. Commented-out code, tool directives, and separators stay as they are ||
|| `all` | The whole block, code included ||
|#

AI providers work in the `adaptive` mode by default, [Yandex Translate](translate-yandex.md) in the `precise` mode. The code itself is not translated in any mode except `all`.

The mode of a single block is set in its info string:

````markdown
```yaml translate=precise
# This comment stays in the source language
key: value
```
````

The [`seed`](translate-ai.md#seed) subcommand must run in the same mode as the translation: the mode decides which segments a file is split into. If you change the mode, pass the same `--code` value to both commands.

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
|| `--code` |
How much of code blocks goes to translation: `no`, `precise`, `adaptive`, or `all`. Defaults to `adaptive` for AI providers and `precise` for Yandex Translate. See [Code and diagrams](#code)
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
|| `--report` |
Path of the file to write a machine-readable JSON run report to. Disabled by default; a short summary line is always logged. See [Run report](#report)
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

## Run report {#report}

The `--report` option writes a machine-readable JSON report of the translation run: timings, translation volume, cache and fallback usage, quality scores and errors. The report is meant for automation around translation - CI pipelines, usage accounting, dashboards. It does not affect translation itself and is disabled by default.

```bash
{{PROGRAM}} translate -i . -o ./translated --provider openai --source ru --target en \
  --report ./translate-report.json
```

A command-line path is resolved from the current directory; a path from the [configuration file](translate-ai.md#config) (the `report` key) is resolved from the location of `.yfm`.

A short summary line is always logged, with or without the option:

```
INFO PROCESSED run success in 12.4s; files: 12 translated, 0 failed; units: 340 (154 cached, 45.3% hit rate); chars: 15200 in / 16900 out; tokens: 5200 in / 4800 out; requests: 18 (2 fallback, 3 retries); errors: 0
```

### Report structure {#report-schema}

The report shape is a public contract. The `schemaVersion` field is bumped on any breaking change of the format, so a consumer should check it and reject versions it does not understand instead of reading the data blindly. The current version is `1`.

Top-level fields:

#|
|| **Field** | **Description** ||
|| `schemaVersion` | Report schema version ||
|| `startedAt`, `finishedAt` | Run start and finish time in ISO 8601 format ||
|| `durationMs` | Run duration in milliseconds ||
|| `status` | `success`, `partial` (the run finished but recorded errors) or `failed` (the run was aborted by a fatal error) ||
|| `provider` | Translation provider: `yandex`, `yandexgpt`, `openai`, `openrouter` or `anthropic` ||
|| `model`, `fallbackModel` | The model and the [fallback model](translate-ai.md#fallback). AI providers only ||
|| `fallbackUsed` | `true` when at least one request was served by the fallback model ||
|| `dryRun` | `true` for a `--dry-run` run: volume and tokens in such a report are estimates ||
|| `sourceLanguage`, `targetLanguages` | Languages of the run ||
|| `files` | `selected` - files picked for translation, `skipped` - files filtered out before translation ||
|| `totals` | Counters summed over all target languages ||
|| `targets` | Counters per target language, plus a `judge` block when [quality assessment](translate-ai.md#judge) is enabled ||
|| `errors` | Recorded errors: `target`, `path`, a stable `code` and a message ||
|#

Counters (`totals` and every entry of `targets`):

#|
|| **Field** | **Description** ||
|| `files` | `translated` - processed files, `failed` - failed ones, `retried` - files re-queued after transient errors ||
|| `units` | Segments: `total` - seen in total, `translated` - translated during this run, `fromCache` - served from the [cache](translate-ai.md#cache), `untranslated` - returned by the model untranslated, `oversized` - skipped as too big for a single request ||
|| `chars` | Characters: `source` - in the source segments, `translated` - in the translations of this run, `request` - actually sent in requests ||
|| `tokens` | Token usage as reported by the provider: `input` and `output`. `null` when the provider does not report usage ||
|| `requests` | Requests: `total` - in total, `fallback` - served by the fallback model, `retries` - extra attempts after transient errors ||
|| `cache` | `enabled` - whether the cache was active, `hits` and `misses` - lookups, `hitRate` - the hit ratio or `null`, `hints` - segments sent with their previous version from the seed (see [Changed sentences](translate-ai.md#seed-hints)) ||
|| `fixes` | Repairs of model answers, see [Repairing model answers](translate-ai.md#fixes) ||
|#

The `judge` block of a `targets` entry appears when quality assessment is enabled and holds the judge model (`model`), the threshold (`threshold`), the number of scored pairs (`scored`), the average score (`averageScore`), the number of pairs below the threshold (`belowThreshold`), the number of pairs the judge failed to score (`unscored`) and the `distribution` histogram with the keys `0-9` ... `90-99` and `100`.

All counters are filled by AI providers only. [Machine translation](translate-yandex.md) has no token usage, no cache, no quality assessment and no markup repair: `tokens` in its report is `null`, `cache.enabled` is `false`, the `fixes` counters stay zero and there is no `judge` block.

An example report:

```json
{
  "schemaVersion": 1,
  "startedAt": "2026-08-25T10:00:00.000Z",
  "finishedAt": "2026-08-25T10:00:12.400Z",
  "durationMs": 12400,
  "status": "success",
  "provider": "openai",
  "model": "gpt-4o-mini",
  "fallbackModel": "gpt-4o",
  "fallbackUsed": true,
  "dryRun": false,
  "sourceLanguage": "ru",
  "targetLanguages": ["en"],
  "files": {"selected": 12, "skipped": 3},
  "totals": {
    "files": {"translated": 12, "failed": 0, "retried": 1},
    "units": {"total": 340, "translated": 182, "fromCache": 154, "untranslated": 4, "oversized": 0},
    "chars": {"source": 15200, "translated": 16900, "request": 8300},
    "tokens": {"input": 5200, "output": 4800},
    "requests": {"total": 18, "fallback": 2, "retries": 3},
    "cache": {"enabled": true, "hits": 154, "misses": 186, "hitRate": 0.4529, "hints": 12},
    "fixes": {
      "markupStripped": 2,
      "markupRetried": 1,
      "markupDamaged": 0,
      "untranslatedRetried": 1,
      "untranslatedKept": 0
    }
  },
  "targets": [
    {
      "language": "en",
      "files": {"translated": 12, "failed": 0, "retried": 1},
      "units": {"total": 340, "translated": 182, "fromCache": 154, "untranslated": 4, "oversized": 0},
      "chars": {"source": 15200, "translated": 16900, "request": 8300},
      "tokens": {"input": 5200, "output": 4800},
      "requests": {"total": 18, "fallback": 2, "retries": 3},
      "cache": {"enabled": true, "hits": 154, "misses": 186, "hitRate": 0.4529, "hints": 12},
      "fixes": {
        "markupStripped": 2,
        "markupRetried": 1,
        "markupDamaged": 0,
        "untranslatedRetried": 1,
        "untranslatedKept": 0
      }
    }
  ],
  "errors": []
}
```

The run report and the [quality assessment](translate-ai.md#judge) report are different files. The run report carries only the aggregate scores; the per-segment breakdown stays in `translate-quality.<language>.json`.

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
