# Получение группы

Возвращает группу по ее идентификатору.

## Формат запроса

```
GET {{ push-api-url }}/push/v1/management/group/{groupId}
```

#|
|| `groupId` | {{ push-get-id }} ||
|#

## Формат ответа

```json translate=no
{
  "group": {
    "id": int,
    "app_id": int,
    "name": "string",
    "send_rate": int
  }
}
```

#|
|| `group` | {{ push-get-groups }} ||
|| `group.id` | {{ push-get-id }} ||
|| `group.app_id` | {{ app_id }} ||
|| `group.name` | {{ push-name }} ||
|| `group.send_rate` | {{ push-send_rate }}

{% note info %}

Уменьшение скорости отправки позволяет снизить нагрузку на ваш сервис.

{% endnote %}

||
|#

## Пример запроса {#example}

{% list tabs %}

- cURL

  ```bash translate=no
  curl -X GET \
    {{ push-api-url }}/push/v1/management/group/XXXXXX \
    -H 'Authorization: OAuth <your_token>'
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../intro/authorization.md#get-oauth-token).
  
- HTTP
  
  ```http translate=no
  GET /push/v1/management/group/XXXXXX HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Authorization: OAuth <your_token>
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../intro/authorization.md#get-oauth-token).

{% endlist %}

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
