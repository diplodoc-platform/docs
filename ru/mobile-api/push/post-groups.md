# Создание группы

Создает [группу](*группу) для отправок push-сообщений заданному приложению.

## Формат запроса {#request-format}

```
POST {{ push-api-url }}/push/v1/management/groups
```

## Тело запроса

```json translate=no
{
  "group": {
    "app_id": int,
    "name": "string",
    "send_rate": int
  }
}
```

#|
|| `group` | {{ push-group }} ||
|| `group.app_id`* | {{ push-app_id }} ||
|| `group.name`* | {{ push-name }} ||
|| `group.send_rate` | {{ push-send_rate }} ||
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
|| `group` | {{ push-group }} ||
|| `group.id` | {{ push-id }} ||
|| `group.app_id` | {{ push-app_id }} ||
|| `group.name` | {{ push-name }} ||
|| `group.send_rate` | {{ push-send_rate }} ||
|#

## Пример запроса

> ```bash translate=no
> curl -X POST \
>   {{ push-api-url }}/push/v1/management/groups \
>   -H 'Authorization: OAuth AQAAAAAR62cMAAQgnh4fTgjnrEH...' \
>   -H 'Content-Type: application/json' \
>   -d '{
>   "group": {
>     "app_id": XXXXXX,
>     "name": "group-name",
>     "send_rate": 200
>   }
> }'
> ```

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}

[*группу]: Группа — это контейнер для отправки push-сообщений. Позволяет группировать отправки в [отчете по push-кампаниям](../../mobile-reports/push-campaign.md). Группа может содержать произвольное количество отправок. В отчете отображается на первом уровне вместе с push-кампаниями, запущенными через [веб-интерфейс](../../push/marketing.md).
