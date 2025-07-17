# Post API

Allows you to send events using an HTTP request to the AppMetrica server. Uploaded data is displayed in [AppMetrica reports](../../mobile-reports/index.md).

You can upload events in request parameters or in the request body (in the `csv` format). Data passed via the SDK and the API is merged if you passed the same value of [profile_id](*profile_id) or [appmetrica_device_id](*appmetrica_device_id).

Uploaded data is added to the data that has been received from the SDK. Data that is uploaded via the Post API is synced with the other data every 4 hours.

## Accessing the API {#access}

To work with the Post API, you need to get the _Post API key_ in the **Settings** section of your application.

You should pass the token in every API request in the  `post_api_key` parameter.

Learn more in the [example](post-import-events.md).

## Hosts {#hosts}

You should send requests to the `{{ api-url }}` host. For example:

```httpget translate=no
{{ api-url }}/logs/v1/import/events
```

or

```httpget translate=no
{{ api-url }}/logs/v1/import/events.csv
```

## API resources {#resources}

- [Uploading events](post-import-events.md)
- [Uploading In-App Revenue events](post-revenue.md)
- [Uploading Ad Revenue events](post-adrevenue.md)
- [Uploading E-commerce events](post-ecommerce.md)
- [Profile attributes](post-profile-attributes.md)

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}

[*profile_id]: {{ profile_id }}

[*appmetrica_device_id]: Hash from the unique identifier of the device set by AppMetrica.
