# Category list

Returns a list of all app categories.

## Request format {#request-format}

```
GET {{ api-url }}/management/v1/metadata/application/categories
  ? [lang=<locale>]
```

#|
|| `lang` | Response localization.

Possible values:
- ru — The response is in Russian;
- en — The response is in English. ||
   |#

## Response format {#response-body}

```json translate=no
{
  "data": [
    {
      "id": int,
      "name": "string",
      "type": "string"
    },
    ...
  ]
}
```
#|
|| `data` | An object that contains information about categories. ||
|| `data.id` | ID of the category. ||
|| `data.name` | Name of the category.

To get the category name in English, add the parameter `lang=en` to the request. ||
|| `data.type` | Type of category.

Possible values:
- game — Games category.
- common — Common category. ||
   |#

## Example {#example}

{% list tabs %}

- cURL

   ```bash translate=no
   curl -X GET \
     '{{ api-url }}/management/v1/metadata/application/categories?lang=en' \
     -H 'Authorization: OAuth <your_token>'
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../../intro/authorization.md#get-oauth-token).

- HTTP

   ```http translate=no
   GET /management/v1/metadata/application/categories?lang=en HTTP/1.1
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
