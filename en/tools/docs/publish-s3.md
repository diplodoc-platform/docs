# Uploading to S3

You can configure your build so that documentation is automatically published to [S3 storage](https://cloud.yandex.com/services/storage). To do this, use the `yfm publish` command.

You can set upload settings in one of the following ways (secret keys can only be passed as command-line arguments):
* via startup keys — the key name corresponds to the setting name;
* in the [configuration file](settings.md#config).

Secret keys are passed exclusively as arguments:

```bash
--access-key-id "XXXXXX"
--secret-access-key "XXXXX"
```

## `publish` section {#publish}

Parameter | Description | Default value
--- | --- | ---
`endpoint` | Endpoint for S3 storage. | `https://s3.amazonaws.com`
`bucket` | Bucket. | —
`prefix` | Prefix for file paths.<br><br>Optional parameter. Can be used to pass the build version so that each build is placed in a separate folder. | —
`region` | S3 storage region. | `eu-central-1`
`hidden` | List of glob patterns for files that should not be uploaded to the storage. | —

Example:

```yaml
publish:
 endpoint: "https://s3.example.com"
 bucket: "my-docs-bucket"
 prefix: "docs/"
 region: "eu-central-1"
 hidden:
   - ".yfm"
```

If you prefer not to store settings in `.yfm`, all parameters can be passed via the command:

```bash
yfm publish -i docs-html/ \
  --endpoint "" \
  --bucket "" \
  --prefix "" \
  --region "" \
  --access-key-id "" \
  --secret-access-key ""
```


{% note info %}

The `publish` command only uploads files to S3 — it does not build the documentation. If you want to upload already-built static files to S3, you need to build the documentation first:

```bash
yfm -i docs/ -o docs-html/
yfm publish -i docs-html/ ...
```

{% endnote %}
