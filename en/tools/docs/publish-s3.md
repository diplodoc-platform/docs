# Deploying to S3

To publish documentation to [S3 storage](https://cloud.yandex.ru/services/storage), use the `yfm publish` command.

{% note warning %}

The command does not build the documentation — it must be built with `yfm build` before publishing.

```bash
# Building documentation
yfm build -i docs/ -o docs-html/

# Publishing to S3
yfm publish -i docs-html/ \
  --access-key-id "YCAJE..." \
  --secret-access-key "YCO..."
```

{% endnote %}

## Arguments of the publish command

#|
|| **Argument** | **Description** | **Default value** ||
|| `--input` (`-i`){{required}} | Path to the directory with the built documentation | — ||
|| `--endpoint` | Endpoint for the S3 storage | `https://s3.amazonaws.com` ||
|| `--bucket`{{required}} | Bucket name | — ||
|| `--prefix` |
Prefix for file paths.
\
Can be used to pass a build version, so each build is placed in a separate folder.
| — ||
|| `--region` | S3 storage region | `eu-central-1` ||
|| `--hidden` | List of glob patterns for files that should not be uploaded to the storage | — ||
|| `--access-key-id`{{required}} | S3 access key ID | — ||
|| `--secret-access-key`{{required}} | S3 secret access key | — ||
|#

It is recommended to move some parameters to the [configuration file](../../settings.md). This avoids repeating them every time the command is run. Sensitive data (`--access-key-id`, `--secret-access-key`) is passed **only via arguments**.

## Examples

### The publish section in the configuration file **.yfm**

```yaml
publish:
  endpoint: "https://storage.yandexcloud.net"
  bucket: "my-docs-bucket"
  prefix: "docs/"
  region: "eu-central-1"
  hidden:
    - ".yfm"
```

### Command-line arguments

```bash
yfm publish -i docs-html/ \
  --endpoint "https://storage.yandexcloud.net" \
  --bucket "my-docs-bucket" \
  --prefix "docs/v1.0/" \
  --region "eu-central-1" \
  --access-key-id "YCAJE..." \
  --secret-access-key "YCO..."
```