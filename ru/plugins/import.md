# Дополнительные плагины

YFM использует [markdown-it](https://www.npmjs.com/package/markdown-it) в качестве парсера, поэтому вы можете подключить любой плагин из [списка плагинов для markdown-it](https://www.npmjs.com/search?q=keywords:markdown-it-plugin).

## Подключение {#require}

Перед подключением установите пакет с нужным плагином с помощью команды `npm i <имя_плагина>`. Например, чтобы установить [markdown-it-emoji](https://www.npmjs.com/package/markdown-it-emoji), выполните:

```shell
npm i markdown-it-emoji
```

{% list tabs %}

- Transformer

   {% note warning %}

   При переопределении параметра `plugins` необходимо заново подключать [плагины YFM](index.md). Для этого импортируйте их из пакета `@diplodoc/transform` и передайте в массиве плагинов.

   {% endnote %}

   1. Подключите плагин в своем коде с помощью функций `require()` или `import()`:
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

   1. Создайте файл `index.js` в папке `./plugins` в пакете `@diplodoc/cli` со следующим содержимым:
 
  ```javascript
   // node_modules/@diplodoc/cli/build/plugins/index.js
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
   * Установите исходный код с [GitHub](https://github.com/yandex-cloud/yfm-docs).
   * Перенесите дополнительные плагины в папку `./plugins`.
   * Соберите Builder по [инструкции с GitHub](https://github.com/yandex-cloud/yfm-docs#installation-1).

   {% endnote %}

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

2. Установите зависимости и соберите проект:
   ```bash
   npm i && npm run build
   ```

3. Перейдите в папку `build` и создайте файл `index.js` со следующим содержимым:
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

### Списки задач (чекбоксы)

Плагин для создания интерактивных списков задач уже входит в состав Diplodoc, но требует явного подключения.

**Подключение:**

{% list tabs %}

- Transformer

   ```javascript
   const checkbox = require('@diplodoc/transform/lib/plugins/checkbox');
   
   const {result: {html, meta}, logs} = transform(content, {
     plugins: [checkbox],
     // Параметры плагина
     divClass: 'checkbox',    // CSS-класс для div
     idPrefix: 'checkbox'     // Префикс для id чекбокса
   });
   ```

- Builder

   ```javascript
   // build/plugins/index.js
   const checkbox = require('@diplodoc/transform/lib/plugins/checkbox');
   
   module.exports = [
     checkbox
   ];
   ```

{% endlist %}

**Использование:**

```markdown
- [x] ~~Написать пресс-релиз~~
- [ ] Обновить веб-сайт  
- [ ] Связаться со СМИ
```

**Параметры:**
- `divClass` — CSS-класс для `div`, который оборачивает чекбокс (по умолчанию: `checkbox`)
- `idPrefix` — префикс для id чекбокса (по умолчанию: `checkbox`)

### Эмодзи

Плагин [markdown-it-emoji](https://www.npmjs.com/package/markdown-it-emoji) добавляет поддержку эмодзи.

**Установка:**
```bash
npm i markdown-it-emoji
```

**Подключение:**
```javascript
const emoji = require('markdown-it-emoji');

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
:smile: :heart: :thumbsup:
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
Inline формула: $E = mc^2$

Блочная формула:
$$
\int_{-\infty}^{\infty} e^{-x^2} dx = \sqrt{\pi}
$$
```

## Создание собственного Builder

Для удобства работы с дополнительными плагинами рекомендуется создать собственную сборку Builder:

1. **Склонируйте репозиторий:**
   ```bash
   git clone https://github.com/diplodoc-platform/cli.git
   cd cli
   ```

2. **Установите зависимости:**
   ```bash
   npm install
   ```

3. **Добавьте нужные плагины:**
   ```bash
   npm install markdown-it-plantuml markdown-it-emoji markdown-it-katex
   ```

4. **Настройте плагины в `build/plugins/index.js`:**
   ```javascript
   const plantuml = require('markdown-it-plantuml');
   const emoji = require('markdown-it-emoji');
   const katex = require('markdown-it-katex');
   const checkbox = require('@diplodoc/transform/lib/plugins/checkbox');
   
   module.exports = [
     plantuml,
     emoji,
     katex,
     checkbox
   ];
   ```

5. **Соберите проект:**
   ```bash
   npm run build
   ```

Теперь у вас есть собственная версия Diplodoc CLI со всеми необходимыми плагинами.

## Полезные ссылки

- [Список всех плагинов markdown-it](https://www.npmjs.com/search?q=keywords:markdown-it-plugin)
- [Документация markdown-it](https://markdown-it.github.io/)
- [Создание собственных плагинов](https://github.com/markdown-it/markdown-it/tree/master/docs)
- [Предустановленные плагины Diplodoc](index.md)
- [Расширения Diplodoc](extensions.md)
