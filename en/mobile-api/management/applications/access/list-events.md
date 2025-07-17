# Event list

Returns a list of custom events

## Request format {#request-format}

```
GET {{ api-url }}/v1/traffic/sources/events?appId={id}
```
#|
|| `id` | App ID ||
|#

## Response format {#response-body}

```json translate=no
  "events_info": {
    "events": [
      "string",
      "string",
      "string"
    ],
    "totals": 3
```
#|
|| `events` | Event names. ||
|#

## Example {#example}

{% list tabs %}

- cURL

   ```bash translate=no
   curl -X GET \
     '{{ api-url }}/v1/traffic/sources/events?appId=1111' \
     -H 'Authorization: OAuth <your_token>'
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../../../intro/authorization.md#get-oauth-token).

- HTTP

   ```http translate=no
   GET /v1/traffic/sources/events?appId=1111 HTTP/1.1
   Host: api.appmetrica.yandex.ru
   Authorization: OAuth <your_token>
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../../../intro/authorization.md#get-oauth-token).

{% endlist %}

{{ feedback }}

<a href="../../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../../_includes/feedback-button.md) %}
