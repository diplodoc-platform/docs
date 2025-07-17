# Quick start

1. Enable this option in the organization's account or [contact](../../troubleshooting/feedback-priority.md) a manager to learn how to access the Data Stream API.

2. If you haven't used AppMetrica API products yet, get an access token (for more information, see [Authorization](../../mobile-api/intro/authorization.md)).

3. Configure data streams using the [Changing settings](ref/settings-post.md) request. If you have multiple apps, you need to configure streams for each app.

   {% note info %}

   If you want to change the settings, use the same request. The new settings will be applied only to the new data and already generated files won't be changed.

   {% endnote %}

4. Wait a few minutes and check the setting using the [Stream status](ref/status.md) request. Pay attention to the `update_timestamp` field: data for the last 10 minutes usually continues to be updated.

5. Download data using the [Downloading data](ref/data.md) request. Each data type, such as events, installations, and session starts, is a separate stream.

6. Automate export by regularly calling the [Downloading data](ref/data.md) request with the desired `stream_window_timestamp`. We recommend checking the [stream status](ref/status.md) first to exclude requests with data that wasn't generated.

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
