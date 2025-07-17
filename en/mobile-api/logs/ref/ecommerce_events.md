# E-commerce

{{ ecommerce_events }}

## Request format {#request-format}

```
GET {{ api-url }}/logs/v1/export/ecommerce_events.{csv | json}
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
ecom_type,ecom_screen_name,ecom_screen_search_query,ecom_screen_payload,ecom_screen_category_path_1,ecom_screen_category_path_2,ecom_screen_category_path_3,ecom_screen_category_path_4,ecom_screen_category_path_5,ecom_screen_category_path_6,ecom_screen_category_path_7,ecom_screen_category_path_8,ecom_screen_category_path_9,ecom_screen_category_path_10,ecom_product_name,ecom_product_sku,ecom_product_promocodes,ecom_product_payload,ecom_product_category_path_1,ecom_product_category_path_2,ecom_product_category_path_3,ecom_product_category_path_4,ecom_product_category_path_5,ecom_product_category_path_6,ecom_product_category_path_7,ecom_product_category_path_8,ecom_product_category_path_9,ecom_product_category_path_10,ecom_product_actual_price_fiat_unit_type,ecom_product_actual_price_fiat_value,ecom_product_actual_price_internal_components,ecom_product_original_price_fiat_unit_type,ecom_product_original_price_fiat_value,ecom_product_original_price_internal_components,ecom_cart_item_price_fiat_unit_type,ecom_cart_item_price_fiat_value,ecom_cart_item_quantity,ecom_cart_item_internal_components,ecom_referrer_type,ecom_referrer_id,ecom_order_id,ecom_order_payload,event_datetime,event_name,event_receive_datetime,event_receive_timestamp,event_timestamp,session_id,installation_id,android_id,appmetrica_device_id,appmetrica_sdk_version,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,event_datetime,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,original_device_model,os_version,profile_id,windows_aid,app_build_number,app_package_name,app_version_name
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
        "ecom_type": "string",
        "ecom_screen_name": "string",
        "ecom_screen_search_query": "string",
        "ecom_screen_payload": "string",
        "ecom_screen_category_path_1": "string",
        "ecom_screen_category_path_2": "string",
        "ecom_screen_category_path_3": "string",
        "ecom_screen_category_path_4": "string",
        "ecom_screen_category_path_5": "string",
        "ecom_screen_category_path_6": "string",
        "ecom_screen_category_path_7": "string",
        "ecom_screen_category_path_8": "string",
        "ecom_screen_category_path_9": "string",
        "ecom_screen_category_path_10": "string",
        "ecom_product_name": "string",
        "ecom_product_sku": "integer",
        "ecom_product_promocodes": "string",
        "ecom_product_payload": "string",
        "ecom_product_category_path_1": "string",
        "ecom_product_category_path_2": "string",
        "ecom_product_category_path_3": "string",
        "ecom_product_category_path_4": "string",
        "ecom_product_category_path_5": "string",
        "ecom_product_category_path_6": "string",
        "ecom_product_category_path_7": "string",
        "ecom_product_category_path_8": "string",
        "ecom_product_category_path_9": "string",
        "ecom_product_category_path_10": "string",
        "ecom_product_actual_price_fiat_unit_type": "string",
        "ecom_product_actual_price_fiat_value": "string",
        "ecom_product_actual_price_internal_components": "string",
        "ecom_product_original_price_fiat_unit_type": "string",
        "ecom_product_original_price_fiat_value": "string",
        "ecom_product_original_price_internal_components": "string",
        "ecom_cart_item_price_fiat_unit_type": "string",
        "ecom_cart_item_price_fiat_value": "string",
        "ecom_cart_item_quantity": "integer",
        "ecom_cart_item_internal_components": "string",
        "ecom_referrer_type": "string",
        "ecom_referrer_id": "integer",
        "ecom_order_id": "integer",
        "ecom_order_payload": "string",
        "event_datetime": "string",
        "event_json": "string",
        "event_name": "string",
        "event_receive_datetime": "string",
        "event_receive_timestamp": "integer",
        "event_timestamp": "integer",
        "session_id": "integer",
        "installation_id": "string",
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
        "original_device_model": "string",
        "os_name": "string",
        "os_version": "string",
        "profile_id": "string",
        "windows_aid": "string",
        "app_build_number": "integer",
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
|| `ecom_type` | {{ ecom-type }} ||
|| `ecom_screen_name` | Screen name. ||
|| `ecom_screen_search_query` | Search query. ||
|| `ecom_screen_payload` | Screen parameters as passed to the SDK. The format is a JSON object with string key-value pairs, for example:

```
{
  "configuration": "landscape",
  "fullscreen": "true"
}

```
||
|| `ecom_screen_category_path_1` | Screen category. Level 1. ||
|| `ecom_screen_category_path_2` | Screen category. Level 2. ||
|| `ecom_screen_category_path_3` | Screen category. Level 3. ||
|| `ecom_screen_category_path_4` | Screen category. Level 4. ||
|| `ecom_screen_category_path_5` | Screen category. Level 5. ||
|| `ecom_screen_category_path_6` | Screen category. Level 6. ||
|| `ecom_screen_category_path_7` | Screen category. Level 7. ||
|| `ecom_screen_category_path_8` | Screen category. Level 8. ||
|| `ecom_screen_category_path_9` | Screen category. Level 9. ||
|| `ecom_screen_category_path_10` | Screen category. Level 10. ||
|| `ecom_product_name` | Product name. ||
|| `ecom_product_sku` | Product ID. ||
|| `ecom_product_promocodes` | Product promo codes. The format is a JSON array of strings, for example:

```
["BT79IYX", "UT5412EP"]

```
||
|| `ecom_product_payload` | Product parameters as passed to the SDK. The format is a JSON object with string key-value pairs, for example:

```
{
  "configuration": "landscape",
  "fullscreen": "true"
}

```
||
|| `ecom_product_category_path_1` | Product category. Level 1. ||
|| `ecom_product_category_path_2` | Product category. Level 2. ||
|| `ecom_product_category_path_3` | Product category. Level 3. ||
|| `ecom_product_category_path_4` | Product category. Level 4. ||
|| `ecom_product_category_path_5` | Product category. Level 5. ||
|| `ecom_product_category_path_6` | Product category. Level 6. ||
|| `ecom_product_category_path_7` | Product category. Level 7. ||
|| `ecom_product_category_path_8` | Product category. Level 8. ||
|| `ecom_product_category_path_9` | Product category. Level 9. ||
|| `ecom_product_category_path_10` | Product category. Level 10. ||
|| `ecom_product_actual_price_fiat_unit_type` | Currency of the actual product price. ||
|| `ecom_product_actual_price_fiat_value` | Actual product price. ||
|| `ecom_product_actual_price_internal_components` | Components of the actual product price. The format is an array of JSON objects with one key-value pair each, for example:

```
[
  { "wood": 25.01 },
  { "iron": 10 }
]

```
||
|| `ecom_product_original_price_fiat_unit_type` | Currency of the base product price. ||
|| `ecom_product_original_price_fiat_value` | Base product price. ||
|| `ecom_product_original_price_internal_components` | Components of the base product price. The format is an array of JSON objects with one key-value pair each, for example:

```
[
  { "wood": 25.01 },
  { "iron": 10 }
]

```
||
|| `ecom_cart_item_price_fiat_unit_type` | Price currency for the item in the cart. ||
|| `ecom_cart_item_price_fiat_value` | Price of the item in the cart. ||
|| `ecom_cart_item_quantity` | Number of items in the cart. ||
|| `ecom_cart_item_internal_components` | Price components for the item in the cart. The format is an array of JSON objects with one key-value pair each, for example:

```
[
  { "wood": 25.01 },
  { "iron": 10 }
]

```
||
|| `ecom_referrer_type` | Traffic source type. ||
|| `ecom_referrer_id` | Traffic source ID. ||
|| `ecom_order_id` | Purchase ID. ||
|| `ecom_order_payload` | Purchase parameters as passed to the SDK. The format is a JSON object with string key-value pairs, for example:

```
{
  "configuration": "landscape",
  "fullscreen": "true"
}
```
||
|| `event_datetime` | {{ event_datetime }} ||
|| `event_name` | {{ event_name }} ||
|| `event_receive_datetime` | {{ event_receive_datetime }} ||
|| `event_receive_timestamp` | {{ event_receive_timestamp }} ||
|| `event_timestamp` | {{ event_timestamp }} ||
|| `session_id` | {{ session_id }} ||
|| `installation_id` | {{ installation_id }} ||
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
|| `operator_name` | {{ operator_name }} ||
|| `original_device_model` | {{ original_device_model }} ||
|| `os_name` | {{ os_name }} ||
|| `os_version` | {{ os_version }} ||
|| `profile_id` | {{ profile_id }} ||
|| `windows_aid` | {{ windows_aid }} ||
|| `app_build_number` | {{ app_build_number }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|| `application_id` | {{ application_id }} ||
|#

## Example {#example}

Request:

```bash translate=no
curl -X GET \
  'https://api.appmetrica.yandex.ru/logs/v1/export/ecommerce_events.json?application_id=2421017&date_since=2023-01-04+00%3A00%3A00&date_until=2023-01-04+23%3A59%3A59&date_dimension=receive&use_utf8_bom=true&fields=ecom_type,ecom_screen_name,ecom_screen_search_query,ecom_screen_payload,ecom_screen_category_path_1,ecom_screen_category_path_2,ecom_screen_category_path_3,ecom_screen_category_path_4,ecom_screen_category_path_5,ecom_screen_category_path_6,ecom_screen_category_path_7,ecom_screen_category_path_8,ecom_screen_category_path_9,ecom_screen_category_path_10,ecom_product_name,ecom_product_sku,ecom_product_promocodes,ecom_product_payload,ecom_product_category_path_1,ecom_product_category_path_2,ecom_product_category_path_3,ecom_product_category_path_4,ecom_product_category_path_5,ecom_product_category_path_6,ecom_product_category_path_7,ecom_product_category_path_8,ecom_product_category_path_9,ecom_product_category_path_10,ecom_product_actual_price_fiat_unit_type,ecom_product_actual_price_fiat_value,ecom_product_actual_price_internal_components,ecom_product_original_price_fiat_unit_type,ecom_product_original_price_fiat_value,ecom_product_original_price_internal_components,ecom_cart_item_price_fiat_unit_type,ecom_cart_item_price_fiat_value,ecom_cart_item_quantity,ecom_cart_item_internal_components,ecom_referrer_type,ecom_referrer_id,ecom_order_id,ecom_order_payload,event_datetime,event_json,event_name,event_receive_datetime,event_receive_timestamp,event_timestamp,session_id,installation_id,appmetrica_device_id,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,original_device_model,os_name,os_version,profile_id,windows_aid,app_build_number,app_package_name,app_version_name,application_id' \
  -H 'Authorization: OAuth oauth_token'
```

Response:

```json translate=no
{
  "data": [
    {
      "ecom_type": "show_screen",
      "ecom_screen_name": "",
      "ecom_screen_search_query": "",
      "ecom_screen_payload": {
        "full_screen": "true"
      },
      "ecom_screen_category_path_1": "",
      "ecom_screen_category_path_2": "",
      "ecom_screen_category_path_3": "",
      "ecom_screen_category_path_4": "",
      "ecom_screen_category_path_5": "",
      "ecom_screen_category_path_6": "",
      "ecom_screen_category_path_7": "",
      "ecom_screen_category_path_8": "",
      "ecom_screen_category_path_9": "",
      "ecom_screen_category_path_10": "",
      "ecom_product_name": "",
      "ecom_product_sku": "",
      "ecom_product_promocodes": [],
      "ecom_product_payload": {},
      "ecom_product_category_path_1": "",
      "ecom_product_category_path_2": "",
      "ecom_product_category_path_3": "",
      "ecom_product_category_path_4": "",
      "ecom_product_category_path_5": "",
      "ecom_product_category_path_6": "",
      "ecom_product_category_path_7": "",
      "ecom_product_category_path_8": "",
      "ecom_product_category_path_9": "",
      "ecom_product_category_path_10": "",
      "ecom_product_actual_price_fiat_unit_type": "",
      "ecom_product_actual_price_fiat_value": 0,
      "ecom_product_actual_price_internal_components": [],
      "ecom_product_original_price_fiat_unit_type": "",
      "ecom_product_original_price_fiat_value": 0,
      "ecom_product_original_price_internal_components": [],
      "ecom_cart_item_price_fiat_unit_type": "",
      "ecom_cart_item_price_fiat_value": 0,
      "ecom_cart_item_quantity": 0,
      "ecom_cart_item_internal_components": [],
      "ecom_referrer_type": "",
      "ecom_referrer_id": "",
      "ecom_order_id": "",
      "ecom_order_payload": {},
      "event_datetime": "2024-07-29 23:37:01",
      "event_receive_datetime": "2024-07-29 23:37:14",
      "event_name": "",
      "event_receive_timestamp": 1722285434,
      "event_timestamp": 1722285421,
      "session_id": 10000000807,
      "installation_id": "6559cf2bb96c44189ef889bc4976b240",
      "appmetrica_device_id": 383777566819598200,
      "city": "",
      "connection_type": "wifi",
      "country_iso_code": "RU",
      "device_ipv6": "::ffff:79.173.67.100",
      "device_locale": "ru_RU",
      "device_manufacturer": "Realme",
      "device_model": "realme C21",
      "device_type": "phone",
      "google_aid": "",
      "ios_ifa": "",
      "ios_ifv": "",
      "mcc": 250,
      "mnc": 1,
      "operator_name": "MTS RUS",
      "original_device_model": "RMX3201",
      "os_name": "android",
      "os_version": 11,
      "profile_id": 107010519,
      "windows_aid": "",
      "app_build_number": 2024060301,
      "app_package_name": "com.biglion",
      "app_version_name": "7.4.40",
      "application_id": 178725
    },
    ...
  ]
}
```

### See also

- [How do I determine the event's source based on raw data?](../../../troubleshooting/troubleshooting.md#raw-data)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}

