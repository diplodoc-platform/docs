# Configuration file

In the configuration file, you can specify:

* [Standard YFM settings](../settings.md).
* [YFM to HTML transformation settings](../tools/transform/settings.md).
* [Build settings](../tools/docs/settings.md).

By default, the `.yfm` file is located at the root of the document. When building, you can specify the path to another file using the [launch key](../tools/docs/settings.md) `--config`.

## Structure

The `.yfm` configuration file contains a list of all parameters in YAML format:

```yaml
parameter: value
parameter: value
```

* `parameter`: Name of the setting.
* `value`: Setting value.

