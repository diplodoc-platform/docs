# Расширенная навигация

Платформа поддерживает гибкую настройку верхней навигации ("шапки") на странице.
Для этого используется пакет [page-constructor](https://gravity-ui.com/libraries/page-constructor).

В [StoryBook](https://preview.gravity-ui.com/page-constructor/?path=/docs/navigation-navigation--docs) можно ознакомиться с примерами конфигурации навигации.

## Настройка

{% note warning %}

Стоит учитывать, что, при использовании расширенной навигации, вся развертка страницы переходит в режим page-constructor.
Т.е. будут отличаться отсуты контента от краев экрана.

Так же в этом режиме игнорируются любые настройки навигации из `.yfm` файла.

{% endnote %}

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

Относительные ссылки расчитываются всегда от корня проекта, на каком бы уровне не находился toc.yaml

## Специальные элементы

- `controls` - отвечает за позицию размещения поиска и настроек в навигации.
  Если не указан вручную, то автоматически добавляется последним элементов в `rightItems`.
