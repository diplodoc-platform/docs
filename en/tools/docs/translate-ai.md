---
keywords: ['translate', 'ai', 'llm', 'yandexgpt', 'openai', 'openrouter', 'anthropic', 'translation', 'machine translation']
---
# AI translation

The command `{{PROGRAM}} translate` can translate documentation using large language models (LLMs). Supported providers are `yandexgpt`, `openai`, `openrouter`, and `anthropic`.

The pipeline is the same as for [other translation providers](translate.md): text is extracted from the markup, translated, and assembled back. Markdown markup, HTML tags, code, and Liquid constructs do not reach the model — only text segments are translated.

Here, a provider describes an API protocol, not a specific vendor: any compatible installation (self-hosted model, internal gateway) can be connected with the same provider by [replacing the API address](#custom-api).

## Quick start {#quickstart}

1. Get an API key and pass it via an environment variable or the `--auth` option (a value or a path to a file with the token):

   ```bash
   export OPENAI_API_KEY="sk-..."
   ```

2. Estimate the translation volume without API requests:

   ```bash
   {{PROGRAM}} translate -i . -o ./translated --provider openai --source ru --target en --dry-run
   ```

   The `PROCESSED` line will show a forecast of the number of requests and tokens. Files in the output are assembled with the original, untranslated text in this case — do not take them as the translation result.

3. Try translating a single file or section:

   ```bash
   {{PROGRAM}} translate -i . -o ./translated --provider openai --source ru --target en \
     --files ru/index.md --cache-dir .translate-cache
   ```

   Check the quality of the result and, if necessary, configure the [glossary](#glossary) or [prompts](#prompts).

4. Run a full pass with caching and asset copying:

   ```bash
   {{PROGRAM}} translate -i . -o ./translated --provider openai --source ru --target en \
     --cache-dir .translate-cache --copy-assets
   ```

5. Check the result: re-running the same command should show `requests: 0` — all segments are taken from the [cache](#cache). The translated version can be built with the usual `{{PROGRAM}} build`.

An error in one file or exceeding limits does not stop the run: failed files are marked with `ERR`, while the rest continue. Re-running the command will finish the leftovers — already translated segments will be taken from the cache.

## Providers {#providers}

#|
|| **Provider** | **API** | **Default model** | **Environment variables** ||
|| `yandexgpt` | [Yandex AI Studio](https://yandex.cloud/ru/docs/ai-studio/) | `yandexgpt-lite` | `YANDEX_API_KEY`, `YC_IAM_TOKEN` ||
|| `openai` | [OpenAI Chat Completions](https://platform.openai.com/docs/api-reference/chat) | `gpt-4o-mini` | `OPENAI_API_KEY` ||
|| `openrouter` | [OpenRouter](https://openrouter.ai/docs) | `openai/gpt-4o-mini` | `OPENROUTER_API_KEY` ||
|| `anthropic` | [Anthropic Messages](https://docs.anthropic.com/en/api/messages) | `claude-sonnet-4-5` | `ANTHROPIC_API_KEY` ||
|#

Authorization:

* `yandexgpt` — IAM token (`t1.`) or OAuth token (`y0_`) are passed as `Bearer`, any other value is passed as the `Api-Key` of the service account. Additionally, `--folder` is required — the [folder ID](https://yandex.cloud/ru/docs/resource-manager/operations/folder/get-id), if `--model` is set with a short name (`yandexgpt-lite`). The full model URI (`gpt://<folder>/yandexgpt/latest`) can be specified without `--folder`.
* `openai`, `openrouter` - Bearer key.
* `anthropic` - key in the `x-api-key` header.

### Connecting compatible installations {#custom-api}

A self-hosted model or an internal gateway with a compatible API is connected using the same provider with the `--api-base` option. The request path is appended to the base automatically:

#|
|| **Provider** | **Default base** | **Request path** ||
|| `yandexgpt` | `https://llm.api.cloud.yandex.net` | `/foundationModels/v1/completion` ||
|| `openai` | `https://api.openai.com/v1` | `/chat/completions` ||
|| `openrouter` | `https://openrouter.ai/api/v1` | `/chat/completions` ||
|| `anthropic` | `https://api.anthropic.com/v1` | `/messages` ||
|#

For `openai`, `openrouter`, and `anthropic`, include `/v1` in the base. The base can also be set via the environment variables `OPENAI_BASE_URL`, `OPENROUTER_BASE_URL`, `ANTHROPIC_BASE_URL`.

If the gateway requires its own authorization scheme, pass the headers using the `--api-header` option (can be repeated). Custom headers override the standard ones, so you can completely replace authorization this way. The `--auth` option is formally required in this case - pass a placeholder:

```bash
{{PROGRAM}} translate -i . -o ./translated \
  --provider openai \
  --api-base https://llm.internal.example.com/v1 \
  --model my-model \
  --auth dummy \
  --api-header "Authorization: OAuth $(cat ~/.tokens/llm)" \
  --source ru --target en --cache-dir .translate-cache
```

The request path for each provider is fixed: if the gateway uses a non-standard path, it cannot be overridden.

## Options reference {#options}

Common command options (`--source`, `--target`, `--files`, `--include`, `--exclude`, `--dry-run`, and others) are described on the [Localization](translate.md) page. The `--target` option can be passed multiple times - translation will be performed into each language. Below are the AI provider options.

#|
|| **Option** | **Default** | **Description** ||
|| `--provider` | `yandex` | Translation provider. For AI translation: `yandexgpt`, `openai`, `openrouter`, or `anthropic`. The default value `yandex` is machine translation via [Yandex Translate](translate.md#auto), not an LLM ||
|| `--auth` | from the environment variable | Token or path to a file with the token. Cannot be placed in the configuration file ||
|| `--model` | depends on the provider | Model identifier ||
|| `--folder` | - | Identifier of the Yandex AI Studio folder. Only for `yandexgpt`, required with a short model name ||
|| `--api-base` | Provider API URL | Base URL for [compatible installations](#custom-api) ||
|| `--api-header` | - | Additional HTTP header in the format `"Name: value"`. Can be repeated. Overrides standard headers ||
|| `--system-prompt` | built-in | System prompt: string or path to a file. See [Prompts](#prompts) ||
|| `--user-prompt` | built-in | User prompt: string or path to a file ||
|| `--prompt-mode` | `append` | `append` - your system prompt is appended to the built-in one, `replace` - completely replaces it ||
|| `--glossary` | - | Path to a YAML file with mandatory term translations, relative to input. See [Glossary](#glossary) ||
|| `--judge` | disabled | Translation quality assessment by a second model. See [Quality assessment](#judge) ||
|| `--judge-model` | translation model | Model for quality assessment ||
|| `--judge-threshold` | `70` | Threshold: segments with a lower score are included in the report and log ||
|| `--cache-dir` | - | Directory for the persistent translation cache. See [Cache](#cache) ||
|| `--no-cache` | - | Disable cache for the current run ||
|| `--temperature` | `0` | Sampling temperature. `0` - deterministic translation ||
|| `--max-output-tokens` | `4000` | Maximum tokens in a single model response ||
|| `--max-batch-tokens` | `2000` | Input token budget for a single request. Segments are grouped into batches up to this limit ||
|| `--max-concurrency` | `5` | Maximum concurrent API requests ||
|| `--retry` | `3` | Number of retries on temporary API errors ||
|| `--timeout` | `60000` | Timeout for a single request in milliseconds ||
|#

### Configuration in a file {#config}

All options except `--auth` can be fixed in the `translate` section of the [configuration file](../../settings.md) `.yfm`. Names are in camelCase, command-line flags take precedence:

```yaml
translate:
  provider: openai
  model: gpt-4o-mini
  cacheDir: .translate-cache
  maxConcurrency: 2
  apiHeaders:
    X-Custom-Header: value
```

The token cannot be stored in the configuration: the command will fail with the error `Do not store authToken in public config`. Use environment variables or `--auth`.

### Prompts {#prompts}

The built-in system prompt is tuned for technical translation: preserve markup, do not translate code and identifiers, do not add explanations. You can add your own instructions to it (`--prompt-mode append`, default) or completely replace it (`--prompt-mode replace`).

The value of `--system-prompt` and `--user-prompt` is a string or a path to a file. Placeholders are supported:

* ``{{source}}`, `{{target}}` - translation languages;
* ``{{glossary}}` - glossary in text form;
* ``{{context}}` - document context (title and file path);
* ``{{separator}}` - fragment separator;
* ``{{fragments}}`, `{{text}}` - fragments to translate (only in `--user-prompt`).

Example: require adherence to a corporate tone:

```bash
{{PROGRAM}} translate -i . -o ./translated --provider openai --source ru --target en \
  --system-prompt "Use formal tone. Address the reader as 'you'."
```

### Glossary {#glossary}

The model translates each segment separately and does not see how the same term is translated in a neighboring file or in a previous run. Because of this, "сборка" becomes `build` in one place, `assembly` in another, and the product name is unexpectedly translated. The glossary sets mandatory translations for terms and eliminates such inconsistency.

Typical cases:

* the product has established terminology, and the translation must match the interface and the rest of the documentation;
* a term, name, or identifier should not be translated at all — then `translatedText` repeats `sourceText`;
* the model systematically makes mistakes on a specific term.

The glossary is a YAML file with a single key `glossaryPairs`. This is a list of pairs "term in the original — required translation":

```yaml
glossaryPairs:
  - sourceText: оглавление
    translatedText: table of contents
  - sourceText: сборка
    translatedText: build
  - sourceText: Diplodoc
    translatedText: Diplodoc
```

#|
|| **Field** | **Description** ||
|| `sourceText` | The term in the source language, i.e., in the language from `--source` ||
|| `translatedText` | The translation that should appear in the result. Repeat the original spelling to keep the term unchanged ||
|#

There is one glossary per run, and it is not tied to a language pair, so for translating into multiple languages you need a separate file for each `--target`.

The path in `--glossary` is specified relative to `--input`:

```bash
{{PROGRAM}} translate -i . -o ./translated --provider openai --source ru --target en \
  --glossary glossary.yaml
```

In the [configuration file](#config), the path is specified relative to the `.yfm` itself:

```yaml
translate:
  glossary: glossary.yaml
```

If the file is missing, the command will fail with an error.

The pairs are inserted into the prompt of each request to the model as a list of the form `term → translation` (placeholder `not_var{{glossary}}`, see [Prompts](#prompts)). Three features follow from this:

* This is an instruction to the model, not a text replacement after translation. A term from the glossary is followed almost always, but there is no guarantee: the result should be checked by searching for the translation or by [quality assessment](#judge).
* The model handles word forms on its own; you do not need to add separate entries for cases and plural forms.
* The entire glossary goes into every request and consumes tokens on each batch. Keep only terms that are truly important or that the model confuses, not the entire product dictionary.

Changing the glossary invalidates the [translation cache](#cache): after editing the file, all segments are translated again.

## Translation cache {#cache}

The `--cache-dir` option enables a persistent cache: "segment — translation" pairs are saved to disk, and repeated runs send only new and changed segments to the model. The cache is flushed to disk after each processed file, so interrupting a run is safe — a restart will continue from the same point.

How the cache works:

* For each combination of "provider + model + language pair", a separate file `<provider>.<model>.<source>-<target>.json` is created. Changing `--model` does not overwrite the cache of another model, but it does not use it either.
* Changing prompts or the glossary automatically invalidates the cache: saved translations become outdated and are performed again. Updating the CLI with built-in prompts has the same effect.
* `--no-cache` disables the cache for one run without deleting saved translations.

It makes sense to commit the cache directory to the repository or keep it between CI runs - then, with regular translations, only the changed segments are paid for.

## Quality assessment {#judge}

The `--judge` option enables translation evaluation by a second model: each "original - translation" pair gets a score from 0 to 100. The mode is strictly optional - token consumption roughly doubles.

```bash
{{PROGRAM}} translate -i . -o ./translated --provider openai --source ru --target en \
  --cache-dir .translate-cache --judge --judge-model gpt-4o --judge-threshold 80
```

By default, the same model that performed the translation evaluates it. This is convenient for finding gross errors, but such self-assessment is inflated. For a fair comparison, use `--judge-model` with a model no weaker than the translating one: a weak judge will not notice the errors of a strong translator.

Results:

* Segments with a score below `--judge-threshold` are logged as `WARN` with the score and reason.
* A report `translate-quality.<language>.json` is written to the output:

  ```json
  {
    "model": "gpt-4o",
    "threshold": 80,
    "scored": 214,
    "averageScore": 93.4,
    "low": 2,
    "segments": [
      {
        "path": "ru/tools/docs/build.md",
        "source": "Сборка проекта выполняется командой...",
        "translation": "The project is built with...",
        "score": 55,
        "issue": "Omitted the second sentence"
      }
    ]
  }
  ```

  Only segments below the threshold are included in `segments`, sorted from worst to best.
* The final line in the log: `judge: 214 units scored, average score 93.4/100, 2 below threshold 80`. The first number is the count of evaluated segments, not a score.

The evaluation does not affect the translation result and does not interrupt the run: a failure in evaluating an individual batch is logged and skipped. In `--dry-run` mode, evaluation is not performed.

## How to read the log {#log}

#|
|| **Line** | **Meaning** ||
|| `TRANSLATE <file>` | The file has been taken into processing. If the line is absent, the file did not fall within the run's scope (filters `--files`, `--include`, `--exclude`, language) ||
|| `SKIPPED [reason] <file>` | The file was filtered out; the reason is in parentheses: `exclude`, `include`, `language` ||
|| `REQUEST <file> N units, ~X tokens` | A batch of N segments has been sent to the model. In `--dry-run` mode, there are no such lines ||
|| `TRANSLATED <file>` | The file has been translated and written to the output ||
|| `WARN ... Part is too big (~N tokens > M)` | The segment is larger than `--max-batch-tokens` and remained in the source language ||
|| `WARN ... Batch of N fragments failed ... retrying one-by-one` | The model's response could not be parsed into fragments; the batch is retried one segment at a time ||
|| `WARN <file> Translation quality N/100: ...` | The segment's score is below `--judge-threshold` ||
|| `ERR <file> ...` | The file was not translated; the run continues. Only an authorization error is fatal ||
|| `PROCESSED requests: R input-tokens: I output-tokens: O bytes: B cached-units: C` | Run summary: requests, tokens, text volume, and the number of segments from the cache ||
|| `PROCESSED judge: N units scored, average score A/100, M below threshold T` | Quality assessment summary ||
|#

## Troubleshooting {#troubleshooting}

### Error 429 (rate limit) {#throttling}

The CLI itself retries the request up to `--retry` times with an exponential pause and takes the `Retry-After` header into account. If API limits are still exceeded, restart the run with lower parallelism:

```bash
{{PROGRAM}} translate -i . -o ./translated --provider openai --source ru --target en \
  --cache-dir .translate-cache --max-concurrency 2
```

Already translated segments will be taken from the cache; only the remaining ones will go to the model.

### WARN Part is too big {#too-big}

The segment turned out to be larger than `--max-batch-tokens` and remained in the source language. Increase `--max-batch-tokens` (if necessary, together with `--max-output-tokens`) or split the text in the source into shorter paragraphs.

### Model response was truncated {#truncated}

Errors like `response was truncated` mean that the model ran out of the response limit. Increase `--max-output-tokens` or decrease `--max-batch-tokens`.

### File is not translated {#out-of-scope}

If an edit in a file does not make it into the translation, first check the run scope: the `--files` and `--include` options narrow the set of files, and changes outside this set do not get into the run — the log for such a file has no `TRANSLATE` line. This is not a cache issue.

Also keep in mind that the cache is maintained separately for each model: after changing `--model`, translations from another model are not reused.

### Source text in the output {#source-text-in-output}

* After `--dry-run` this is expected: files are assembled without calling the model, with the source text.
* An individual segment may match the original even in a regular run: the model deliberately does not translate text that is already in the target language, proper names, and non-text fragments. An empty model response is never accepted as a translation — in this case, the source text is preserved.

## Known limitations {#limitations}

* Pages with `::: page-constructor` blocks inside `.md` files are translated unreliably ([translation#273](https://github.com/diplodoc-platform/translation/issues/273)). For now, it is recommended to exclude them from the run via `--exclude`.
* The request path is fixed for each provider — a gateway with a non-standard API path cannot be connected.
* The model may corrupt inline markup within a segment (links, emphasis). There is no structural Markdown validation after translation — [quality assessment](#judge) helps find such cases.
