# Дополнительные плагины

YFM использует [markdown-it](https://www.npmjs.com/package/markdown-it) в качестве парсера, поэтому вы можете подключить любой плагин из [списка плагинов для markdown-it](https://www.npmjs.com/search?q=keywords:markdown-it-plugin).

## Подключение {#require}

Перед подключением установите пакет с нужным плагином с помощью команды `npm i <имя_плагина>`. Например, чтобы установить [markdown-it-emoji](https://www.npmjs.com/package/markdown-it-emoji), выполните:

```shell
npm i markdown-it-emoji
```

{% list tabs %}

- Transformer

   {% note warning %}

   При переопределении параметра `plugins` необходимо заново подключать [плагины YFM](index.md). Для этого импортируйте их из пакета `@diplodoc/transform` и передайте в массиве плагинов.

   {% endnote %}

   1. Подключите плагин в своем коде, используя функцию `require()` или `import()`:
      ```javascript
      const plugin1 = require('<имя_плагина>');
      ```

   1. В параметре `plugins` добавьте новый плагин в массив:
      ```javascript
      const {result: {html, meta}, logs} = transform(content, {plugins: [<имя_плагина>]});
      ```

   **Пример:**
   ```javascript
   const fs = require('fs');
   const transform = require('@diplodoc/transform');
   const cut = require('@diplodoc/transform/lib/plugins/cut');
   const sup = require('@diplodoc/transform/lib/plugins/sup');
   const emoji = require('markdown-it-emoji');
   const content = fs.readFileSync(filePath, 'utf');
   const {result: {html, meta}, logs} = transform(content, {plugins: [cut, sup, emoji]});
   ```


- Builder

   1. Перенесите установленный плагин в папку `./plugins` в пакете `@diplodoc/cli`.

   {% note tip %}

   Чтобы не переносить необходимые плагины перед каждой сборкой, соберите собственный Builder:
   * Установите исходный код с [GitHub](https://github.com/yandex-cloud/yfm-docs).
   * Перенесите дополнительные плагины в папку `./plugins`.
   * Соберите Builder по [инструкции с GitHub](https://github.com/yandex-cloud/yfm-docs#installation-1).

   {% endnote %}

{% endlist %}

## Передача параметров {#options}

YFM применяет неизвестные параметры из объекта `options` ко всем плагинам, поэтому для передачи параметров добавьте их в объект `options`.
