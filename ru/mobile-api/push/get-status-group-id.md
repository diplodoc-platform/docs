# Проверка статуса отправки по clientTransferId

Возвращает статус отправки по идентификатору, который был указан при отправке сообщений в группе.

Позволяет проверить статус отправки с помощью заданного пользовательского идентификатора, если не удалось получить идентификатор `transferId`.

## Формат запроса

```
GET {{ push-api-url }}/push/v1/status/{groupId}/{clientTransferId}
```

#|
|| `groupId` | {{ push-get-id }} ||
|| `clientTransferId` | Идентификатор (ID) отправки, заданный пользователем. ||
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
    "creation_date": "2017-08-28T17:30:15+03:00",
    "client_transfer_id": 12345
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
|| `transfer.client_transfer_id` | Идентификатор (ID) отправки, заданный пользователем в теле запроса [POST /push/v1/send-batch](post-send-batch.md). ||
|#

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}

[*Тег]: Тег — это произвольная строка, маркирующая каждую отправку push-сообщений через API. Одним тегом может быть промаркировано произвольное количество отправок. В отчете отображается на втором уровне.
