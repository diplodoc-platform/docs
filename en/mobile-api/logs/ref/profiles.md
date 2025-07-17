# Profiles

{{ profiles }}

{% note info %}

The latest resource version is `profiles_v2`. The `profiles` resource will soon be removed. Resource version `profiles_v2` now includes new required parameters: `date_since` and `date_until`.

{% endnote %}

## Request format {#request-format}

```
GET {{ api-url }}/logs/v1/export/profiles_v2.{csv | json}
  ? application_id=<int>
  & [date_since=<string>]
  & [date_until=<string>]  
  & fields=<string>
  & [date_dimension=<string>]
  & [limit=<string>]
  & [use_utf8_bom=<bool>]
  & [<any field name>=<string>]
  & [version=<string>]
  & [update_timestamp=<string>]
```

#|
|| `application_id`* | {{ application_id_query }} ||
|| `date_since`* | {{ date_since-query }} ||
|| `date_until`* | {{ date_until-query }} ||
|| `fields`* | A comma-separated [list of fields](../endpoints.md) for the sample.

A list that contains all available fields (for quick copy):

```objectivec translate=no
profile_id,appmetrica_gender,appmetrica_birth_date,appmetrica_notifications_enabled,appmetrica_name,<any attribute name>,appmetrica_crashes,appmetrica_errors,appmetrica_first_session_date,appmetrica_last_start_date,appmetrica_push_opens,appmetrica_push_send_count,appmetrica_sdk_version,appmetrica_sessions,android_id,appmetrica_device_id,city,connection_type,country_iso_code,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,windows_aid,app_build_number,app_framework,app_package_name,app_version_name
```
||
|| `date_dimension` | {{ date_dimension-query }} ||
|| `limit` | {{ limit-query }} ||
|| `use_utf8_bom` | {{ use_utf8_bom-query }} ||
|| `<any field name>` | {{ any-field-name-query }} ||
|| `version` | {{ version_profile }} ||
|| `update_timestamp` | {{ update_timestamp }} ||
|#

## Response format {#response-format}

If all available fields are requested:

{% list tabs %}

- JSON

  ```json translate=no
  {
    "data": [
      {
        "profile_id": "string",
        "appmetrica_gender": "string",
        "appmetrica_birth_date": "string",
        "appmetrica_notifications_enabled": "boolean",
        "appmetrica_name": "string",
        "appmetrica_crashes": "integer",
        "appmetrica_errors": "integer",
        "appmetrica_first_session_date": "string",
        "appmetrica_last_start_date": "string",
        "appmetrica_push_opens": "integer",
        "appmetrica_push_send_count": "integer",
        "appmetrica_sdk_version": "integer",
        "appmetrica_sessions": "integer",
        "android_id": "string",
        "appmetrica_device_id": "integer",
        "city": "string",
        "connection_type": "string",
        "country_iso_code": "string",
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
        "windows_aid": "string",
        "app_build_number": "integer",
        "app_framework": "integer",
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
|| `profile_id` | {{ profile_id }} ||
|| `appmetrica_gender` | {{ appmetrica_gender }} ||
|| `appmetrica_birth_date` | {{ appmetrica_birth_date }} ||
|| `appmetrica_notifications_enabled` | {{ appmetrica_notifications_enabled }} ||
|| `appmetrica_name` | {{ appmetrica_name }} ||
|| `appmetrica_crashes` | {{ appmetrica_crashes }} ||
|| `appmetrica_errors` | {{ appmetrica_errors }} ||
|| `appmetrica_first_session_date` | {{ appmetrica_first_session_date }} ||
|| `appmetrica_last_start_date` | {{ appmetrica_last_start_date }} ||
|| `appmetrica_push_opens` | {{ appmetrica_push_opens }} ||
|| `appmetrica_push_send_count` | {{ appmetrica_push_send_count }} ||
|| `appmetrica_sdk_version` | {{ appmetrica_sdk_version }} ||
|| `appmetrica_sessions` | {{ appmetrica_sessions }} ||
|| `android_id` | {{ android_id }} ||
|| `appmetrica_device_id` | {{ appmetrica_device_id }} ||
|| `city` | {{ city }} ||
|| `connection_type` | {{ connection_type }} ||
|| `country_iso_code` | {{ country_iso_code }} ||
|| `device_manufacturer` | {{ device_manufacturer }} ||
|| `device_model` | {{ device_model }} ||
|| `device_type` | {{ device_type }} ||
|| `google_aid` | {{ google_aid }} ||
|| `ios_ifa` | {{ ios_ifa }} ||
|| `ios_ifv` | {{ ios_ifv }} ||
|| `mcc` | {{ mcc }} ||
|| `mnc` | {{ mnc }} ||
|| `operator_name` | {{ operator_name }} ||
|| `os_name` | {{ os_name }} ||
|| `os_version` | {{ os_version }} ||
|| `windows_aid` | {{ windows_aid }} ||
|| `app_build_number` | {{ app_build_number }} ||
|| `app_framework` | {{ app_framework }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|#

## Example {#example}

Request:

```bash translate=no
curl -X GET \
  '{{ api-url }}/logs/v1/export/profiles_v2.json?application_id=1111&fields=profile_id,appmetrica_gender,appmetrica_birth_date,appmetrica_notifications_enabled,appmetrica_name,appmetrica_crashes,appmetrica_errors,appmetrica_first_session_date,appmetrica_last_start_date,appmetrica_push_opens,appmetrica_push_send_count,appmetrica_sdk_version,appmetrica_sessions,android_id,appmetrica_device_id,city,connection_type,country_iso_code,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,windows_aid,app_build_number,app_framework,app_package_name,app_version_name' \
  -H 'Authorization: OAuth oauth_token'
```

Response:

```json translate=no
{
  "data": [
    {
      "profile_id": "test",
      "appmetrica_gender": "M",
      "appmetrica_birth_date": "30",
      "appmetrica_notifications_enabled": "false",
      "appmetrica_name": "John",
      "appmetrica_crashes": "1",
      "appmetrica_errors": "3",
      "appmetrica_first_session_date": "yyyy-mm-dd",
      "appmetrica_last_start_date": "yyyy-mm-dd",
      "appmetrica_push_opens": "3",
      "appmetrica_push_send_count": "8",
      "appmetrica_sdk_version": "3001000",
      "appmetrica_sessions": "15",
      "android_id": "android_id__example",
      "appmetrica_device_id": "123456789012345678",
      "city": "Moscow",
      "connection_type": "wifi",
      "country_iso_code": "RU",
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
      "windows_aid": "windows_aid__example",
      "app_build_number": "1",
      "app_framework": "0",
      "app_package_name": "ru.yandex.metro",
      "app_version_name": "1.0"
    }
  ]
}
```

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
