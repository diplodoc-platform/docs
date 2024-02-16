# Разводящая страница

Для быстрой навигации по документу вы можете оформить корневую страницу в виде сетки с ссылками на основные разделы `index.yaml`.

Для небольших документов допустимо использовать упрощенный вариант - обычную страницу с описанием и ссылками `index.md`.

**Пример**: оформление разводящей страницы [документации сервиса Yandex Compute Cloud](https://cloud.yandex.ru/docs/compute/).

![Пример разводящей страницы](../_images/leading.png)

## Структура {#structure}

Стандартная структура файла разводящей страницы `index.yaml` имеет вид:

```yaml
title: Имя документа
description: Описание документа
meta:
  title: Метаданные
  noIndex: true
links:
- title: Первый раздел
  description: Описание первого раздела
  href: path/to/file.md
- title: Второй раздел
  description: Описание второго раздела
  href: path/to/file.md
```
* `title` — название документа. Отображается в оглавлении над списком всех разделов.
* `description` — описание документа.
* `meta`— [метаданные](../syntax/meta.md#meta).
* `links` — группирующий элемент. Для каждого раздела внутри него задается:
    * `title` — название раздела. Отображается как имя ссылки.
    * `description`— описание раздела.
    * `href` — относительный путь до файла.

## Условия видимости элементов {#when}

Отдельные разделы можно отображать или не отображать на разводящей странице в зависимости от значений [переменных](../syntax/vars.md). Для описания условий видимости используется параметр `when`.

Доступные операторы сравнения: `==`, `!=`, `<`, `>`, `<=`, `>=`.

```yaml
- title: Раздел с условным вхождением
  description: Описание раздела
  href: path/to/conditional/file.md
  when: version == 12
```

## Подстановки и условные операторы {#subtitudes}

Название и описание документа и ссылок поддерживают [подстановки](../syntax/vars#subtitudes) и [условные операторы](../syntax/vars#conditions).

```yaml
title: "not_var{{ title }}"
description: "{% if version == 10 %}not_var{{ description_legacy }}{% else %}not_var{{ description }}{% endif %}"
meta:
  title: "not_var{{ meta_title }}"
links:
- title: "not_var{{ link_title }}"
  description: "not_var{{ link_description }}"
  href: path/to/conditional/file.md
```
