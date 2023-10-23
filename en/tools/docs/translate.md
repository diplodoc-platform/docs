# Translate

`yfm translate` translates your documentation using [Yandex Translator](https://cloud.yandex.com/en/docs/translate/)

## Setup

- get your OAUTH token as described in [yandex.cloud documentation](https://cloud.yandex.com/en/docs/iam/concepts/authorization/oauth-token)

- put it inside `.ya_oauth_token` file inside home folder or set it with `YANDEX_OAUTH_TOKEN` environment variable

- get the ID of any folder that your account is granted the editor role or higher for as described in [yandex.cloud documentation](https://cloud.yandex.com/en/docs/resource-manager/operations/folder/get-id)

- set `yandexCloudTranslateFolderId` inside `.yfm` config file to folder id you got from previous step

- set `yandexCloudTranslateGlossaryPairs` inside `.yfm` config file if you need to use glossary dictionary while translating (example below)

```
# glossary example

yandexCloudTranslateGlossaryPairs:
    - { sourceText: InstreamAdBreakPositionType, translatedText: InstreamAdBreakPositionType }
```

_This will make **InstreamAdBreakPositionType** stay without change in the target(translated) document_

Now you can use yfm cli to translate your documentation.

## Flags

| Option name       | required | value         | description                                                                  |
| ----------------- | -------- | ------------- | ---------------------------------------------------------------------------- |
| --input           | yes      | path          | source path to the documentation                                             |
| --output          | yes      | path          | target path to the translated documentation                                  |
| --source-language | yes      | language code | language code in [ISO 639-1 format](https://en.wikipedia.org/wiki/ISO_639-1) |
| --target-language | yes      | language code | language code in [ISO 639-1 format](https://en.wikipedia.org/wiki/ISO_639-1) |

## Usage

```
yfm translate --input input_folder --output output_folder --source-language ru --target-language en
```

_This will translate your russian documentation in the **input_folder** into english one putting it to **output_folder**_
