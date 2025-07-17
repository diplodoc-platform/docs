# Проверка статуса отправки по transferId

Возвращает статус отправки по ее идентификатору.

## Формат запроса

```
GET {{ push-api-url }}/push/v1/status/{transferId}
```

#|
|| `transferId` | {{ push-transfer-id }} ||
|#

## Формат ответа

```json translate=no
{
  "transfer": {
    "id": 1,
    "group_id": 1,
    "status": "failed",
    "errors": [
      "Identifier type google_aid requires defined message for platform android"
    ],
    "tag": "string",
    "creation_date": "2017-08-28T17:30:15+03:00"
  }
}
```

#|
|| `transfer` | {{ push-transfer }} ||
|| `transfer.id` | {{ push-transfer-id }} ||
|| `transfer.group_id` | {{ push-get-id }} ||
|| `transfer.status` | {{ push-transfer-status }} ||
|| `transfer.errors` | {{ push-transfer-errors }} ||
|| `transfer.tag` | [Тег](*Тег) отправки. ||
|| `transfer.creation_date` | {{ push-transfer-creation-date }} ||
|#

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}

[*Тег]: Тег — это произвольная строка, маркирующая каждую отправку push-сообщений через API. Одним тегом может быть промаркировано произвольное количество отправок. В отчете отображается на втором уровне.
