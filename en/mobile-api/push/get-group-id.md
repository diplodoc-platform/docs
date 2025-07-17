# Getting a group

Returns the group by its ID.

## Request format

```
GET {{ push-api-url }}/push/v1/management/group/{groupId}
```

#|
|| `groupId` | {{ push-get-id }} ||
|#

## Response format

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
   curl -X GET \
     {{ push-api-url }}/push/v1/management/group/XXXXXX \
     -H 'Authorization: OAuth <your_token>'
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../intro/authorization.md#get-oauth-token).

- HTTP

   ```http translate=no
   GET /push/v1/management/group/XXXXXX HTTP/1.1
   Host: api.appmetrica.yandex.ru
   Authorization: OAuth <your_token>
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../intro/authorization.md#get-oauth-token).

{% endlist %}

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
