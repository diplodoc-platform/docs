# Список событий

Возвращает список пользовательских событий.

## Формат запроса {#request-format}

```
GET {{ api-url }}/v1/traffic/sources/events?appId={id}
```
#|
|| `id` | Идентификатор приложения. ||
|#

## Формат ответа {#response-body}

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
|| `events` | Наименования событий. ||
|#

## Пример {#example}

{% list tabs %}

- cURL

  ```bash translate=no
  curl -X GET \
    '{{ api-url }}/v1/traffic/sources/events?appId=1111' \
    -H 'Authorization: OAuth <your_token>'
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../../../intro/authorization.md#get-oauth-token).

- HTTP

  ```http translate=no
  GET /v1/traffic/sources/events?appId=1111 HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Authorization: OAuth <your_token>
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../../../intro/authorization.md#get-oauth-token).

{% endlist %}

{{ feedback }}

<a href="../../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../../_includes/feedback-button.md) %}
