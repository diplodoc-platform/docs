# External plugins

## Connection {#require}

The difference between external plugins and built-in ones is that before connecting them, they must first be installed (`npm install`), and then added to the plugins section `mdit-plugins`.

For external plugins, the plugin name is specified in the `plugins` field.

### Example of enabling {#example}

**Installing and configuring the [markdown-it-katex](https://www.npmjs.com/package/markdown-it-katex)** plugin.

The plugin allows displaying mathematical formulas.

1. Install the package with the plugin:

   ```bash
   npm install markdown-it-katex
   ```

2. Add the following configuration to the `.yfm` file:

   ```yaml
   extensions:
   - name: mdit-plugins
      plugins:
         - "markdown-it-katex"
   ```

**Usage:**

```markdown
$\sqrt{3x-1}+(1+x)^2$
```

**Result:**

$\sqrt{3x-1}+(1+x)^2$
