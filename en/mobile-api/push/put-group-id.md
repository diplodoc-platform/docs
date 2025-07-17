# Updating a group

Changes the name of the existing [group](*group).

## Request format

```
PUT {{ push-api-url }}/push/v1/management/group/{groupId}
```

#|
|| `groupId` | {{ push-get-id }} ||
|#

## Request body

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
|| `group.name`* | New name for the group. ||
|| `group.send_rate` | {{ push-send_rate }}

{% note info %}

Reducing the speed allows you to decrease your handling service load.

{% endnote %}

||
|#

## Response format {#response-format}

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

Reducing the speed allows you to decrease your handling service load.

{% endnote %}

||
|#

## Sample request {#example}

{% list tabs %}

- cURL

   ```bash translate=no
   curl -X POST \
     'https://push.api.appmetrica.yandex.net/push/v1/management/group/XXXXXX' \
     -H 'Content-Type: application/json' \
     -H 'Authorization: OAuth <your_token>'
     -d '{"group":{"name":"new_group_name"}}'
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../intro/authorization.md#get-oauth-token).

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

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../intro/authorization.md#get-oauth-token).

{% endlist %}

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}

[*group]: A group is a container for sending push messages. It allows grouping messages sendings in the [push campaign report](../../mobile-reports/push-campaign.md). The group can contain an arbitrary number of sendings. The push campaign report displays these groups at the first level along with push campaigns that are launched through the [web interface](../../push/marketing.md).
