# Page constructor

Page constructor (hereinafter – PC) is a library of the [Gravity UI](https://gravity-ui.com/) family for rendering web pages based on data presented in YAML format.
When creating pages, a component-based approach is used: the page is built using a set of ready-made blocks that can be placed in any order. Each block has a specific type and a set of input data parameters.
The input data format and the list of available blocks can be found in the [library documentation](https://preview.gravity-ui.com/page-constructor/?path=/docs/documentation-blocks--docs). In the PC storybook, there is a [convenient sandbox](https://preview.gravity-ui.com/page-constructor/1116/?path=/story/editor-main--default) where you can first try out all the blocks and assemble a page, and then copy the ready-made config into your documentation.

Examples of page design using PC [\[1\]](./pc-example1.yaml) [\[2\]](./pc-example2.yaml) [\[3\]](./pc-example3.yaml)

## Usage methods

Page constructor can be used in two ways:

1. **Separate YAML files** — creating full-fledged pages using YAML configuration.
2. **Embedding blocks** — adding individual Page constructor blocks directly into markdown documentation.

## Adding Page constructor pages { #page }

The standard structure of a PC page configuration is stored in the `.yaml` format and looks like this:

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
        theme: 'dark'
        size: 'promo'
        url: '/quickstart'
      - text: 'GitHub'
        theme: 'outlined'
        size: 'promo'
        url: 'https://github.com/diplodoc-platform'
```

Field descriptions for each block can be found in the [documentation](https://preview.gravity-ui.com/page-constructor/?path=/docs/documentation-blocks--docs).

## Adding Page constructor blocks to Markdown { #block }

You can embed individual Page constructor blocks directly into markdown documentation. This allows you to combine regular markdown content with interactive Page constructor blocks on a single page.

### Syntax { #syntax }

To add a Page constructor block to markdown, use the `page-constructor` directive:

```yaml
::: page-constructor
blocks:
  - type: 'header-block'
    title: 'Заголовок'
    description: 'Описание'
:::
```

Important: the `blocks:` property is required. Inside the directive, the same YAML format is used as when creating separate YAML files. Basic YFM syntax is supported in text fields (headings, descriptions, texts).

### Usage examples

You can use Page constructor to add a single block or multiple blocks at once.

{% cut "Block markup" %}

```yaml
::: page-constructor
blocks:
  - type: 'filter-block'
    centered: true
    title:
      text: 'Нам доверяют'
    tags:
      - id: 'one'
        label: 'DoubleСloud'
      - id: 'two'
        label: 'Yandex Support'
      - id: 'three'
        label: 'Yandex Cloud'
      - id: 'four'
        label: 'YDB'
      - id: 'five'
        label: 'CatBoost'
    colSizes:
      all: 12
      xl: 12
      md: 12
      sm: 12
    indent:
      top: s
    items:
      - tags:
          - 'one'
        card:
          type: 'layout-item'
          media:
            image:
              src: 'https://storage.yandexcloud.net/cloud-www-assets/pages/index-diplodoc/diplodoc-tab-1.png'
              disableCompress: true
          border: true
          content:
            links:
              - text: 'Посмотреть документацию'
                url: 'https://double.cloud/docs/en/'
                theme: 'normal'
                arrow: true
                color: #54BA7E

      - tags:
          - 'two'
        card:
          type: 'layout-item'
          media:
            image:
              src: 'https://storage.yandexcloud.net/diplodoc-www-assets/pages/index-diplodoc/ddos-index-trust-support.png'
              disableCompress: true
          border: true
          content:
            links:
              - text: 'Посмотреть документацию'
                url: 'https://yandex.ru/support2/audience/ru/'
                theme: 'normal'
                arrow: true
                color: #54BA7E
      - tags:
          - 'three'
        card:
          type: 'layout-item'
          media:
            image:
              src: 'https://storage.yandexcloud.net/cloud-www-assets/pages/index-diplodoc/ddos-index-trust-yandex-cloud.png'
              disableCompress: true
          border: true
          content:
            links:
              - text: 'Посмотреть документацию'
                url: 'https://cloud.yandex.ru/docs/compute/'
                theme: 'normal'
                arrow: true
                color: #54BA7E
      - tags:
          - 'four'
        card:
          type: 'layout-item'
          media:
            image:
              src: 'https://storage.yandexcloud.net/cloud-www-assets/pages/index-diplodoc/ddos-index-trust-ydb.png'
              disableCompress: true
          border: true
          content:
            links:
              - text: 'Посмотреть документацию'
                url: 'https://ydb.tech/en/docs/'
                theme: 'normal'
                arrow: true
                color: #54BA7E
      - tags:
          - 'five'
        card:
          type: 'layout-item'
          media:
            image:
              src: 'https://storage.yandexcloud.net/cloud-www-assets/pages/index-diplodoc/ddos-index-trust-yandex-cat.png'
              disableCompress: true
          border: true
          content:
            links:
              - text: 'Посмотреть документацию'
                url: 'https://catboost.ai/en/docs/'
                theme: 'normal'
                arrow: true
                color: #54BA7E
  - type: 'card-layout-block'
    title: 'Как это работает?'
    colSizes:
      all: 12
      md: 4
      sm: 6
    indent:
      top: sm
    children:
      - type: 'layout-item'
        content:
          title: 'Архитектура'
          text: 'Платформа Diplodoc имеет клиент-серверную архитектуру: серверная часть состоит из компонентов на Node.js, которые генерируют и отображают документационные проекты. Такая архитектура обеспечивает надёжность и горизонтальное масштабирование в случае необходимости.  '
        media:
          image:
            src: 'https://storage.yandexcloud.net/diplodoc-www-assets/pages/index-diplodoc/ddos-index-item-01-01.png'
            disableCompress: true
        fullScreen: true
        border: true
      - type: 'layout-item'
        content:
          title: 'Интеграция с GitHub'
          text: 'Платформа Diplodoc имеет сквозную интеграцию с GitHub для обеспечения простого и стабильного механизма сборки и развёртывания документационных проектов. GitHub используется как хранилище исходного кода для документов и исполнения пайплайна проекта.'
        media:
          image:
            src: 'https://storage.yandexcloud.net/diplodoc-www-assets/pages/index-diplodoc/ddos-index-item-01-02.png'
            disableCompress: true
        fullScreen: true
        border: true
      - type: 'layout-item'
        content:
          title: 'Развёртывание'
          text: 'Компании – пользователи сервиса Diplodoc используют встроенные механизмы выкладки документационного проекта с последующей их индексацией и отслеживанием версий. Документы могут обновляться как в автоматическом, так и в полуавтоматическом режиме с привлечением администратора со стороны пользователя.'
        media:
          image:
            src: 'https://storage.yandexcloud.net/diplodoc-www-assets/pages/index-diplodoc/ddos-index-item-01-03.png'
            disableCompress: true
        fullScreen: true
        border: true
:::
```

{% endcut %}

Display result:

::: page-constructor
blocks:
  - type: 'filter-block'
    centered: true
    title:
      text: 'Trusted by'
    tags:
      - id: 'one'
        label: 'DoubleCloud'
      - id: 'two'
        label: 'Yandex Support'
      - id: 'three'
        label: 'Yandex Cloud'
      - id: 'four'
        label: 'YDB'
      - id: 'five'
        label: 'CatBoost'
    colSizes:
      all: 12
      xl: 12
      md: 12
      sm: 12
    indent:
      top: s
    items:
      - tags:
          - 'one'
        card:
          type: 'layout-item'
          media:
            image:
              src: 'https://storage.yandexcloud.net/cloud-www-assets/pages/index-diplodoc/diplodoc-tab-1.png'
              disableCompress: true
          border: true
          content:
            links:
              - text: 'Посмотреть документацию'
                url: 'https://double.cloud/docs/en/'
                theme: 'normal'
                arrow: true
                color: #54BA7E

      - tags:
          - 'two'
        card:
          type: 'layout-item'
          media:
            image:
              src: 'https://storage.yandexcloud.net/diplodoc-www-assets/pages/index-diplodoc/ddos-index-trust-support.png'
              disableCompress: true
          border: true
          content:
            links:
              - text: 'Посмотреть документацию'
                url: 'https://yandex.ru/support2/audience/ru/'
                theme: 'normal'
                arrow: true
                color: #54BA7E
      - tags:
          - 'three'
        card:
          type: 'layout-item'
          media:
            image:
              src: 'https://storage.yandexcloud.net/cloud-www-assets/pages/index-diplodoc/ddos-index-trust-yandex-cloud.png'
              disableCompress: true
          border: true
          content:
            links:
              - text: 'Посмотреть документацию'
                url: 'https://cloud.yandex.ru/docs/compute/'
                theme: 'normal'
                arrow: true
                color: #54BA7E
      - tags:
          - 'four'
        card:
          type: 'layout-item'
          media:
            image:
              src: 'https://storage.yandexcloud.net/cloud-www-assets/pages/index-diplodoc/ddos-index-trust-ydb.png'
              disableCompress: true
          border: true
          content:
            links:
              - text: 'Посмотреть документацию'
                url: 'https://ydb.tech/en/docs/'
                theme: 'normal'
                arrow: true
                color: #54BA7E
      - tags:
          - 'five'
        card:
          type: 'layout-item'
          media:
            image:
              src: 'https://storage.yandexcloud.net/cloud-www-assets/pages/index-diplodoc/ddos-index-trust-yandex-cat.png'
              disableCompress: true
          border: true
          content:
            links:
              - text: 'Посмотреть документацию'
                url: 'https://catboost.ai/en/docs/'
                theme: 'normal'
                arrow: true
                color: #54BA7E
  - type: 'card-layout-block'
    title: 'How does it work?'
    colSizes:
      all: 12
      md: 4
      sm: 6
    indent:
      top: sm
    children:
      - type: 'layout-item'
        content:
          title: 'Архитектура'
          text: 'Платформа Diplodoc имеет клиент-серверную архитектуру: серверная часть состоит из компонентов на Node.js, которые генерируют и отображают документационные проекты. Такая архитектура обеспечивает надёжность и горизонтальное масштабирование в случае необходимости.  '
        media:
          image:
            src: 'https://storage.yandexcloud.net/diplodoc-www-assets/pages/index-diplodoc/ddos-index-item-01-01.png'
            disableCompress: true
        fullScreen: true
        border: true
      - type: 'layout-item'
        content:
          title: 'Интеграция с GitHub'
          text: 'Платформа Diplodoc имеет сквозную интеграцию с GitHub для обеспечения простого и стабильного механизма сборки и развёртывания документационных проектов. GitHub используется как хранилище исходного кода для документов и исполнения пайплайна проекта.'
        media:
          image:
            src: 'https://storage.yandexcloud.net/diplodoc-www-assets/pages/index-diplodoc/ddos-index-item-01-02.png'
            disableCompress: true
        fullScreen: true
        border: true
      - type: 'layout-item'
        content:
          title: 'Развёртывание'
          text: 'Компании – пользователи сервиса Diplodoc используют встроенные механизмы выкладки документационного проекта с последующей их индексацией и отслеживанием версий. Документы могут обновляться как в автоматическом, так и в полуавтоматическом режиме с привлечением администратора со стороны пользователя.'
        media:
          image:
            src: 'https://storage.yandexcloud.net/diplodoc-www-assets/pages/index-diplodoc/ddos-index-item-01-03.png'
            disableCompress: true
        fullScreen: true
        border: true
:::

