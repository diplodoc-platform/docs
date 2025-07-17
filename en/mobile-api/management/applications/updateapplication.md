# Update app settings

Changes settings of the specified app.

## Request format {#request-format}

```
PUT {{ api-url }}/management/v1/application/{id}
```

#|
|| `id` | App ID ||
|#

### Request body {#request-body}

```json translate=no
{
  "application": {
    "name": "string",
    "category": int,
    "time_zone_name": "string",
    "hide_address": bool,
    "gdpr_agreement_accepted": bool,
    "bundle_id": "string",
    "team_id": "string",
    "use_universal_links": bool
  }
}
```

#|
|| `name` | App name ||
|| `category` | ID of the app category.

To get a list of all app categories, use the [Category list](get-categories.md) method. ||
|| `time_zone_name` | Time zone for statistics ||
|| `hide_address` | The status indicating if the collecting complete IP addresses of users from the EU is enabled.

Possible values:
- `true` — Enabled.
- `false` — Disabled. ||
   || `gdpr_agreement_accepted` | Acceptance status of the [General Data Protection Regulation compliance](https://yandex.ru/legal/metrica_agreement/).

Possible values:
- `true` — The compliance is accepted.
- `false` — The compliance is declined. ||
   || `bundle_id` | Bundle ID. ||
   || `team_id` | App Prefix или Team ID. ||
   || `use_universal_links` | Status of using the Universal Link.

Possible values:
- `true` — Use universal link is enabled.
- `false` — Use universal link is disabled. ||
   |#

## Response format {#response-body}

```json translate=no
{
  "application": {
    "name": "string",
    "time_zone_name": "string",
    "hide_address": bool,
    "gdpr_agreement_accepted": bool,
    "category": int,
    "bundle_id": "string",
    "team_id": "string",
    "use_universal_links": bool,
    "universal_link": "string",
    "id": int,
    "uid": int,
    "owner_login": "string",
    "api_key128": "string",
    "import_token": "string",
    "permission": "string",
    "time_zone_offset": int,
    "create_date": "YYYY-MM-DD"
  }
}
```

#|
|| `name` | App name ||
|| `time_zone_name` | Time zone for statistics ||
|| `hide_address` | The status indicating if the collecting complete IP addresses of users from the EU is enabled.

Possible values:
- `true` — Enabled.
- `false` — Disabled. ||
   || `gdpr_agreement_accepted` | Acceptance status of the [General Data Protection Regulation compliance](https://yandex.ru/legal/metrica_agreement/).

Possible values:
- `true` — The compliance is accepted.
- `false` — The compliance is declined. ||
   || `category` | ID of the app category.

To get a list of all app categories, use the [Category list](get-categories.md) method. ||
|| `bundle_id` | Bundle ID. ||
|| `team_id` | App Prefix или Team ID. ||
|| `use_universal_links` | Status of using the Universal Link.

Possible values:
- `true` — Use universal link is enabled.
- `false` — Use universal link is disabled. ||
   || `universal_link` | Universal Link. ||
   || `id` | App ID ||
   || `uid` | ID of the user who added the app. ||
   || `owner_login` | Login of the app owner. ||
   || `api_key128` | API key. ||
   || `import_token` | Post API key. ||
   || `permission` | Access rights.

Possible values:

- `view` — Read only.
- `edit` — Read/Edit.
- `agency_view` — Agency read only.
- `agency_edit` — Agency read/edit.
- `own` — App owner.

For more information, see [Managing app access](../../../common/access.md). ||
|| `time_zone_offset` | The time zone offset relative to UTC in seconds. ||
|| `create_date` | Date the app was added. ||
|#

## Example {#example}

{% list tabs %}

- cURL

   ```bash translate=no
   curl -X PUT \
     '{{ api-url }}/management/v1/application/1111' \
     -H 'Content-Type: application/json' \
     -H 'Authorization: OAuth <your_token>' \
     -d '{
       "application": {
           "name": "string",
           "hide_address": true,
           "category": 85,
           "gdpr_agreement_accepted": true,
           "bundle_id": "string",
           "team_id": "string",
           "use_universal_links": true
       }
   }'
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../../intro/authorization.md#get-oauth-token).

- HTTP

   ```http translate=no
   PUT /management/v1/application/{id} HTTP/1.1
   Host: api.appmetrica.yandex.ru
   Content-Type: application/json
   Authorization: OAuth <your_token>

   {
       "application": {
           "name": "string",
           "hide_address": true,
           "category": 85,
           "gdpr_agreement_accepted": true,
           "bundle_id": "string",
           "team_id": "string",
           "use_universal_links": true
       }
   }
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../../intro/authorization.md#get-oauth-token).

{% endlist %}

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
