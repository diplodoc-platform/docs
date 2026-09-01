---
keywords: ['translate', 'yandex translate', 'машинный перевод', 'i18n', 'l10n', 'перевод']
tags:
    - Локализация
---
# Машинный перевод

Без опции `--provider` команда `{{PROGRAM}} translate` переводит документацию через [Yandex Translate](https://yandex.cloud/ru/services/translate). Это самый быстрый способ перевода: он подходит для черновых версий и регулярной синхронизации языков, но результат обычно требует вычитки. Для более качественного перевода используйте [AI-перевод](translate-ai.md) или [CAT-системы](translate-xliff.md).

## Использование {#usage}

1. Получите токен авторизации: [OAuth-токен](https://yandex.cloud/ru/docs/iam/concepts/authorization/oauth-token), [IAM-токен](https://yandex.cloud/ru/docs/iam/concepts/authorization/iam-token) или [API-ключ](https://yandex.cloud/ru/docs/iam/operations/api-key/create) сервисного аккаунта.
2. Узнайте [идентификатор каталога](https://yandex.cloud/ru/docs/resource-manager/operations/folder/get-id), для которого у аккаунта есть роль `ai.translate.user` или выше.
3. Оцените объем перевода без запросов к API:

   ```bash
   {{PROGRAM}} translate -i ./docs --source ru --target en --auth <токен> --folder <идентификатор> --dry-run
   ```

4. Запустите перевод:

   ```bash
   {{PROGRAM}} translate -i ./docs --source ru --target en --auth <токен> --folder <идентификатор>
   ```

Переведенные файлы появятся в папке целевого языка - в примере выше это `docs/en`.

## Параметры {#options}

Общие параметры (`--source`, `--target`, `--files`, `--include`, `--exclude`, `--dry-run` и другие) описаны на странице [Локализация](translate.md#options). Ниже - параметры провайдера `yandex`.

#|
|| **Параметр** | **Описание** ||
|| `--auth` |
Токен авторизации: значение или путь к файлу с токеном. Тип определяется по префиксу: `y0_` - OAuth-токен, `t1.` - IAM-токен, `AQVN` - API-ключ сервисного аккаунта. Обязательный
||
|| `--folder` |
[Идентификатор каталога](https://yandex.cloud/ru/docs/resource-manager/operations/folder/get-id), для которого у аккаунта есть роль `ai.translate.user` или выше. Обязательный
||
|| `--glossary` |
Путь к YAML-файлу с [глоссарием](https://yandex.cloud/ru/docs/translate/concepts/glossary) - парами терминов, которые нужно переводить фиксированно
||
|#

## Лимиты {#limits}

У Yandex Translate есть [ограничения](https://yandex.cloud/ru/docs/translate/concepts/limits) на объем переводимого текста. CLI сокращает объем сам: документы разбиваются на сегменты, повторяющиеся сегменты переводятся один раз.

Если лимит все же превышен, команда завершается ошибкой `TRANSLATE_LIMIT_EXCEED`. В этом случае повторите запуск позже или сузьте набор файлов [фильтрами](translate.md#options) - уже переведенные файлы можно исключить.

Оценить объем текста до запуска помогает опция `--dry-run`.
