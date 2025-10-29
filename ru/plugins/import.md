# Дополнительные плагины

YFM использует [markdown-it](https://www.npmjs.com/package/markdown-it) в качестве парсера, поэтому вы можете подключить любой плагин из [списка плагинов для markdown-it](https://www.npmjs.com/search?q=keywords:markdown-it-plugin).

## Подключение {#require}

Перед подключением установите пакет с нужным плагином с помощью команды `npm i <имя_плагина>`. Например, чтобы установить [markdown-it-emoji](https://www.npmjs.com/package/markdown-it-emoji), выполните:

```shell
npm i markdown-it-emoji
```

{% list tabs %}

- Builder
  
  1. Склонируйте репозиторий CLI:

      ```bash
      git clone https://github.com/diplodoc-platform/cli.git
      ```

  1. Установите зависимости и соберите проект:

      ```bash
      npm i && npm run build
      ```

   1. Перейдите в папку `node_modules/@diplodoc/cli/build/plugins` и создайте файл `index.js` со следующим содержимым:
 
      ```javascript
         const emojiPlugin = require('markdown-it-emoji');

         // Плагины необходимо экспортировать в виде массива функций, а не как отдельные именованные экспорты.
         // Экспортируем массив функций плагинов
         module.exports = [
         emojiPlugin.full, // Используем конкретную версию плагина
         // Добавьте другие плагины при необходимости
         ];
         ```


   {% note tip %}

   Чтобы не переносить необходимые плагины перед каждой сборкой, соберите собственный Builder:
   - Установите исходный код с [GitHub](https://github.com/yandex-cloud/yfm-docs).
   - Перенесите дополнительные плагины в папку `./plugins`.
   - Соберите Builder по [инструкции с GitHub](https://github.com/yandex-cloud/yfm-docs#installation-1).

   {% endnote %}

- Transformer

   {% note warning %}

   При переопределении параметра `plugins` необходимо заново подключать [плагины YFM](index.md). Для этого импортируйте их из пакета `@diplodoc/transform` и передайте в массиве плагинов.

   {% endnote %}

   1. Подключите плагин в своем коде с помощью функций `require()` или `import()`:

      ```javascript
      const plugin1 = require('markdown-it-emoji');
      ```

   2. В параметре `plugins` добавьте новый плагин в массив:
   
      ```javascript
      const {result: {html, meta}, logs} = transform(content, {plugins: [markdown-it-emoji]});
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

{% endlist %}

## Передача параметров {#options}

YFM применяет неизвестные параметры из объекта `options` ко всем плагинам, поэтому для передачи параметров добавьте их в объект `options`.

## Примеры подключения популярных плагинов

### PlantUML диаграммы

Плагин [markdown-it-plantuml](https://www.npmjs.com/package/markdown-it-plantuml) позволяет создавать UML-диаграммы прямо в Markdown.

**Установка и настройка:**

1. Склонируйте репозиторий CLI:

   ```bash
   git clone https://github.com/diplodoc-platform/cli.git
   ```

1. Установите зависимости и соберите проект:

   ```bash
   npm i && npm run build
   ```
1. Установите пакет с плагином:

    ```bash
      npm install markdown-it-plantuml --save
      ```

1. Перейдите в папку `build` и создайте файл `index.js` со следующим содержимым:

   ```javascript
   const plantuml = require('markdown-it-plantuml');
   
   module.exports = [
     plantuml
   ];
   ```

**Использование:**

После настройки вы можете добавлять PlantUML диаграммы в любую Markdown страницу:

```markdown
@startuml
Alice -> Bob: Authentication Request
Bob --> Alice: Authentication Response
Alice -> Bob: Another authentication Request
Alice <-- Bob: another authentication Response
@enduml
```

**Результат:**

@startuml
Alice -> Bob: Authentication Request
Bob --> Alice: Authentication Response
Alice -> Bob: Another authentication Request
Alice <-- Bob: another authentication Response
@enduml

### Эмодзи

Плагин [markdown-it-emoji](https://www.npmjs.com/package/markdown-it-emoji) добавляет поддержку синтаксиса emoji и смайликов.

**Установка:**

```bash
npm install i markdown-it-emoji
```

**Подключение:**

```javascript
import { full as emoji } from 'markdown-it-emoji'
import markdownit from 'markdown-it'

const md = markdownit().use(emoji/* , options */);

// Для Transformer
const {result: {html, meta}, logs} = transform(content, {
  plugins: [emoji]
});

// Для Builder (в build/plugins/index.js)
module.exports = [
  emoji
];
```

**Использование:**

```markdown
:smile: :heart: :thumbsup: :satellite:
```

### Математические формулы

Плагин [markdown-it-katex](https://www.npmjs.com/package/markdown-it-katex) позволяет отображать математические формулы.

**Установка:**

```bash
npm i markdown-it-katex
```

**Подключение:**

```javascript
const katex = require('markdown-it-katex');

const {result: {html, meta}, logs} = transform(content, {
  plugins: [katex]
});
```

**Использование:**

```markdown
$\sqrt{3x-1}+(1+x)^2$
```
