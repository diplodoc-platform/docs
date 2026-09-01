---
keywords: ['translate', 'yandex translate', 'machine translation', 'i18n', 'l10n']
---
# Machine translation

Without the `--provider` option, the `{{PROGRAM}} translate` command translates documentation via [Yandex Translate](https://yandex.cloud/en/services/translate). This is the fastest translation method: it suits draft versions and regular language synchronization, but the result usually needs proofreading. For higher quality, use [AI translation](translate-ai.md) or [CAT tools](translate-xliff.md).

## Usage {#usage}

1. Get an authorization token: an [OAuth token](https://yandex.cloud/en/docs/iam/concepts/authorization/oauth-token), an [IAM token](https://yandex.cloud/en/docs/iam/concepts/authorization/iam-token), or a service account [API key](https://yandex.cloud/en/docs/iam/operations/api-key/create).
2. Find out the [folder ID](https://yandex.cloud/en/docs/resource-manager/operations/folder/get-id) for which your account has the `ai.translate.user` role or higher.
3. Estimate the translation volume without API requests:

   ```bash
   {{PROGRAM}} translate -i ./docs --source ru --target en --auth <token> --folder <folder-id> --dry-run
   ```

4. Run the translation:

   ```bash
   {{PROGRAM}} translate -i ./docs --source ru --target en --auth <token> --folder <folder-id>
   ```

Translated files appear in the target language folder - `docs/en` in the example above.

## Parameters {#options}

Common parameters (`--source`, `--target`, `--files`, `--include`, `--exclude`, `--dry-run`, and others) are described on the [Localization](translate.md#options) page. Below are the `yandex` provider parameters.

#|
|| **Parameter** | **Description** ||
|| `--auth` |
Authorization token: a value or a path to a file with the token. The type is detected by prefix: `y0_` - OAuth token, `t1.` - IAM token, `AQVN` - service account API key. Required
||
|| `--folder` |
[Folder ID](https://yandex.cloud/en/docs/resource-manager/operations/folder/get-id) for which your account has the `ai.translate.user` role or higher. Required
||
|| `--glossary` |
Path to a YAML file with a [glossary](https://yandex.cloud/en/docs/translate/concepts/glossary) - pairs of terms that must be translated in a fixed way
||
|#

## Limits {#limits}

Yandex Translate has [limits](https://yandex.cloud/en/docs/translate/concepts/limits) on the amount of translated text. The CLI reduces the volume on its own: documents are split into segments, and repeated segments are translated once.

If a limit is still exceeded, the command fails with the `TRANSLATE_LIMIT_EXCEED` error. In that case, retry later or narrow the file set with [filters](translate.md#options) - already translated files can be excluded.

The `--dry-run` option helps estimate the text volume before running.
