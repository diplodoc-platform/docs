# Request flow

There are two stages in the request flow for the AppMetrica Logs API:

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-api/logsapi-scheme.png)

## Request to prepare data {#request-data-processing}

The AppMetrica Logs API accepts the request and puts it in the queue. If the request is processed successfully, AppMetrica prepares a file for download. In this case, the API returns the HTTP `202 Accepted` status. If the request resulted in an error, the API returns the appropriate response status, and the HTTP message body contains the error description.

{% note info %}

Requests in the queue are processed sequentially (each subsequent request is executed strictly after the previous one is completed).

{% endnote %}

While the request is being processed and the file is being prepared, all identical requests (with the same parameters) will return the HTTP `202 Accepted` status.

Sample request:

```no-highlight translate=no
GET /logs/v1/export/installations.json HTTP/1.1
Host: api.appmetrica.yandex.ru
Authorization: OAuth <your_token>
```

where `<your_token>` is an OAuth token that can be obtained using [instructions](../intro/authorization.md#get-oauth-token).

Response example:

```no-highlight translate=no
HTTP/1.1 202 Accepted
Content-Type: text/plain

Wait for result
```

To get compressed data, send the HTTP `Accept-Encoding:: gzip` header.

## Request to download data {#request-data-uploading}

The request to download data is identical to the request to prepare data. If the request to prepare the file is complete, for the next identical request, the Logs API returns the `200 OK` status. The results file is ready to be downloaded.

The file is available for download for 24 hours at the URL of the initial request. For a repeat request after 24 hours has passed, the request is put in the queue for processing and preparing a new file.

You can force regenerating the file using the HTTP `Cache-Control` header:

- To generate a new file, send the `Cache-Control: no-cache` header in the request.
- To download a file that was generated within the last N seconds, send the `Cache-Control: max-age=N` header in the request. If the file was created more than N seconds ago, AppMetrica generates a new file.
- To download the last generated file (if one exists), don't send the `Cache-Control` header in the request.

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
