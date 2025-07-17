# Открытия приложения через deeplink

{{ deeplinks }}

## Формат запроса {#request-format}

```
GET {{ api-url }}/logs/v1/export/deeplinks.{csv | json}
  ? application_id=<int>
  & date_since=<string>
  & date_until=<string>
  & fields=<string>
  & [date_dimension=<string>]
  & [limit=<string>]
  & [use_utf8_bom=<bool>]
  & [<any field name>=<string>]
```

#|
|| `application_id`* | {{ application_id_query }} ||
|| `date_since`* | {{ date_since-query }} ||
|| `date_until`* | {{ date_until-query }} ||
|| `fields`* | Разделенный запятой [список полей](../endpoints.md) для выборки.

Список, который содержит все доступные поля (для быстрого копирования):

```objectivec translate=no
deeplink_url_host,deeplink_url_parameters,deeplink_url_path,deeplink_url_scheme,event_datetime,event_receive_datetime,event_receive_timestamp,event_timestamp,is_reengagement,profile_id,publisher_id,publisher_name,session_id,tracker_name,tracking_id,android_id,appmetrica_device_id,appmetrica_sdk_version,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,event_datetime,google_aid,ios_ifa,ios_ifv,mcc,mnc,original_device_model,os_version,windows_aid,app_build_number,app_package_name,app_version_name
``` ||
|| `date_dimension` | {{ date_dimension-query }} ||
|| `limit` | {{ limit-query }} ||
|| `use_utf8_bom` | {{ use_utf8_bom-query }} ||
|| `<any field name>` | {{ any-field-name-query }} ||
|#

## Формат ответа {#response-format}

В случае, если запрашиваются все доступные поля:

{% list tabs %}

- JSON

  ```json translate=no
  {
    "data": [
      {
        "deeplink_url_host": "string",
        "deeplink_url_parameters": "string",
        "deeplink_url_path": "string",
        "deeplink_url_scheme": "string",
        "event_datetime": "string",
        "event_receive_datetime": "string",
        "event_receive_timestamp": "integer",
        "event_timestamp": "integer",
        "is_reengagement": "boolean",
        "profile_id": "string",
        "publisher_id": "integer",
        "publisher_name": "string",
        "session_id": "integer",
        "tracker_name": "string",
        "tracking_id": "integer",
        "android_id": "string",
        "appmetrica_device_id": "integer",
        "appmetrica_sdk_version": "integer",
        "city": "string",
        "connection_type": "string",
        "country_iso_code": "string",
        "device_ipv6": "string",
        "device_locale": "string",
        "device_manufacturer": "string",
        "device_model": "string",
        "device_type": "string",
        "google_aid": "string",
        "ios_ifa": "string",
        "ios_ifv": "string",
        "mcc": "integer",
        "mnc": "integer",
        "original_device_model": "string",
        "os_version": "string",
        "windows_aid": "string",
        "app_build_number": "integer",
        "app_package_name": "string",
        "app_version_name": "string"
      },
      ...
    ]
  }
  ```

- CSV

  ```
  application_id,ios_ifa,os_name,...
  1111,024AE7EB-4128-4237-9803-D24950323D4D,ios,...
  1111,3A86D5E8-1985-4A23-B147-5A1C0CF8781E,ios,...
  1111,,android
  ...
  ```

{% endlist %}

#|
|| `deeplink_url_host` | {{ deeplink_url_host }} ||
|| `deeplink_url_parameters` | {{ deeplink_url_parameters }} Подробнее о передаче параметров в разделе [Параметры tracking URL](../../../mobile-tracking/tracking-specification.md#to-deeplink). ||
|| `deeplink_url_path` | {{ deeplink_url_path }} ||
|| `deeplink_url_scheme` | {{ deeplink_url_scheme }} ||
|| `event_datetime` | {{ event_datetime }} ||
|| `event_receive_datetime` | {{ event_receive_datetime }} ||
|| `event_receive_timestamp` | {{ event_receive_timestamp }} ||
|| `event_timestamp` | {{ event_timestamp }} ||
|| `is_reengagement` | {{ is_reengagement }} ||
|| `profile_id` | {{ profile_id }} ||
|| `publisher_id` | {{ publisher_id }} ||
|| `publisher_name` | {{ publisher_name }} ||
|| `session_id` | {{ session_id }} ||
|| `tracker_name` | {{ tracker_name }} ||
|| `tracking_id` | {{ tracking_id }} ||
|| `android_id` | {{ android_id }} ||
|| `appmetrica_device_id` | {{ appmetrica_device_id }} ||
|| `appmetrica_sdk_version` | {{ appmetrica_sdk_version }} ||
|| `city` | {{ city }} ||
|| `connection_type` | {{ connection_type }} ||
|| `country_iso_code` | {{ country_iso_code }} ||
|| `device_ipv6` | {{ device_ipv6 }} ||
|| `device_locale` | {{ device_locale }} ||
|| `device_manufacturer` | {{ device_manufacturer }} ||
|| `device_model` | {{ device_model }} ||
|| `device_type` | {{ device_type }} ||
|| `google_aid` | {{ google_aid }} ||
|| `ios_ifa` | {{ ios_ifa }} ||
|| `ios_ifv` | {{ ios_ifv }} ||
|| `mcc` | {{ mcc }} ||
|| `mnc` | {{ mnc }} ||
|| `original_device_model` | {{ original_device_model }} ||
|| `os_version` | {{ os_version }} ||
|| `windows_aid` | {{ windows_aid }} ||
|| `app_build_number` | {{ app_build_number }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|#

## Пример {#example}

Запрос:

```bash translate=no
curl -X GET \
  '{{ api-url }}/logs/v1/export/deeplinks.json?application_id=1111&date_since=2018-10-10&date_until=2018-10-11&fields=deeplink_url_host,deeplink_url_parameters,deeplink_url_path,deeplink_url_scheme,event_datetime,event_receive_datetime,event_receive_timestamp,event_timestamp,is_reengagement,profile_id,publisher_id,publisher_name,session_id,tracker_name,tracking_id,android_id,appmetrica_device_id,appmetrica_sdk_version,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,original_device_model,os_version,windows_aid,app_build_number,app_package_name,app_version_name' \
  -H 'Authorization: OAuth oauth_token'
```

Ответ:

```json translate=no
{
  "data": [
    {
      "deeplink_url_host": "deeplink_url_host__example",
      "deeplink_url_parameters": "custom_parameter=value1&another_param=value2",
      "deeplink_url_path": "deeplink_url_path__example",
      "deeplink_url_scheme": "myscheme",
      "event_datetime": "yyyy-mm-dd hh:mm:ss",
      "event_receive_datetime": "yyyy-mm-dd hh:mm:ss",
      "event_receive_timestamp": "1556258667",
      "event_timestamp": "1556258660",
      "is_reengagement": "false",
      "profile_id": "test",
      "publisher_id": "39",
      "publisher_name": "AdColony",
      "session_id": "10000000049",
      "tracker_name": "Advertising iOS campaign",
      "tracking_id": "12345678901234567890",
      "android_id": "android_id__example",
      "appmetrica_device_id": "123456789012345678",
      "appmetrica_sdk_version": "3001000",
      "city": "Moscow",
      "connection_type": "wifi",
      "country_iso_code": "RU",
      "device_ipv6": "::ffff:5.255.232.147",
      "device_locale": "ru_RU",
      "device_manufacturer": "Apple",
      "device_model": "iPhone X",
      "device_type": "phone",
      "google_aid": "google_aid__example",
      "ios_ifa": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "ios_ifv": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "mcc": "250",
      "mnc": "1",
      "original_device_model": "iPhone10,3",
      "os_version": "12.2",
      "windows_aid": "windows_aid__example",
      "app_build_number": "1",
      "app_package_name": "ru.yandex.metro",
      "app_version_name": "1.0"
    }
  ]
}
```

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
