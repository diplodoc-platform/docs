# Uploading events

Uploads information about events.

Usage example: You can send offline events to AppMetrica if the user doesn't log in to the app to perform them. For example, events like full energy recovery in a game or watching a movie on a Smart TV.

Event properties can be passed in parameters or in the body of the request. When you pass data in the body, you should add `.csv` to the URL of the request. For more information, see [Sample request](#sample).

To bind an event to a user, you should use one of the following fields in the API request:

- `profile_id`
- `appmetrica_device_id`

{% note alert %}

The Post API has restrictions on loading data. For more information, see [Restrictions](restrictions.md).

{% endnote %}

## Request format

```
POST {{api-url }}/logs/v1/import/events
  ? post_api_key=<string>
  & application_id=<int>
  & profile_id=<string>
  & appmetrica_device_id=<int>
  & event_name=<string>
  & event_timestamp=<int>
  & [event_json=<json>]
  & [session_type=<string>]
  & [ios_ifa=<string>]
  & [ios_ifv=<string>]
  & [google_aid=<string>]
  & [windows_aid=<string>]
  & [os_name=<string>]
  & [os_version=<string>]
  & [device_manufacturer=<string>]
  & [device_model=<string>]
  & [device_type=<string>]
  & [device_locale=<string>]
  & [app_version_name=<string>]
  & [app_package_name=<string>]
  & [connection_type=<string>]
  & [operator_name=<string>]
  & [mcc=<int>]
  & [mnc=<int>]
  & [device_ipv6=<string>]
```

#|
|| `post_api_key`* | {{ post_api_key }} ||
|| `application_id`* | {{ application_id }} ||
|| `profile_id`* | {{ post-profile_id }}

{% note alert %}

Do not pass the value with the `appmetrica_device_id` parameter. The server accepts only one of these parameters.

{% endnote %}

||
|| `appmetrica_device_id`* | {{ post-appmetrica_device_id }}

{% note alert %}

Do not pass the value with the `profile_id` parameter. The server accepts only one of these parameters.

{% endnote %}

||
|| `event_name`* | {{ event_name }} ||
|| `event_timestamp`* | {{ event_timestamp }} ||
|| `event_json` | {{ event_json }} Event parameters can be nested, for example: `{"param1":"param2","param1":{"param2":"param3"}}`. ||
|| `session_type` | The type of session. Possible values:

- `foreground` — In the [Events](../../mobile-reports/events-report.md) report AppMetrica increases the **Users** metric.
- `background` — In the [Events](../../mobile-reports/events-report.md) report AppMetrica increases the **Devices** metric. Such events are not included to the report with grouping by users, and into the profile card.

Default value is `background`. ||
|| `ios_ifa` | {{ ios_ifa }} ||
|| `ios_ifv` | {{ ios_ifv }} ||
|| `google_aid` | {{ google_aid }} ||
|| `windows_aid` | {{ windows_aid }} ||
|| `os_name` | {{ os_name }} ||
|| `os_version` | {{ os_version }} ||
|| `device_manufacturer` | {{ device_manufacturer }} ||
|| `device_model` | {{ device_model }} ||
|| `device_type` | {{ device_type }} ||
|| `device_locale` | {{ device_locale }} ||
|| `app_version_name` | {{ app_version_name }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `connection_type` | {{ connection_type }} ||
|| `operator_name` | {{ operator_name }} ||
|| `mcc` | {{ mcc }} ||
|| `mnc` | {{ mnc }} ||
|| `device_ipv6` | {{ device_ipv6 }} ||
|#

## Response codes

| Code | Description |
| ----- | ----- |
| 200 | Data has been uploaded successfully. |
| 403 | The request omitted an authorization header, or an invalid token was specified. |
| 400 | One or more required parameters were missing in the request. |

## Sample request {#sample}

{% list tabs %}

- Sending data in the request body

  ```http translate=no
  POST /logs/v1/import/events.csv?post_api_key=0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ012 HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Content-Length: 540i
  Connection: close

  device_model,device_ipv6,device_type,google_aid,app_package_name,operator_name,mnc,application_id,event_json,profile_id,event_name,event_timestamp
  iPhone X,2a02:6b8::40c:6676:baff:fea6:53d8,phone,01234567-890a-bcde-f012-3456789abcde,com.yandex.sample.metrica,MegaFon,2,1111,"{""key"":""value_1""}",1234567890123456789,event_name_1,1234567890
  iPhone X,2a02:6b8::40c:6676:baff:fea6:53d9,phone,fedcba98-7654-3210-fedc-ba9876543210,com.yandex.sample.metrica,MegaFon,2,1111,"{""key"":""value_2""}",9876543210987654321,event_name_2,1234567891
  ```

- Sending data in request parameters

  ```http translate=no
  POST /logs/v1/import/events?post_api_key=0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ012&device_model=iPhone%20X&device_ipv6=2a02%3A6b8%3A%3A40c%3A6676%3Abaff%3Afea6%3A53d8&device_type=phone&google_aid=01234567-890a-bcde-f012-3456789abcde&app_package_name=com.yandex.sample.metrica&operator_name=MegaFon&mnc=2&application_id=1111&event_json=%7B%22key%22%3A%22value%22%7D&profile_id=1234567890123456789&event_name=event_name&event_timestamp=1234567890 HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Content-Length: 0
  Connection: close
  ```

{% endlist %}

## Other Post API methods {#other-methods}

- [Uploading In-App Revenue events](post-revenue.md)
- [Uploading Ad Revenue events](post-adrevenue.md)
- [Uploading E-commerce events](post-ecommerce.md)
- [Profile attributes](post-profile-attributes.md)

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
