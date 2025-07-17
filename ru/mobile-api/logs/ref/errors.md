# Ошибки

{{ errors }}

## Формат запроса {#request-format}

```
GET {{ api-url }}/logs/v1/export/errors.{csv | json}
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
error,error_datetime,error_id,error_name,error_receive_datetime,error_receive_timestamp,error_timestamp,appmetrica_device_id,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,profile_id,windows_aid,app_package_name,app_version_name,application_id
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
        "error": "string",
        "error_datetime": "string",
        "error_id": "string",
        "error_name": "string",
        "error_receive_datetime": "string",
        "error_receive_timestamp": "integer",
        "error_timestamp": "integer",
        "appmetrica_device_id": "integer",
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
        "operator_name": "string",
        "os_name": "string",
        "os_version": "string",
        "profile_id": "string",
        "windows_aid": "string",
        "app_package_name": "string",
        "app_version_name": "string",
        "application_id": "integer"
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
|| `error` | {{ error }} ||
|| `error_datetime` | {{ error_datetime }} ||
|| `error_id` | {{ error_id }} ||
|| `error_name` | {{ error_name }} ||
|| `error_receive_datetime` | {{ error_receive_datetime }} ||
|| `error_receive_timestamp` | {{ error_receive_timestamp }} ||
|| `error_timestamp` | {{ error_timestamp }} ||
|| `appmetrica_device_id` | {{ appmetrica_device_id }} ||
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
|| `operator_name` | {{ operator_name }}||
|| `os_name` | {{ os_name }} ||
|| `os_version` | {{ os_version }} ||
|| `profile_id` | {{ profile_id }} ||
|| `windows_aid` | {{ windows_aid }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|| `application_id` | {{ application_id }} ||
|#

## Пример {#example}

Запрос:

```bash translate=no
curl -X GET \
  '{{ api-url }}/logs/v1/export/errors.json?application_id=1111&date_since=2018-10-10&date_until=2018-10-11&fields=error,error_datetime,error_id,error_name,error_receive_datetime,error_receive_timestamp,error_timestamp,appmetrica_device_id,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,profile_id,windows_aid,app_package_name,app_version_name,application_id' \
  -H 'Authorization: OAuth oauth_token'
```

Ответ:

```json translate=no
{
  "data": [
    {
      "error": "Incident Identifier: 0D315FB9-E548-4DB4-A740-CE99C44D8CEC\nCrashReporter Key: (null)\nHardware Model: iPhone10,3\nProcess: (null) [(null)]\nPath: (null)\nIdentifier: (null)\nVersion: (null) ((null))\nCode Type: ARM-64\nParent Process: ? [(null)]\n\nDate/Time: yyyy-mm-dd hh:mm:ss +0300\nOS Version: (null) (null) ((null))\nReport Version: 104\n\nException Type: Custom Exception\n\nName: API request error after 2 retries: AjaxError, ajax error [/api/v3/launcher/similar]. Actions: FEED_ITEM_SHOW,FEED_ITEM_IS_VIEWABLE,FEED_ITEM_CLICK,FEED_ITEM_IS_VIEWABLE,FEED_ITEM_SHOW,FEED_ITEM_CLICK,FEED_ITEM_IS_VIEWABLE,FEED_ITEM_SHOW. \nReason: \nUserInfo: {\n \"js_stack\" = \"\";\n}\n\n\n",
      "error_datetime": "yyyy-mm-dd hh:mm:ss",
      "error_id": "8553967143270641335",
      "error_name": "error_name__example",
      "error_receive_datetime": "yyyy-mm-dd hh:mm:ss",
      "error_receive_timestamp": "1556258667",
      "error_timestamp": "1556258660",
      "appmetrica_device_id": "123456789012345678",
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
      "operator_name": "MTS RUS",
      "os_name": "ios",
      "os_version": "12.2",
      "profile_id": "test",
      "windows_aid": "windows_aid__example",
      "app_package_name": "ru.yandex.metro",
      "app_version_name": "1.0",
      "application_id": "1111"
    }
  ]
}
```

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
