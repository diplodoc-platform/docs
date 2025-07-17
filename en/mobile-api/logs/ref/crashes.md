# Crashes

{{ crashes }}

## Request format {#request-format}

```
GET {{ api-url }}/logs/v1/export/crashes.{csv | json}
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
|| `fields`* | A comma-separated [list of fields](../endpoints.md) for the sample.

A list that contains all available fields (for quick copy):

```objectivec translate=no
crash,crash_datetime,crash_group_id,crash_id,crash_name,crash_receive_datetime,crash_receive_timestamp,crash_timestamp,appmetrica_device_id,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,profile_id,windows_aid,app_package_name,app_version_name,application_id
``` ||
|| `date_dimension` | {{ date_dimension-query }} ||
|| `limit` | {{ limit-query }} ||
|| `use_utf8_bom` | {{ use_utf8_bom-query }} ||
|| `<any field name>` | {{ any-field-name-query }} ||
|#

## Response format {#response-format}

If all available fields are requested:

{% list tabs %}

- JSON

  ```json translate=no
  {
    "data": [
      {
        "crash": "string",
        "crash_datetime": "string",
        "crash_group_id": "integer",
        "crash_id": "integer",
        "crash_name": "string",
        "crash_receive_datetime": "string",
        "crash_receive_timestamp": "integer",
        "crash_timestamp": "integer",
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
|| `crash` | {{ crash }} ||
|| `crash_datetime` | {{ crash_datetime }} ||
|| `crash_group_id` | {{ crash_group_id }} ||
|| `crash_id` | {{ crash_id }} ||
|| `crash_name` | {{ crash_name }} ||
|| `crash_receive_datetime` | {{ crash_receive_datetime }} ||
|| `crash_receive_timestamp` | {{ crash_receive_timestamp }} ||
|| `crash_timestamp` | {{ crash_timestamp }} ||
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

## Example {#example}

Request:

```bash translate=no
curl -X GET \
  '{{ api-url }}/logs/v1/export/crashes.json?application_id=1111&date_since=2018-10-10&date_until=2018-10-11&fields=crash,crash_datetime,crash_group_id,crash_id,crash_name,crash_receive_datetime,crash_receive_timestamp,crash_timestamp,appmetrica_device_id,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,profile_id,windows_aid,app_package_name,app_version_name,application_id' \
  -H 'Authorization: OAuth oauth_token'
```

Response:

```json translate=no
{
  "data": [
    {
      "crash": "Incident Identifier: 2BC150BD-6FBE-403E-A6EA-8BCBBB88D1FE\nCrashReporter Key: 45f8b76444af32746930a175a32f6ec4a3d34a81\nHardware Model: iPhone10,3,\n ... \"sessions_since_launch\": 1\n}\n",
      "crash_datetime": "yyyy-mm-dd hh:mm:ss",
      "crash_group_id": "2198476647264792568",
      "crash_id": "4076630759621469783",
      "crash_name": "crash_name__example",
      "crash_receive_datetime": "yyyy-mm-dd hh:mm:ss",
      "crash_receive_timestamp": "1556258667",
      "crash_timestamp": "1556258660",
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
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
