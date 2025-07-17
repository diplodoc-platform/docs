# Доступность Logs API

Проверяет доступность [Logs API](../logs/about.md).

## Формат запроса {#request-format}

```
GET /management/v1/logsapi/status
```

## Формат ответа {#response-body}

```json translate=no
{
  "status": "string"
}
```
#|
|| `status` | Доступность Logs API. 

Возможные значения:

- `enabled` — Logs API доступен.
- `disabled` — Logs API недоступен. ||
|#

## Пример {#example}

{% list tabs %}

- cURL

  ```bash translate=no
  curl -X GET \
    '{{ api-url }}/management/v1/logsapi/status' \
    -H 'Authorization: OAuth <your_token>'
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../intro/authorization.md#get-oauth-token).

- HTTP

  ```http translate=no
  GET /management/v1/logsapi/status HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Authorization: OAuth <your_token>
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../intro/authorization.md#get-oauth-token).

{% endlist %}

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
