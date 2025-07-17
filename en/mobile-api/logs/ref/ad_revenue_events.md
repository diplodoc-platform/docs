# Ad Revenue

{{ ad_revenue_events }}

## Request format {#request-format}

```
GET {{ api-url }}/logs/v1/export/ad_revenue_events.{csv | json}
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
ad_revenue_datetime,ad_revenue_timestamp,ad_revenue_receive_datetime,ad_revenue_receive_timestamp,ad_revenue,ad_revenue_currency,ad_revenue_type,ad_revenue_data_source,ad_revenue_network,ad_revenue_placement_id,ad_revenue_placement_name,ad_revenue_unit_id,ad_revenue_unit_name,ad_revenue_precision,ad_revenue_payload,session_id,installation_id,android_id,appmetrica_device_id,appmetrica_sdk_version,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,original_device_model,os_version,profile_id,windows_aid,app_build_number,app_package_name,app_version_name
```
||
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
         "ad_revenue_type": "string",
         "ad_revenue": "string",
         "ad_revenue_currency": "string",
         "ad_revenue_data_source": "string",
         "ad_revenue_network": "string",
         "ad_revenue_placement_id": "string",
         "ad_revenue_placement_name": "string",
         "ad_revenue_unit_id": "string",
         "ad_revenue_unit_name": "string",
         "ad_revenue_precision": "string",
         "ad_revenue_payload": "string",
         "ad_revenue_datetime": "string",
         "ad_revenue_receive_datetime": "string",
         "ad_revenue_receive_timestamp": "integer",
         "ad_revenue_timestamp": "integer",
         "session_id": "integer",
         "installation_id": "string",
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
         "google_aid": "string",
         "ios_ifa": "string",
         "ios_ifv": "string",
         "mcc": "integer",
         "mnc": "integer",
         "operator_name": "string",
         "original_device_model": "string",
         "os_version": "string",
         "profile_id": "string",
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
|| `ad_revenue_datetime` | {{ event_datetime}} ||
|| `ad_revenue_timestamp` | {{ event_timestamp }} ||
|| `ad_revenue_receive_datetime` | {{ ad_revenue_receive_datetime }} ||
|| `ad_revenue_receive_timestamp` | {{ ad_revenue_receive_timestamp }} ||
|| `ad_revenue` |  {{ ad_revenue }} ||
|| `ad_revenue_currency` |  {{ ad_revenue_currency }} ||
|| `ad_revenue_type` | {{ ad_revenue_type }} ||
|| `ad_revenue_data_source` | {{ ad_revenue_data_source }} ||
|| `ad_revenue_network` | {{ ad_revenue_network }} ||
|| `ad_revenue_placement_id` | {{ ad_revenue_placement_id }} ||
|| `ad_revenue_placement_name` | {{ ad_revenue_placement_name }} ||
|| `ad_revenue_unit_id` | {{ ad_revenue_unit_id }} ||
|| `ad_revenue_unit_name` | {{ ad_revenue_unit_name }} ||
|| `ad_revenue_precision` | {{ ad_revenue_precision }} ||
|| `ad_revenue_payload` | {{ ad_revenue_payload }} ||
|| `session_id` | {{ session_id }} ||
|| `installation_id` | {{ installation_id }} ||
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
|| `google_aid` | {{ google_aid }} ||
|| `ios_ifa` | {{ ios_ifa }} ||
|| `ios_ifv` | {{ ios_ifv }} ||
|| `mcc` | {{ mcc }} ||
|| `mnc` | {{ mnc }} ||
|| `operator_name` | {{ operator_name }} ||
|| `original_device_model` | {{ original_device_model }} ||
|| `os_version` | {{ os_version }} ||
|| `profile_id` | {{ profile_id }} ||
|| `windows_aid` | {{ windows_aid }} ||
|| `app_build_number` | {{ app_build_number }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|#


## Example {#example}

Request:

```bash translate=no
curl -X GET \
  '{{ api-url }}/logs/v1/export/ad_revenue_events.json?application_id=1111&date_since=2018-10-10&date_until=2018-10-11&fields=ad_revenue_datetime,ad_revenue_timestamp,ad_revenue_receive_datetime,ad_revenue_receive_timestamp,ad_revenue,ad_revenue_currency,ad_revenue_type,ad_revenue_data_source,ad_revenue_network,ad_revenue_placement_id,ad_revenue_placement_name,ad_revenue_unit_id,ad_revenue_unit_name,ad_revenue_precision,ad_revenue_payload,session_id,installation_id,android_id,appmetrica_device_id,appmetrica_sdk_version,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,original_device_model,os_version,profile_id,windows_aid,app_build_number,app_package_name,app_version_name' \
  -H 'Authorization: OAuth oauth_token'
```

Response:

```json translate=no
{
  "data": [
    {
      "ad_revenue_type": "banner",
      "ad_revenue": "299",
      "ad_revenue_currency": "RUB",
      "ad_revenue_data_source": "manual",
      "ad_revenue_network": "network__example",
      "ad_revenue_placement_id": "ad_revenue_placement_id__example",
      "ad_revenue_placement_name": "ad_revenue_placement_name__example",
      "ad_revenue_unit_id": "ad_revenue_unit_id__example",
      "ad_revenue_unit_name": "ad_revenue_unit_name__example",
      "ad_revenue_precision": "estimated",
      "ad_revenue_payload": "{\"example_key1\":\"example_value1\", \"example_key2\":\"example_value2\"}",
      "ad_revenue_datetime": "yyyy-mm-dd hh:mm:ss",
      "ad_revenue_receive_datetime": "yyyy-mm-dd hh:mm:ss",
      "ad_revenue_receive_timestamp": "1556258667",
      "ad_revenue_timestamp": "1556258660",
      "session_id": "10000000049",
      "installation_id": "installation_id__example",
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
      "google_aid": "google_aid__example",
      "ios_ifa": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "ios_ifv": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "mcc": "250",
      "mnc": "1",
      "operator_name": "MTS RUS",
      "original_device_model": "iPhone10,3",
      "os_version": "12.2",
      "profile_id": "test",
      "windows_aid": "windows_aid__example",
      "app_build_number": "1",
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
