# Предустановленные плагины

Diplodoc поставляется с набором предустановленных плагинов, которые расширяют базовый синтаксис [CommonMark Spec](https://spec.commonmark.org/) дополнительными возможностями и уникальными элементами разметки.

## Как работают плагины

Плагины — это модули [markdown-it](https://www.npmjs.com/package/markdown-it), которые обрабатывают и преобразуют разметку Markdown. Каждый плагин отвечает за определённый синтаксис или функциональность.

## Подключение и настройка

### Подключение отдельных плагинов

Большинство предустановленных плагинов включены по умолчанию. Однако некоторые плагины требуют явного подключения:

```javascript
const transform = require('@diplodoc/transform');

// Подключение плагина списка задач
const checkbox = require('@diplodoc/transform/lib/plugins/checkbox');

const {result: {html, meta}, logs} = transform(content, {
  plugins: [checkbox]
});
```

### Настройка параметров плагинов

Параметры плагинов передаются через объект `options`:

```javascript
const {result: {html, meta}, logs} = transform(content, {
  plugins: [checkbox],
  // Параметры применяются ко всем подключённым плагинам
  extractTitle: true,        // для плагина Anchors
  supportGithubAnchors: true // для плагина Anchors
});
```

{% note warning %}

При переопределении параметра `plugins` необходимо заново подключать все нужные плагины YFM. Порядок добавления плагинов важен — указывайте полный набор плагинов в правильной последовательности.

{% endnote %}

## Список предустановленных плагинов

{% include [plugins.md](../_includes/plugins.md) %}

## Примеры использования

### Настройка якорей заголовков

```javascript
const transform = require('@diplodoc/transform');

const result = transform(content, {
  extractTitle: true,           // Учитывать заголовок первого уровня
  supportGithubAnchors: true,   // Генерировать якоря, совместимые с GitHub
  disableCommonAnchors: false   // Включить стандартные якоря
});
```

### Настройка заметок

```javascript
const result = transform(content, {
  lang: 'en' // Язык для отображения типа заметки (по умолчанию 'ru')
});
```

### Настройка списка задач

```javascript
const checkbox = require('@diplodoc/transform/lib/plugins/checkbox');

const result = transform(content, {
  plugins: [checkbox],
  divClass: 'custom-checkbox',  // CSS-класс для div, оборачивающего чекбокс
  idPrefix: 'task'              // Префикс для id чекбокса
});
```

## Дополнительные возможности

Помимо предустановленных плагинов, вы можете:

- [Подключить дополнительные плагины](import.md) из экосистемы markdown-it
- [Создать собственные расширения](extensions.md) для специфических потребностей
- Использовать [встроенные расширения](extensions.md) как примеры для разработки

## Отключение плагинов

Чтобы отключить предустановленный плагин, исключите его из списка при явном указании плагинов:

```javascript
// Подключаем только нужные плагины
const cut = require('@diplodoc/transform/lib/plugins/cut');
const sup = require('@diplodoc/transform/lib/plugins/sup');

const result = transform(content, {
  plugins: [cut, sup] // Другие предустановленные плагины будут отключены
});
