# Deleting access

Deletes previously granted access permissions.

## Request format {#request-format}

```
DELETE {{ api-url }}/management/v1/application/{id}/grant?user_login={login}
```
#|
|| `id` | App ID ||
|| `login` | Yandex email address (login) of the user.

{% note alert %}

If you omit the `user_login` parameter, the access is revoked from the user making the request, that is, the user unsubscribes from the app.

{% endnote %}

||
|#

## Example {#example}

{% list tabs %}

- cURL

   ```bash translate=no
   curl -X DELETE \
     '{{ api-url }}/management/v1/application/1111/grant?user_login=user123' \
     -H 'Authorization: OAuth <your_token>'
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../../../intro/authorization.md#get-oauth-token).

- HTTP

   ```http translate=no
   GET /management/v1/application/1111/grant?user_login=user123' HTTP/1.1
   Host: api.appmetrica.yandex.ru
   Authorization: OAuth <your_token>
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../../../intro/authorization.md#get-oauth-token).

{% endlist %}

{{ feedback }}

<a href="../../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../../_includes/feedback-button.md) %}
