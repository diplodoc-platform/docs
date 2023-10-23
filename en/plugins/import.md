# Adding additional plugins

YFM uses [markdown-it](https://www.npmjs.com/package/markdown-it) as a parser, so you can add any plugin from the [markdown-it plugin list](https://www.npmjs.com/search?q=keywords:markdown-it-plugin).

## Adding plugins {#require}

Before adding a plugin, install the package that contains it using the `npm i <plug_name>` command. For example, to install [markdown-it-emoji](https://www.npmjs.com/package/markdown-it-emoji), run:

```shell
npm i markdown-it-emoji
```

{% list tabs %}

- Transformer

   1. Add the plugin in your code using the `require()` or `import()` function:

      ```javascript
      const plugin1 = require('<plug_name>');
      ```

   1. For the `plugins` parameter, add a new plugin to the array:

      ```javascript
      const {result: {html, meta}, logs} = transform(content, {plugins: [<plug_name>]});
      ```

   **Example:**

   ```javascript
   const fs = require('fs');
   const transform = require('@doc-tools/transform');
   const cut = require('@doc-tools/transform/lib/plugins/cut');
   const sup = require('@doc-tools/transform/lib/plugins/sup');
   const emoji = require('markdown-it-emoji');
   const content = fs.readFileSync(filePath, 'utf');
   const {result: {html, meta}, logs} = transform(content, {plugins: [cut, sup, emoji]});
   ```

   {% note warning %}

   When overriding the `plugins` parameter, you must reconnect [YFM plugins](index.md). To do this, import them from the `@doc-tools/transform` package and pass them in the plugin array.

   {% endnote %}

- Builder
   1. Move the installed plugin to the `./plugins` folder in the `@doc-tools/docs` package.

   {% note tip %}

   If you don't want to transfer the necessary plugins before each build, build your own Builder:
   * Install the source code with [GitHub](https://github.com/yandex-cloud/yfm-docs).
   * Move the additional plugins to the `./plugins` folder.
   * Build the Builder by following the [GitHub instructions](https://github.com/yandex-cloud/yfm-docs#installation-1).

   {% endnote %}

{% endlist %}

## Passing parameters {#options}

YFM applies unknown parameters from the `options` object to all plugins, so to pass parameters, add them to the `options` object.

