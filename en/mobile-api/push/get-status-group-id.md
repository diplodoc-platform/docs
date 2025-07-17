# Checking the status of sending with clientTransferId

Returns the status of sending by using the ID that been set during the request in the group.

It allows you to check the status of sending using the specified ID set by a user, if you can not get the `transferId`.

## Request format

```
GET {{ push-api-url }}/push/v1/status/{groupId}/{clientTransferId}
```

#|
|| `groupId` | {{ push-get-id }} ||
|| `clientTransferId` | Sending ID, specified by the user. ||
|#

## Response format

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
|| `transfer.tag` | The sending [tag](*tag). ||
|| `transfer.creation_date` | {{ push-transfer-creation-date }} ||
|| `transfer.client_transfer_id` | Sending ID specified by the user in the body of the [POST /push/v1/send-batch](post-send-batch.md) request. ||
|#

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}

[*tag]: A tag is an arbitrary string that labels every sending performed by the API. You can label an arbitrary number of sendings by one tag. The report displays tag at the second level.
