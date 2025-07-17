# Downloading data

{{ data }}

**Quotas**
:   No more than ten parallel downloads are permitted.

**Compressed data**
:   We recommend passing the `Accept-Encoding: gzip` request header to speed up the network transfer for large files compressed using `gzip`.

## Request format {#request-format}

```
GET {{ api-url }}/datastream/v1/application/{id}/data
  ? data_type=<string>
  & stream_window_timestamp=<string>
```
#|
|| `id` | App ID ||
|| `data_type`* | Specifies which stream data to load.

Possible values:
- `event`
- `installation`
- `session_start`
- `session_end`
- `push_token`
- `crash`
- `error`
- `click`
- `revenue`
- `ecommerce`
- `ad_revenue`
- `attributed_event`
- `deeplink`
   ||
   || `stream_window_timestamp`* | Unix timestamp in seconds pointing to the data window. You can find out which data windows are available using the [Stream status](status.md) operation. ||
   |#

## Response codes {#codes}

| Response code | Description |
| ----- | ----- |
| 404 | No data. The value of the `stream_window_timestamp` parameter is currently missing in the response to the [Stream status](status.md) request. |
| 500 | Error on the AppMetrica server side. A repeat request won't be successful. Contact [support](../../../troubleshooting/feedback-new.md). |
| 503 | Error on the AppMetrica server side. A repeat request may be successful. |

## Example {#example}

Request:

```bash translate=no
curl -X GET '{{ api-url }}/datastream/v1/application/1111/data?data_type=event&stream_window_timestamp=1670202610' \
-o events1670202610.csv \
-H 'Authorization: OAuth oauth_token' \
-H 'Accept-Encoding: gzip'
```

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
