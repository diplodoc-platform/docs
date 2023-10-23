# Uploading to S3

You can configure the building so that the documentation is automatically uploaded to [S3 storage](https://cloud.yandex.com/services/storage). To do this, when executing the `yfm` command, specify the `--publish` startup key.

You can set layout settings in one of the following ways:

* Using startup keys: The name of the key corresponds to the name of the setting.
* In a [configuration file](../../project/config.md).

## Uploading settings {#settings}

| Configuration | Description |
| --- | --- |
| `storageEndpoint` | Endpoint for S3 storage. |
| `storageBucket` | Bucket. |
| `storageKeyId` | Authorization key ID.</br></br>Can be set in the `YFM_STORAGE_KEY_ID` environment variable. |
| `storageSecretKey` | Authorization key.</br></br>Can be set in the `YFM_STORAGE_SECRET_KEY` environment variable. |
| `storagePrefix` | Prefix for file paths.</br></br>Optional parameter. Can be used to pass the build version, so each build is placed in a separate folder. |

