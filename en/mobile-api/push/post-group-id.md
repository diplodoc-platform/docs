# Unarchiving a group

Unarchives the group.

## Request format

```
POST {{ push-api-url }}/push/v1/management/group/{groupId}/restore
```

#|
|| `groupId` | {{ push-get-id }} ||
|#

## Sample request {#example}

{% list tabs %}

- cURL

   ```bash translate=no
   curl -X POST \
     'https://push.api.appmetrica.yandex.net/push/v1/management/group/XXXXXX/restore' \
     -H 'Authorization: OAuth <your_token>'
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../intro/authorization.md#get-oauth-token).

- HTTP

   ```http translate=no
   GET /push/v1/management/group/XXXXXX/restore HTTP/1.1
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
