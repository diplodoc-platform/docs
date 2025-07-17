# Availability of the Logs API

Checks the availability of the [Logs API](../logs/about.md).

## Request format {#request-format}

```
GET /management/v1/logsapi/status
```

## Response format {#response-body}

```json translate=no
{
  "status": "string"
}
```
#|
|| `status` | Availability of the Logs API. 

Possible values:

- `enabled` — Logs API available. 
- `disabled` — Logs API unavailable. ||
|#

## Example {#example}

{% list tabs %}

- cURL

  ```bash translate=no
  curl -X GET \
    '{{ api-url }}/management/v1/logsapi/status' \
    -H 'Authorization: OAuth <your_token>'
  ```

  where `<your_token>` is an OAuth token that can be obtained using [instructions](../intro/authorization.md#get-oauth-token).

- HTTP

  ```http translate=no
  GET /management/v1/logsapi/status HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Authorization: OAuth <your_token>
  ```

  where `<your_token>` is an OAuth token that can be obtained using [instructions](../intro/authorization.md#get-oauth-token).

{% endlist %}

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
