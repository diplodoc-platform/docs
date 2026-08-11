# Plugins in Diplodoc

Diplodoc provides extended Markdown markup capabilities through a plugin system. Plugins allow you to extend the base syntax of [CommonMark Spec](https://spec.commonmark.org/) with unique markup elements and new features for your technical and project documentation.

Two types of plugins are available:

- [Installed plugins](installed.md) – built into Diplodoc. Some of them are enabled by default, while others can be enabled as needed.
- [External plugins](external.md) – can be downloaded, installed separately, and then connected to your project.
Diplodoc uses the [markdown-it](https://www.npmjs.com/package/markdown-it) parser, so you can connect any plugin from the [list of plugins for markdown-it](https://www.npmjs.com/search?q=keywords:markdown-it-plugin).

The difference between built-in and external plugins is that the former only need to be connected in the configuration, while the latter must first be installed via the package manager [npm](https://www.npmjs.com/package/npm) and then connected.

## How to connect plugins

In Diplodoc, one way to connect plugins is to use the built-in extension `mdit-plugins`, which is managed through the configuration file `.yfm` of your project. You just need to add or modify the `extensions` section as follows:

```yaml
extensions:
  - name: mdit-plugins # включаем встроенное в CLI расширение для подключения плагинов к markdown-it
    plugins:
      - "имя плагина" # если у плагина нет параметров - можно указать его имя строкой
      - name: "имя плагина" # если у плагина есть какие-то параметры или нужно что-то еще прописать, тогда используется полная форма передачи
        options: #...список опций плагина, которые у каждого могут отличаться...
```

If a plugin exports its code not via `export default`, but via a named export — for example, `export const somename = ...,` — specify the name of such an export in the `exportName` field. For example, for [markdown-it-emoji](https://www.npmjs.com/package/markdown-it-emoji) (which has several export variants: full, light, bare), you will need to explicitly specify the required export:


```yaml
extensions:
  - name: mdit-plugins
    plugins:
      - name: markdown-it-emoji
        exportName: full # Доступные значения: full, light, bare
```

Read more about connecting plugins in the sections:
- [Preinstalled plugins](installed.md)
- [External plugins](external.md)

