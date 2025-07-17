# Remove app

Deletes the specified application.

## Request format {#request}

```
DELETE {{ api-url }}/management/v1/application/{id}
```

#|
|| `id` | App ID ||
|#

## Sample request {#example}

{% list tabs %}

- cURL

   ```bash translate=no
   curl -X DELETE \
     '{{ api-url }}/management/v1/application/1111' \
     -H 'Authorization: OAuth <your_token>'
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../../intro/authorization.md#get-oauth-token).

- HTTP

   ```http translate=no
   DELETE /management/v1/application/1111 HTTP/1.1
   Host: api.appmetrica.yandex.ru
   Authorization: OAuth <your_token>
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../../intro/authorization.md#get-oauth-token).

{% endlist %}

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
