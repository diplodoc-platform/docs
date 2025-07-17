# Получение списка групп

Возвращает все группы для заданного приложения.

## Формат запроса

```
GET {{ push-api-url }}/push/v1/management/groups
  ? app_id=<string>
```

#|
||`app_id`* | {{ app_id }} ||
|#

## Формат ответа JSON

```json translate=no
{
  "groups" : [
    {
      "id": int,
      "app_id": int,
      "name": "string",
      "send_rate": int
    },
    ...
  ]
}
```

#|
|| `groups` | {{ push-get-groups }} ||
|| `groups.id` | {{ push-get-id }} ||
|| `groups.app_id` | {{ app_id }} ||
|| `groups.name` | {{ push-name }} ||
|| `groups.send_rate` | {{ push-send_rate }}

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
    '{{ push-api-url }}/push/v1/management/groups?app_id=XXXXXX' \
    -H 'Authorization: OAuth <your_token>'
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../intro/authorization.md#get-oauth-token).
 
- HTTP
 
  ```http translate=no
  GET /push/v1/management/groups?app_id=XXXXXX HTTP/1.1
  Host: push.api.appmetrica.yandex.net
  Authorization: OAuth <your_token>
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../intro/authorization.md#get-oauth-token).
 
{% endlist %}

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
