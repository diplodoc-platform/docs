# Method calls

{% note info %}

Requests are sent to the AppMetrica API over the HTTPS protocol.

{% endnote %}

Requests use the following format:

```no-highlight translate=no
method_type {{ api-url }}/API_section/version/method_name.result_format?parameters
```

- `method type` ― GET, POST, PUT or DELETE.
- `API_section` — The name of the API section that the action applies to.
- `version` — The number of the current version of the API.
- `method_name` — The URL of the resource that the action applies to.
- `result_format` — Optional part of the request. It sets the result format. By default, data is transmitted in JSON format.
- `parameters` — Required and optional request parameters.

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
