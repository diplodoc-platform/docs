# Настройки YFM-проекта

В зависимости от используемого инструмента вы можете задать стандартные настройки YFM-проекта одним из способов:
* в [файле конфигурации](./project/config.md);
* в качестве параметра функции ([Transformer](./tools/transform/settings.md));
* через ключи запуска ([Builder](./tools/docs/settings.md)).

Название | Описание | Тип | Значение по умолчанию
:--- | :--- | :--- | :---
`vars` | Использование [переменных](./syntax/vars.md) | `Object` | `{}`
`allowHTML` | Разрешить использование HTML в разметке | `bool` | `false`
`linkify` | Преобразовывать ссылкоподобные строки в ссылки  | `bool` | `false`
`breaks` | Переносить строки по символу перевода каретки | `bool` | `true`
`conditionsInCode` | Выполнять условия в блоках кода | `bool` | `false`
`disableLiquid` | Отключить использование переменных | `bool` | `false`
`supportGithubAnchors` | Генерировать дополнительные [якоря](./syntax/base.md#headers), совместимые с GitHub | `bool` | `false`
`lang` | Язык локализации дефолтных текстов | `string` | `ru`
`needToSanitizeHtml` | Нужно ли санитайзить сгенерированный HTML | `bool` | `false`
`sanitizeOptions` | Конфигурация санитайзера | `Object` | `undefined`
`linkifyTlds` | Настройка tld для плагина linkify | `string \| string[]` | `undefined`