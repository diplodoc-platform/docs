# Page constructor

Page constructor (hereinafter PC) is a library of the [Gravity UI](https://gravity-ui.com/) family for rendering web pages based on data presented in YAML format.
When creating pages, component-based approach is used: a page is built using a set of ready-made blocks that can be placed in any order. Each block has a certain type and set of input data parameters.
For the format of input data and list of available blocks, see the [documentation](https://preview.gravity-ui.com/page-constructor/?path=/docs/documentation-blocks--docs).

Examples of page design using PC [\[1\]](./pc-example1.yaml) [\[2\]](./pc-example2.yaml)

## Structure {#structure}

The standard PC page configuration structure is stored in `.yaml` format and looks like:

```yaml
blocks:
  - type: 'header-block'
    width: 's'
    offset: 'default'
    title: 'Diplodoc'
    resetPaddings: true
    verticalOffset: 'l'
    description: 'A platform with open-source code for creating technical documentation based on the concept of Docs as Code. A simple and convenient document management solution for large and small teams.'
    background:
      image:
        mobile: 'https://storage.yandexcloud.net/diplodoc-www-assets/pages/index-diplodoc/ddos-index-cover-mini.png'
        desktop: '../../_images/mountain.jpg'
      color: '#C6FE4D'
      fullWidth: false
    buttons:
      - text: 'Quickstart'
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

A description of the fields for each block can be found in [documentation](https://preview.gravity-ui.com/page-constructor/?path=/story/blocks-header--docs&viewMode=docs).
