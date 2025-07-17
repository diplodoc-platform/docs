# Formats for input data and results

## Format for input data {#input}

Input data structures for POST and PUT methods are passed in the request body. Input structures match the output structures of the GET methods of the corresponding resources.

{% note info %}

To properly form the input structure for a POST or PUT method, call the GET method for a resource that already exists. Copy the resulting structure and define all the necessary field values.

{% endnote %}

The API POST and PUT methods accept input data in JSON format.

The format of input data is specified in the HTTP `Content-Type` header.

Acceptable header values: `application/x-yametrika+json` or `application/json`.

## Format of results {#result}

The Management API returns responses in UTF-8 encoding. Responses are in JSON format.

For example, the following request returns information about the app with the 1111 ID:

```no-highlight translate=no
GET /management/v1/application/1111 HTTP/1.1
Host: api.appmetrica.yandex.ru
Authorization: OAuth <your_token>
```

where `<your_token>` is an OAuth token that can be obtained using [instructions](../intro/authorization.md#get-oauth-token).

Response example:

```no-highlight translate=no
{
    "application": {
        "name": "Examples api.yandex.ru",
        "time_zone_name": "Europe/Moscow",
        "hide_address": false,
        "gdpr_agreement_accepted": false,
        "use_universal_links": false,
        "id": 1111,
        "uid": 178121744,
        "owner_login": "login",
        "time_zone_offset": 10800,
        "create_date": "2016-01-02"
    }
}
```

For debugging purposes, results can be formatted. To do this, pass the `pretty` parameter with the value set to `1` in any type of request:

```no-highlight translate=no
GET /management/v1/application/1111?pretty=1 HTTP/1.1
Host: api.appmetrica.yandex.ru
Authorization: OAuth <your_token>
```

where `<your_token>` is an OAuth token that can be obtained using [instructions](../intro/authorization.md#get-oauth-token).

When DELETE methods are executed successfully, the API returns the HTTP status with the code` 200`. If the HTTP status contains a different code, deletion was not performed.

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
