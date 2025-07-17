# Список партнеров

Возвращает список партнеров.

## Формат запроса {#request-format}

```
GET {{ api-url }}/management/v1/tracking/partners
```

## Формат ответа {#response-body}

```json translate=no
  "partners" : {
    "total_rows" : 375,
    "partners" : [ {
      "id" : int,
      "name" : "string",
      "icon_url" : "string",
      "website_url" : "string",
      "campaigns_count" : int,
      "ownership" : "string",
      "type" : "string"
    },
  ...
    ]
  }
```
#|
|| `id` | Идентификатор партнера. ||
|| `name` | Название партнера. ||
|| `icon_url` | Ссылка на иконку. ||
|| `website_url` | Сайт партнера. ||
|| `campaigns_count` | Количество активных трекеров. ||
|| `ownership` | Уровень доступа. 

Возможные значения:
- `common` — общий.
- `own` — владелец партнера.
- `guest` — гостевой доступ. ||
|| `type` | Признак партнера. ||
|#

## Пример {#example}

{% list tabs %}

- cURL

  ```bash translate=no
  curl -X GET \
    '{{ api-url }}/management/v1/tracking/partners' \
    -H 'Authorization: OAuth <your_token>'
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../../../intro/authorization.md#get-oauth-token).
  

- HTTP

  ```http translate=no
  GET /management/v1/tracking/partners HTTP/1.1
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
