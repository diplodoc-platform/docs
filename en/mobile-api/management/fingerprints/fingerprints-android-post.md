# Uploading an app's certificate fingerprint

{{ fingerptints-post }}

## Request format {#request-format}

```
POST {{ api-url }}/management/v1/application/{id}/events_certs_fingerprints/android/add
```

#|
|| `id` | App ID. ||
|#

### Request body format {#structure-in}

```json translate=no
{
    "data": {
        "fingerprint": string
    }
}
```

#|
|| `data` | Object with data. ||
|| `data.fingerprint` | {{ fingerprint }} ||
|#

## Response format {#output-structure}

```json translate=no
{
  "id": int,
  "fingerprint": string
}
```

#|
|| `id` | {{ fingerprints-id }} ||
|| `fingerprint` | {{ fingerprint }} ||
|#

## Example {#example}

Request:
```bash translate=no
curl -X POST '{{ api-url }}/management/v1/application/1111/events_certs_fingerprints/android/add' \
-H 'Content-Type: application/json' \
-H 'Authorization: OAuth oauth_token' \
-d '{
      "data": {
        "fingerprint": "A7:89:E5:05:C8:17:A1:XXXXX"
      }
    }'
```

Response:

```json translate=no
{
  "id": 24,
  "fingerprint": "A7:89:E5:05:C8:17:A1:XXXXX"
}
```

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
