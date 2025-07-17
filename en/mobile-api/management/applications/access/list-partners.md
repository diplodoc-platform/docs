# Partner list

Returns a list of partners.

## Request format {#request-format}

```
GET {{ api-url }}/management/v1/tracking/partners
```

## Response format {#response-body}

```json translate=no
  "partners" : {
    "total_rows" : 375,
    "partners" : [ {
      "id" : int,
      "name" : "string",
      "icon_url" : "string",
      "website_url" : "string",
      "campaigns_count" : int,
      "ownership" : "string",
      "type" : "string"
    },
  ...
    ]
  }
```
#|
|| `id` | Partner ID. ||
|| `name` | Partner name. ||
|| `icon_url` | Link to an icon. ||
|| `website_url` | Partner website. ||
|| `campaigns_count` | Number of active trackers. ||
|| `ownership` | Access level.

Possible values:
- `common`: Common access.
- `own`: Partner's owner access.
- `guest`: Guest access. ||
   || `type` | An attribute associated with the partner. ||
   |#

## Example {#example}

{% list tabs %}

- cURL

   ```bash translate=no
   curl -X GET \
     '{{ api-url }}/management/v1/tracking/partners' \
     -H 'Authorization: OAuth <your_token>'
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../../../intro/authorization.md#get-oauth-token).

- HTTP

   ```http translate=no
   GET /management/v1/tracking/partners HTTP/1.1
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
