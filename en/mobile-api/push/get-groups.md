# List of groups

Returns all groups for the specified application.

## Request format

```
GET {{ push-api-url }}/push/v1/management/groups
  ? app_id=<string>
```

#|
||`app_id`* | {{ app_id }} ||
|#

## Response format (JSON)

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

Reducing the speed allows you to decrease your handling service load.

{% endnote %}

||
|#

## Sample request {#example}

{% list tabs %}

- cURL

   ```bash translate=no
   curl -X GET \
     '{{ push-api-url }}/push/v1/management/groups?app_id=XXXXXX' \
     -H 'Authorization: OAuth <your_token>'
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../intro/authorization.md#get-oauth-token).

- HTTP

   ```http translate=no
   GET /push/v1/management/groups?app_id=XXXXXX HTTP/1.1
   Host: push.api.appmetrica.yandex.net
   Authorization: OAuth <your_token>
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../intro/authorization.md#get-oauth-token).

{% endlist %}

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
