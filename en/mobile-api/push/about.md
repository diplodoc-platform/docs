# Push API

Enables you to create a push group, send push messages to devices, check the status of sending.

{% note info %}

In order to use the API, you need to [get an access token](../intro/authorization.md). You must transmit the access token in the HTTP header or parameters of every request.

{% endnote %}

A group is a container for sending push messages. It allows grouping messages sendings in the [push campaign report](../../mobile-reports/push-campaign.md). The group can contain an arbitrary number of sendings. The push campaign report displays these groups at the first level along with push campaigns that are launched through the [web interface](../../push/marketing.md).

A tag is an arbitrary string that labels every sending by the API. You can label an arbitrary number of sendings by one tag. The report displays tag at the second level.

You should send requests to the `https://push.api.appmetrica.yandex.net` host. For example:

```
https://push.api.appmetrica.yandex.net/push/v1/management/groups
```

Sent groups are displayed in the push campaign report and can be exported by using the [Reporting API](../api_v1/intro.md). The following dimensions and metrics are available to create a report:

- Dimensions: `ym:pc:group`, `ym:pc:tag`, `ym:pc:transfer`, `ym:pc:operatingSystem`.
- Metrics: `ym:pc:sentDevices`, `ym:pc:receivedDevices`, `ym:pc:openedDevices`, `ym:pc:conversion`.

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
