# Метаданные статьи

Метаданные — элементы разметки, которые не отображаются в собранном файле. Они используются для хранения в исходном тексте настроек конкретной статьи, информации для SEO или авторов документа.

В md-файлы метаданные добляются в формате YAML в начало файла для настроек отображения страницы (эта часть файла называется ##frontmatter##).

В yaml-файлы c [Page constructor страницами](./page-constructor.md) и [разводящими](./leading-page.md) — прямо в корневой объект.

Пример:

```yaml
---
title: Заголовок
description: Описание
---

# Заголовок статьи

Текст статьи ......
```

Поддерживаемые параметры:

#|
|| **Название** | **Описание** | **Тип и значение по умолчанию** ||
|| `alternate` | Ссылки на другие языковые версии страницы.

Каждая ссылка прописывается в `<link rel="alternate" hreflang="..." href="..."/>`.

На этапе сборки массив автоматически дополняется совпадающими ссылками из других языков документации.
 | `string[]`

— ||
|| `canonical` | Каноническая ссылка для индексации страницы.

Прописывается в `<link rel="canonical" href="..."/>`.

Если явно не указана, то на этапе сборки автоматически прописывается путь до страницы.
 | `string`

— ||
|| `copyright` | Указание владельца контента страницы.

Прописывается в `<meta name="copyright" content="..."/>`. | `string`

— ||
|| `description` {#description} | Мета-описание страницы.

Прописывается в `<meta name="description" content="..."/>` и в [##llms.txt##](../guides/llms.md). | `string`

— ||
|| `keywords` | Список ключевых слов страницы для поисковых роботов.

Прописывается в `<meta name="keywords" content="key1,key2,..."/>`. | `string[]`

— ||
|| `interface` {#interface} | Секция с настройками отображения интерфейса. Переопределяет установленные в [одноимённой секции .yfm](../settings.md#interface) настройки для текущей страницы.

{% cut "Пример с отключением оглавления на странице" %}

```yaml
---
interface:
  toc: false
---
```

{% endcut %}

| `object`

— ||
|| `metadata` | Список с описанием произвольных метаполей статьи.

Список содержит объекты вида:

```yaml
metadata:
  - name: name 1
    content: content 1
  - http-equiv: http-equiv 2
    content: content 2
  - property: property 3
    content: content 3
...
```

на основе которых формируется набор тегов:

```html
<meta name="name 1" content="content 1"/>
<meta http-equiv="http-equiv 2" content="content 2">
<meta property="property 3" content="content 3">
```

Примеры полей и их возможных значений можно найти в статье об [организации контентной аналитики](../guides/content-analytics.md#meta-information-example).

| `object[]`

— ||
|| `resources` | Секция для управления ресурсами страницы.

Переопределяет настройки ##resources##, установленные в [секции resources .yfm](../settings.md#resources).

{% note warning %}

Доступно только расширение списка значений [##csp##](../settings.md#resources-csp).

{% endnote %}

| `object`

— ||
|| `title` | Мета-заголовок страницы.

Прописывается в `<meta name="title" content="..."/>`. | `string`

— ||

|#

> Смотри также: [Ajv схема метаданных статьи](https://raw.githubusercontent.com/diplodoc-platform/ajv/refs/heads/master/src/json/frontmatter-schema.json)
