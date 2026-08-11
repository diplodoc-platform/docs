# Inserting arbitrary content (includers)

You can include arbitrary content in the documentation via includers — a special mechanism for extending a documentation project with additional files at the build stage.

## Connection {#config}

Includers are connected in the `includers` field of a table of contents item with the `include` parameter:

```yaml
items:
  - name: <item-name>
    include:
      path: <path-where-to-include>
      includers:
        - name: <name-of-the-first-includer>
          <includer-parameter>: <includer-parameter-value>
        - name: <name-of-the-second-includer>
        - name: <name-of-the-third-includer>
      mode: link
```

1. The `include` object must have a `path` field with the path **from which** the content will be included.

2. The `mode` parameter must have the value `link` or be omitted; `link` is the default value.

3. The `includers` parameter must contain a list of _includer objects_ that will be called sequentially in the specified order. 

4. Each _includer object_ must contain a `name` field with the includer type:

    - `generic` — [inserting arbitrary Markdown files into the project structure](generic.md);

    - `openapi` — [auto-generating articles based on OpenAPI specifications](openapi.md);

    - `unarchive` — [unpacking a tar file before running other includers](unarchive.md).

5. Different includer types may have their own parameters, which are specified in the _includer object_.
