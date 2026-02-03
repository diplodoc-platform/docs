# Расширенная навигация

Платформа поддерживает гибкую настройку верхней навигации («шапки») на странице.
Для этого используется пакет [page-constructor](https://gravity-ui.com/libraries/page-constructor).

В [StoryBook](https://preview.gravity-ui.com/page-constructor/?path=/docs/navigation-navigation--docs) можно ознакомиться с примерами конфигурации навигации.

## Настройка

Блок конфигурации добавляется в `toc.yaml` следующим образом:

```yaml
title: Docs navigationExample
href: index.md
navigation:
  logo:
    url: 'https://diplodoc.com'
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

Относительные ссылки рассчитываются всегда от корня проекта, на каком бы уровне ни находился toc.yaml

Для элементов списков `leftItems` и `rightItems` можно использовать условия вывода `when` и подстановки переменных по аналогии с [разделами оглавления](toc.md#when).

## Специальные элементы

- `controls` — отвечает за позицию размещения поиска и настроек в навигации.
  Если не указан вручную, то автоматически добавляется последним элементом в `rightItems`.
