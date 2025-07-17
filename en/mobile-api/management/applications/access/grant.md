# Granting access

Grants access to statistics to a specific user or agency.

## Request format {#request-format}

```
POST {{ api-url }}/management/v1/application/{id}/grants
```

#|
|| `id` | App ID ||
|#

### Request body {#request-body}

```json translate=no
{
  "grant": {
    "user_login": "string",
    "perm": "string",
    "partners": [ int, int ],
    "event_labels": ["string", "string"]
  }
}
```
#|
|| `user_login` | Yandex email address (login) of the user who is granted access. ||
|| `perm` | Access level.

Possible values:

- `view`: Read only.
- `edit`: Read/Edit.
- `agency_view`: Agency read only.
- `agency_edit`: Agency read/edit.

To learn more about access levels, see [{#T}](../../../../common/access.md).
||
|| `partners` | IDs of advertising partners that are granted access. To get a list of all partners, use the [{#T}](list-partners.md) method.

This is a required field when granting `agency_view` and `agency_edit` permissions.

{% note info %}

If you're granting agency-level access, be sure to specify at least one advertising partner ID.

{% endnote %}

||
|| `event_labels` | Target events for which agencies can view statistics.

This is an additional field when granting `agency_view` and `agency_edit` permissions.

||
|#

## Response format {#response-body}

```json translate=no
{
  "grant" : {
    "user_login" : "string",
    "user_uid" : int,
    "perm" : "string",
    "comment" : "string",
    "partners" : [ int, int ],
    "event_labels" : [ "string", "string" ]
  }
```
#|
|| `user_login` | Yandex email address (login) of the user who is granted access. ||
|| `uid` | ID of the user who is granted access. ||
|| `perm` | Access level.

Possible values:

- `view`: Read only.
- `edit`: Read/Edit.
- `agency_view`: Agency read only.
- `agency_edit`: Agency read/edit.

To learn more about access levels, see [Managing app access](../../../../common/access.md). ||
|| `comment` | A comment. ||
|| `partners` | IDs of advertising partners that are granted access. To get a list of all partners, use the [{#T}](list-partners.md) method. ||
|| `event_labels` | Target events for which agencies can view statistics. ||
|#

## Example {#example}

{% list tabs %}

- cURL

   ```bash translate=no
   curl -X POST \
     '{{ api-url }}/management/v1/application/1111/grants' \
     -H 'Content-Type: application/json' \
     -H 'Authorization: OAuth <your_token>' \
     -d '{
     "grant": {
       "user_login": "user_login",
       "perm": "agency_view",
       "partners": [ 145375 ],
       "event_labels": ["Checkout", "Proceed to cart"]
     }
   }'
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../../../intro/authorization.md#get-oauth-token).

- HTTP

   ```http translate=no
   POST /management/v1/application/1111/grants HTTP/1.1
   Host: api.appmetrica.yandex.ru
   Content-Type: application/json
   Authorization: OAuth <your_token>

   {
     "grant": {
       "user_login": "user_login",
       "perm": "agency_view",
       "partners": [ 145375 ],
       "event_labels": ["Checkout", "Proceed to cart"]
     }
   }
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../../../intro/authorization.md#get-oauth-token).

{% endlist %}

{{ feedback }}

<a href="../../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../../_includes/feedback-button.md) %}

