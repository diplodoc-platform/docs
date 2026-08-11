# Preinstalled plugins

## Connection {#require}

For preinstalled plugins, instead of the npm package name, the `plugins` field specifies the path to the file inside Diplodoc CLI. For example, for checkboxes (task list):

```yaml
extensions:
  - name: mdit-plugins
    plugins:
      - '@diplodoc/transform/lib/plugins/checkbox'
```

### Example of enabling {#example}

**Installing and configuring the `Tasks list` plugin (task lists)**.

The plugin for creating interactive task lists is included in Diplodoc but requires explicit connection.

**Connection:**

Add the following configuration to the `.yfm` file:

```yaml
extensions:
  - name: mdit-plugins
    plugins:
    - '@diplodoc/transform/lib/plugins/checkbox'
```

**Usage:**

After connecting, you can create interactive task lists:

```markdown
- [x] ~~Написать пресс-релиз~~
- [ ] Обновить веб-сайт  
- [ ] Связаться со СМИ
```

**Result:**

- [x] ~~Write a press release~~
- [ ] Update the website  
- [ ] Contact the media
