# Publishing to S3

To publish documentation to [S3 storage](https://cloud.yandex.ru/services/storage), use the `yfm publish` command.

{% note warning %}

The command does not build documentation — you need to build it with `yfm build` before publishing.

```bash
# Build documentation
yfm build -i docs/ -o docs-html/

# Publish to S3
yfm publish -i docs-html/ \
  --bucket "my-docs-bucket" \
  --access-key-id "YCAJE..." \
  --secret-access-key "YCO..."
```

{% endnote %}

## publish command arguments

#|
|| **Argument** | **Description** | **Default** ||
|| `--input` (`-i`){{required}} | Path to the directory with the built documentation | — ||
|| `--endpoint` | S3 storage endpoint | `https://s3.amazonaws.com` ||
|| `--bucket`{{required}} | Bucket name | — ||
|| `--prefix` |
File path prefix.
\
Can be used to pass the build version, so each build is stored in a separate folder.
| — ||
|| `--region` | S3 storage region | `eu-central-1` ||
|| `--hidden` | List of glob patterns for files that should not be uploaded to the storage | — ||
|| `--access-key-id`{{required}} | S3 access key ID | — ||
|| `--secret-access-key`{{required}} | S3 secret access key | — ||
|#

Some parameters are recommended to be specified in the [configuration file](../../settings.md). This avoids repeating them on every command run. Sensitive data (`--access-key-id`, `--secret-access-key`) should be passed **only as command-line arguments**.

## Examples

### publish section in the **.yfm** configuration file

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
