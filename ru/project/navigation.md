# Расширенная навигация

Платформа поддерживает гибкую настройку верхней и нижней навигации («шапки» и «подвала») на странице.
Для этого используется пакет [page-constructor](https://gravity-ui.com/libraries/page-constructor). В [StoryBook](https://preview.gravity-ui.com/page-constructor/?path=/docs/navigation-navigation--docs) можно ознакомиться с примерами конфигурации навигации.

## Верхнее меню {#header}

Конфигурация верхнего меню добавляется в `toc.yaml` следующим образом:

```yaml
navigation:
  logo:
    url: 'https://diplodoc.com'
    urlTitle : "Текст всплывающей подсказки"
    dark:
      icon: 'https://storage.yandexcloud.net/diplodoc-www-assets/logo/ddos-logo-dark.svg'
      text: 'Diplodoc'
    light:
      icon: 'https://storage.yandexcloud.net/diplodoc-www-assets/navigation/diplodoc-logo.svg'
      text: 'Diplodoc'
  header:
    leftItems:
      - text: 'Relative Link'
        type: 'link'
        url: './ru/settings'
      - text: 'Absolute Link'
        type: 'link'
        url: 'https://diplodoc.com/docs/ru/project/'
    rightItems:
      - text: 'Other Link'
        type: 'link'
        url: 'ru/contribution'
      - type: controls
```

Для элементов списков `leftItems` и `rightItems` *первого уровня* можно использовать условия вывода `when` и подстановки переменных по аналогии с [разделами оглавления](toc.md#when).

### Поддерживаемые элементы {#item-types}

Тип элемента указывается в свойстве `type`.
На первом уровне доступны:

- `dropdown` — выпадающий список; свойство `items` может содержать элементы следующих типов:
  - `column` — группа элементов, отображаемых в одну колонку;
  - `section` — группа ссылок, объединённых заголовком, задаваемым через поле `title`;
  - `link` — ссылка;

    {% cut "Примеры конфигурации выпадающего списка" %}

    #|
    ||
    Простой список:
    |>
    ||
    ||

    ```yaml
    - type: dropdown
      text: 'Dropdown'
      items:
        - type: link
          text: 'Link 1'
          url: 'https://diplodoc.com'
        - type: link
          text: 'Link 2'
          url: 'https://diplodoc.com/docs/'
    ```

    |
    ||
    ||
    Несколько групп ссылок в одной колонке:
    |>
    ||
    ||

    ```yaml
    - type: dropdown
      text: 'Dropdown'
      items:
        - type: section
          title: 'Section 1'
          items:
            - type: link
              text: Link 1
              url: 'https://diplodoc.com'
            - type: link
              text: Link 2
              url: 'https://diplodoc.com/docs/'
        - type: section
          title: 'Section 2'
          items:
            - type: link
              text: 'Link 3'
              url: 'https://diplodoc.com/docs/'
    ```
    |
    ![Пример с группами ссылок в одной колонке](../../_images/header_sections.png){ height=200 }
    ||
    ||
    Группы ссылок в нескольких колонках:
    |>
    ||
    ||

    ```yaml wrap
    - type: dropdown
      text: 'Dropdown'
      items:
        - type: column
          items:
          - type: section
            title: 'Section 1'
            items:
              - type: link
                text: 'Link 1'
                url: 'https://diplodoc.com'
              - type: link
                text: 'Link 2'
                url: 'https://diplodoc.com/docs/'
          - type: section
            title: 'Section 2'
            items:
              - type: link
                text: 'Link 3'
                url: 'https://diplodoc.com/docs/'
        - type: column
          items:
          - type: section
            title: 'Section 3'
            items:
              - type: link
                text: 'Link 4'
                url: 'https://diplodoc.com/docs/ru/dev/'
              - type: link
                text: 'Link 5'
                url: 'https://diplodoc.com/docs/ru/quickstart/'
              - type: link
                text: 'Link 6'
                url: 'https://diplodoc.com/docs/ru/project/'
    ```

    |

    ![Пример с несколькими колонками](../../_images/header_columns.png){ height=200 }
    ||
    |#

    {% endcut %}

- `label` — статичный текст; свойство `theme` определяет стиль блока:

  ![Пример со стилями блоков статичного текста](../../_images/header_label_themes.png){ width=600 }

  {% cut "Пример конфигурации с блоками текста" %}

    ```yaml
    - type: label
      theme: normal
      text: normal

    - type: label
      theme: info
      text: info

    - type: label
      theme: danger
      text: danger

    - type: label
      theme: warning
      text: warning

    - type: label
      theme: success
      text: success

    - type: label
      theme: utility
      text: utility

    - type: label
      theme: unknown
      text: unknown

    - type: label
      theme: clear
      text: clear
    ```

    {% endcut %}

- `search` — точка размещения поля поиска в навигации.
  Если не указана вручную, то автоматически добавляется последним элементом в `rightItems`.

- `controls` — точка размещения настроек в навигации.
  Если не указана вручную, то автоматически добавляется последним элементом в `rightItems`.

На первом уровне, в выпадающих списках, группах элементов и ссылок доступен элемент:

- `link` — ссылка, свойство `url` содержит текст ссылки, `target: _blank` включает открытие ссылки в новой вкладке; относительные ссылки всегда рассчитываются от корня проекта, на каком бы уровне ни находился ##toc.yaml##.

## Нижнее меню {#footer}

Конфигурация нижнего меню добавляется в `toc.yaml` следующим образом:

```yaml
navigation:
  footer:
    copyright: 'Diplodoc'
    withDivider: true
    menuItems:
      - text: "GitHub"
        url: "https://github.com/diplodoc-platform"
      - text: "Для разработчиков"
        url: "https://diplodoc.com/docs/ru/dev/"
        target: '_self' # по умолчанию _blank
```

Основные параметры:
- `copyright` (строка) — текст копирайта для вывода,
- `menuItems` — список ссылок, в котором каждая ссылка описывается следующими полями:
  - `text` — заголовок,
  - `url` — ссылка,
  - `target` (необязательный параметр) — для открытия ссылки в той-же вкладке браузера можно указать в этом поле значение `_self`.

Полный список поддерживаемых параметров можно найти на [странице компонента Footer на сайте Gravity UI](https://gravity-ui.com/ru/components/navigation/footer).

> Смотри также: [Ajv схема файлов оглавления toc.yaml](https://raw.githubusercontent.com/diplodoc-platform/ajv/refs/heads/master/src/json/toc-schema.json)