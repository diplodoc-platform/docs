# Page constructor

Page constructor (далее -- PC) - это библиотека семейства [Gravity UI](https://gravity-ui.com/) для рендеринга веб-страниц на основе данных представленных в YAML формате.
При создании страниц используется компонентный подход: страница строится с использованием набора готовых блоков, которые можно размещать в любом порядке. Каждый блок имеет определенный тип и набор параметров входных данных.
Формат входных данных и список доступных блоков можно посмотреть в [документации библиотеки](https://preview.gravity-ui.com/page-constructor/?path=/docs/documentation-blocks--docs).

Примеры оформление страниц с помощью PC [\[1\]](./pc-example1.yaml) [\[2\]](./pc-example2.yaml)

## Структура {#structure}

Стандартная структура конфигурации PC страницы хранится в `.yaml` формате и имеет вид:

```yaml
blocks:
  - type: 'header-block'
    width: 's'
    offset: 'default'
    title: 'Diplodoc'
    resetPaddings: true
    verticalOffset: 'l'
    description: 'Платформа для создания технической документации в концепции Docs as Сode с открытым исходным кодом. Простое и удобное решение для развёртывания документации больших и маленьких команд.'
    background:
      image:
        mobile: 'https://storage.yandexcloud.net/diplodoc-www-assets/pages/index-diplodoc/ddos-index-cover-mini.png'
        desktop: '_assets/test-move.png'
      color: '#C6FE4D'
      fullWidth: false
    buttons:
      - text: 'Начать'
        primary: true
        theme: 'dark'
        size: 'promo'
        url: '/quickstart'
      - text: 'GitHub'
        primary: true
        theme: 'outlined'
        size: 'promo'
        url: 'https://github.com/diplodoc-platform'
```

Описание полей для каждого блока можно посмотреть в [документации](https://preview.gravity-ui.com/page-constructor/?path=/story/blocks-header--docs&viewMode=docs).
