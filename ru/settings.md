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
`lang` | Язык локализации дефолтных текстов. 
Для [следующих языков](https://github.com/diplodoc-platform/client/blob/34a5139620874627cfdebe9be74902cf9d3961b1/src/constants.ts#L15) контент будет отображаться в формате RTL (right-to-left) | `string` | `ru`
`needToSanitizeHtml` | Нужно ли санитайзить сгенерированный HTML | `bool` | `true`
`sanitizeOptions` | Конфигурация санитайзера | `Object` | `undefined`
`linkifyTlds` | Настройка tld для плагина linkify | `string \| string[]` | `undefined`
`analytics` | Конфигурация для модуля аналитки | `Object` | `undefined`
`analytics.gtm` | Настройки Google Tag Manager аналитики | `Object` | `undefined`
`analytics.gtm.id` | Идентификатор Google Tag Manager в формате GTM-* | `string` | `undefined`
`analytics.gtm.mode` | Тип уведомления перед отправкой событий `base` или `notification`  | `string` | `base`
