# Обновление группы

Изменяет имя существующей [группы](*группы).

## Формат запроса

```
PUT {{ push-api-url }}/push/v1/management/group/{groupId}
```

#|
|| `groupId` | {{ push-get-id }} ||
|#

## Тело запроса

```json translate=no
{
  "group": {
    "name": "string",
    "send_rate": int
  }
}
```
#|
|| `group` | {{ push-get-groups }} ||
|| `group.name`* | Новое имя группы. ||
|| `group.send_rate` | {{ push-send_rate }}

{% note info %}

Уменьшение скорости отправки позволяет снизить нагрузку на ваш сервис.

{% endnote %}

||
|#

## Формат ответа {#response-format}

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
  curl -X POST \
    'https://push.api.appmetrica.yandex.net/push/v1/management/group/XXXXXX' \
    -H 'Content-Type: application/json' \
    -H 'Authorization: OAuth <your_token>'
    -d '{"group":{"name":"new_group_name"}}'
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../intro/authorization.md#get-oauth-token).
 
- HTTP
   
  ```http translate=no
  GET /push/v1/management/group/XXXXXX HTTP/1.1
  Host: push.api.appmetrica.yandex.net
  Content-Type: application/json
  Authorization: OAuth <your_token>
   
  {
    "group": {
      "name": "new_group_name"
    }
  }
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../intro/authorization.md#get-oauth-token).
 
{% endlist %}

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}

[*группы]: Группа — это контейнер для отправки push-сообщений. Позволяет группировать отправки в [отчете по push-кампаниям](../../mobile-reports/push-campaign.md). Группа может содержать произвольное количество отправок. В отчете отображается на первом уровне вместе с push-кампаниями, запущенными через [веб-интерфейс](../../push/marketing.md).
