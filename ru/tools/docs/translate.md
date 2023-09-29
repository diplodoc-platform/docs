# Перевод

`yfm translate` переводит вашу документацию используя [Yandex Translator](https://cloud.yandex.ru/docs/translate/).

## Настройка

- получите OAUTH-токен как описано в [документации yandex.cloud](https://cloud.yandex.ru/docs/iam/concepts/authorization/oauth-token);

- положите его в `.ya_oauth_token` файл внутри домашней директории или укажите с помощью `YANDEX_OAUTH_TOKEN` переменной окружения;

- получите идентификатор каталога, на который у вашего аккаунта есть роль editor или выше, как описано в [документации yandex.cloud](https://cloud.yandex.ru/docs/resource-manager/operations/folder/get-id);

- в поле `yandexCloudTranslateFolderId` внутри `.yfm` файла конфигурации укажите значение идентификатора из предыдущего пункта;

- добавьте поле `yandexCloudTranslateGlossaryPairs` внутри `.yfm` файла конфигурации если вам требуется использование glossary-словаря:

```
# glossary example

yandexCloudTranslateGlossaryPairs:
    - { sourceText: InstreamAdBreakPositionType, translatedText: InstreamAdBreakPositionType }
```

_В результате выполнения **InstreamAdBreakPositionType** останется без изменения в тексте._

Теперь вы можете использовать `yfm` для перевода вашей документации.

## Опции

| Название опции    | Обязательная или нет | Значение         | Описание                                                                     |
| ----------------- | -------------------- | ---------------- | ---------------------------------------------------------------------------- |
| --input           | да                   | путь             | путь до входной документации                                                 |
| --output          | да                   | путь             | путь до выходной документации                                                |
| --source-language | да                   | код языка        | код языка в [формате ISO 639-1](https://en.wikipedia.org/wiki/ISO_639-1)     |
| --target-language | да                   | код языка        | код языка в [формате ISO 639-1](https://en.wikipedia.org/wiki/ISO_639-1)     |

## Использование

```
yfm translate --input input_folder --output output_folder --source-language ru --target-language en
```

_В результате выполнения ваша русская документация из **input_folder** будет переведена на английский и расположена в **output_folder**._
