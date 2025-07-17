# Archiving a group

Archives a group.

Reports on archived groups remain available.

## Request format

```
DELETE {{ push-api-url }}/push/v1/management/group/{groupId}
```

#|
|| `groupId` | {{ push-get-id }} ||
|#

## Sample request

{% list tabs %}

- cURL

   ```bash translate=no
   curl -X DELETE \
     https://push.api.appmetrica.yandex.net/push/v1/management/group/XXXXXX \
     -H 'Authorization: OAuth <your_token>'
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../intro/authorization.md#get-oauth-token).

- HTTP

   ```http translate=no
   DELETE /push/v1/management/group/XXXXXX HTTP/1.1
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
