# Quotas

The Logs API call restrictions apply to the app's API key. This means that limits for <q>App 1</q> do not affect limits for <q>App 2</q>.

After sending the request, Logs API queues it for further processing. The maximum acceptable number of request in a queue per API key is 3. If you have exceeded the limit, the Logs API returns:

```no-highlight translate=no
HTTP/1.1 429 Too Many Requests
Content-Type: text/plain

There are already 3 enqueued queries for given application_id. Wait until they are completed.
```

{% note info %}

The time to wait depends on the current server load and the amount of data your app has to process.

{% endnote %}

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
