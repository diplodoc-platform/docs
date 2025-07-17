# Deleting an app's certificate fingerprint

{{ fingerptints-delete }}

## Request format {#request-format}

```
DELETE {{ api-url }}/management/v1/application/{id}/events_certs_fingerprints/android/{fingerprint_id}
```

#|
|| `id` | App ID. ||
|| `fingerprint_id` | Certificate fingerprint ID. You can get a list of IDs using the [Information about app certificate fingerprints](fingerprints-android-get.md) operation. ||
|#

## Response format {#output-structure}

```json translate=no
{
    "success": boolean
}
```

#|
|| `success` |  Operation status. ||
|#

## Example {#example}

Request:

```bash translate=no
curl -X DELETE '{{ api-url }}/management/v1/application/8888/events_certs_fingerprints/android/24' \
-H 'Authorization: OAuth oauth_token'
```

Response:

```json translate=no
{
    "success": true
}
```

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
