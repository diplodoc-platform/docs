# Available endpoints

## Tracking clicks and impressions {#clicks}

```no-highlight translate=no
/logs/v1/export/clicks.{csv | json}
```

See detailed description of the resource [in the reference](ref/clicks.md).

Available fields:

```no-highlight translate=no
application_id,click_datetime,click_id,click_ipv6,click_timestamp,click_url_parameters,click_user_agent,publisher_id,publisher_name,tracker_name,tracking_id,touch_type,is_bot,city,country_iso_code,device_manufacturer,device_model,device_type,google_aid,oaid,ios_ifa,ios_ifv,os_name,os_version,windows_aid
```

Tracking information

#|
|| **Field** | **Description** ||
|| `application_id` | {{ application_id }} ||
|| `click_datetime` | {{ click_datetime }} ||
|| `click_id` | {{ click_id }} ||
|| `click_ipv6` | {{ click_ipv6 }} ||
|| `click_timestamp` | {{ click_timestamp }} ||
|| `click_url_parameters` | {{ click_url_parameters }} ||
|| `click_user_agent` | {{ click_user_agent }} ||
|| `publisher_id` | {{ publisher_id }} ||
|| `publisher_name` | {{ publisher_name }} ||
|| `tracker_name` | {{ tracker_name }} ||
|| `tracking_id` | {{ tracking_id }} ||
|| `touch_type` | {{ touch_type }} ||
|| `is_bot` | {{ is_bot }} ||
|#

Device Information (based on click recognition)

#|
|| **Field** | **Description** ||
|| `city` | {{ city_click }} ||
|| `country_iso_code` | {{ country_iso_code }} ||
|| `device_manufacturer` | {{ device_manufacturer }} ||
|| `device_model` | {{ device_model }} ||
|| `device_type` | {{ device_type }} ||
|| `google_aid` | {{ google_aid }} ||
|| `oaid` | {{ oaid }} ||
|| `ios_ifa` | {{ ios_ifa }} ||
|| `ios_ifv` | {{ ios_ifv }} ||
|| `os_name` | {{ os_name }} ||
|| `os_version` | {{ os_version }} ||
|| `windows_aid` | {{ windows_aid }} ||
|#

## App installations {#installations}

```no-highlight translate=no
/logs/v1/export/installations.{csv | json}
```

See detailed description of the resource [in the reference](ref/installations.md).

Available fields:

```no-highlight translate=no
application_id, installation_id,attributed_touch_type,click_datetime,click_id,click_ipv6,click_timestamp,click_url_parameters,click_user_agent,profile_id,publisher_id,publisher_name,tracker_name,tracking_id,install_datetime,install_ipv6,install_receive_datetime,install_receive_timestamp,install_timestamp,is_reattribution,is_reinstallation,match_type,appmetrica_device_id,city,connection_type,country_iso_code,device_locale,device_manufacturer,device_model,device_type,google_aid,oaid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,windows_aid,app_package_name,app_version_name
```

Tracking information

#|
|| **Field** | **Description** ||
|| `application_id` | {{ application_id }} ||
|| `installation_id` | {{ installation_id }} ||
|| `attributed_touch_type` | {{ attributed_touch_type }} ||
|| `click_datetime` | {{ click_datetime }} ||
|| `click_id` | {{ click_id }} ||
|| `click_ipv6` | {{ click_ipv6 }} ||
|| `click_timestamp` | {{ click_timestamp }} ||
|| `click_url_parameters` | {{ click_url_parameters }} ||
|| `click_user_agent` | {{ click_user_agent }} ||
|| `profile_id` | {{ profile_id }} ||
|| `publisher_id` | {{ publisher_id }} ||
|| `publisher_name` | {{ publisher_name }} ||
|| `tracker_name` | {{ tracker_name }} ||
|| `tracking_id` | {{ tracking_id }} ||
|#

Installation information

#|
|| **Field** | **Description** ||
|| `install_datetime` | {{ install_datetime }} ||
|| `install_ipv6` | {{ install_ipv6 }} ||
|| `install_receive_datetime` | {{ install_receive_datetime }} ||
|| `install_receive_timestamp` | {{ install_receive_timestamp }} ||
|| `install_timestamp` | {{ install_timestamp }} ||
|| `is_reattribution` | {{ is_reattribution }} ||
|| `is_reinstallation` | {{ is_reinstallation }} ||
|| `match_type` | [Attribution method](../../mobile-tracking/technology.md): `fingerprint` \| `referrer` \| `identifier` \| `''` (empty string). ||
|#

Device and operating system information

#|
|| **Field** | **Description** ||
|| `appmetrica_device_id` | {{ appmetrica_device_id }} ||
|| `city` | {{ city }} ||
|| `connection_type` | {{ connection_type }} ||
|| `country_iso_code` | {{ country_iso_code }} ||
|| `device_locale` | {{ device_locale }} ||
|| `device_manufacturer` | {{ device_manufacturer }} ||
|| `device_model` | {{ device_model }} ||
|| `device_type` | {{ device_type }} ||
|| `google_aid` | {{ google_aid }} ||
|| `oaid` | {{ oaid }} ||
|| `ios_ifa` | {{ ios_ifa }} ||
|| `ios_ifv` | {{ ios_ifv }} ||
|| `mcc` | {{ mcc }} ||
|| `mnc` | {{ mnc }} ||
|| `operator_name` | {{ operator_name }} ||
|| `os_name` | {{ os_name }} ||
|| `os_version` | {{ os_version }} ||
|| `windows_aid` | {{ windows_aid }} ||
|#

App information

#|
|| **Field** | **Description** ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|#

## Postbacks {#postback}

```no-highlight translate=no
/logs/v1/export/postbacks.{csv | json}
```

See detailed description of the resource [in the reference](ref/postbacks.md).

Available fields:

```no-highlight translate=no
application_id,attributed_touch_type,click_datetime,click_id,click_ipv6,click_timestamp,click_url_parameters,click_user_agent,profile_id,publisher_id,publisher_name,tracker_name,tracking_id,install_datetime,install_ipv6,install_timestamp,match_type,identifier,appmetrica_device_id,city,country_iso_code,device_locale,device_manufacturer,device_model,device_type,google_aid,oaid,ios_ifa,os_name,os_version,windows_aid,app_package_name,app_version_name,conversion_datetime,conversion_timestamp,event_name,attempt_datetime,attempt_timestamp,cost_model (postback_type),notifying_status,postback_url,postback_url_parameters,response_body,response_code
```

Tracking information

#|
|| **Field** | **Description** ||
|| `application_id` | {{ application_id }} ||
|| `attributed_touch_type` | {{ attributed_touch_type }} ||
|| `click_datetime` | {{ click_datetime }} ||
|| `click_id` | {{ click_id }} ||
|| `click_ipv6` | {{ click_ipv6 }} ||
|| `click_timestamp` | {{ click_timestamp }} ||
|| `click_url_parameters` | {{ click_url_parameters }} ||
|| `click_user_agent` | {{ click_user_agent }} ||
|| `profile_id` | {{ profile_id }} ||
|| `publisher_id` | {{ publisher_id_postback }} ||
|| `publisher_name` | {{ publisher_name_postback }} ||
|| `tracker_name` | {{ tracker_name_postback }} ||
|| `tracking_id` | {{ tracking_id_postback }} ||
|#

Installation and re-engagement information

#|
|| **Field** | **Description** ||
|| `install_datetime` | {{ install_datetime }} ||
|| `install_ipv6` | {{ install_ipv6 }} ||
|| `install_timestamp` | {{ install_timestamp }} ||
|| `match_type` | [Attribution method](../../mobile-tracking/technology.md): `fingerprint` \| `referrer` \| `identifier` \| `''` (empty string). ||
|| `identifier` | {{ identifier }} ||
|#

Device Information (based on click recognition)

#|
|| **Field** | **Description** ||
|| `appmetrica_device_id` | {{ appmetrica_device_id }} ||
|| `city` | {{ city_click }} ||
|| `country_iso_code` | {{ country_iso_code }} ||
|| `device_locale` | {{ device_locale }} ||
|| `device_manufacturer` | {{ device_manufacturer }} ||
|| `device_model` | {{ device_model }} ||
|| `device_type` | {{ device_type }} ||
|| `google_aid` | {{ google_aid }} ||
|| `oaid` | {{ oaid }} ||
|| `ios_ifa` | {{ ios_ifa }} ||
|| `ios_ifv` | {{ ios_ifv }} ||
|| `os_name` | {{ os_name }} ||
|| `os_version` | {{ os_version }} ||
|| `windows_aid` | {{ windows_aid }} ||
|#

App information

#|
|| **Field** | **Description** ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|#

Event information

#|
|| **Field** | **Description** ||
|| `conversion_datetime` | {{ conversion_datetime }} ||
|| `conversion_timestamp` | {{ conversion_timestamp }} ||
|| `event_name` | {{ event_name }} ||
|#

Information about the postback

#|
|| **Field** | **Description** ||
|| `attempt_datetime` | {{ attempt_datetime }} ||
|| `attempt_timestamp` | {{ attempt_timestamp }} ||
|| `cost_model (postback_type)` | {{ cost_model }} ||
|| `notifying_status` | {{ notifying_status }} ||
|| `postback_url` | {{ postback_url }} ||
|| `postback_url_parameters` | {{ postback_url_parameters }} ||
|| `response_body` | {{ response_body }} ||
|| `response_code` | {{ response_code }} ||
|#

## Events {#events}

```no-highlight translate=no
/logs/v1/export/events.{csv | json}
```

See detailed description of the resource [in the reference](ref/events.md).

Available fields:

```no-highlight translate=no
event_datetime,event_json,event_name,event_receive_datetime,event_receive_timestamp,event_timestamp,session_id,installation_id,appmetrica_device_id,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,original_device_model,os_name,os_version,profile_id,windows_aid,app_build_number,app_package_name,app_version_name,application_id
```

Event and session information

#|
|| **Field** | **Description** ||
|| `event_datetime` | {{ event_datetime }} ||
|| `event_json` | {{ event_json }} ||
|| `event_name` | {{ event_name }} ||
|| `event_receive_datetime` | {{ event_receive_datetime }} ||
|| `event_receive_timestamp` | {{ event_receive_timestamp }} ||
|| `event_timestamp` | {{ event_timestamp }} ||
|| `session_id` | {{ session_id }} ||
|| `installation_id` | {{ installation_id }} ||
|#

Device and OS information

#|
|| **Field** | **Description** ||
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
|| `operator_name` | {{ operator_name }} ||
|| `original_device_model` | {{ original_device_model }} ||
|| `os_name` | {{ os_name }} ||
|| `os_version` | {{ os_version }} ||
|| `profile_id` | {{ profile_id }} ||
|| `windows_aid` | {{ windows_aid }} ||
|#

App information

#|
|| **Field** | **Description** ||
|| `app_build_number` | {{ app_build_number }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|| `application_id` | {{ application_id }} ||
|#

## E-commerce {#ecommerce}

```no-highlight translate=no
/logs/v1/export/ecommerce_events.{csv | json}
```

See detailed description of the resource [in the reference](ref/ecommerce_events.md).

Available fields:

```no-highlight translate=no
ecom_type,ecom_screen_name,ecom_screen_search_query,ecom_screen_payload,ecom_screen_category_path_1,ecom_screen_category_path_2,ecom_screen_category_path_3,ecom_screen_category_path_4,ecom_screen_category_path_5,ecom_screen_category_path_6,ecom_screen_category_path_7,ecom_screen_category_path_8,ecom_screen_category_path_9,ecom_screen_category_path_10,ecom_product_name,ecom_product_sku,ecom_product_promocodes,ecom_product_payload,ecom_product_category_path_1,ecom_product_category_path_2,ecom_product_category_path_3,ecom_product_category_path_4,ecom_product_category_path_5,ecom_product_category_path_6,ecom_product_category_path_7,ecom_product_category_path_8,ecom_product_category_path_9,ecom_product_category_path_10,ecom_product_actual_price_fiat_unit_type,ecom_product_actual_price_fiat_value,ecom_product_actual_price_internal_components,ecom_product_original_price_fiat_unit_type,ecom_product_original_price_fiat_value,ecom_product_original_price_internal_components,ecom_cart_item_price_fiat_unit_type,ecom_cart_item_price_fiat_value,ecom_cart_item_quantity,ecom_cart_item_internal_components,ecom_referrer_type,ecom_referrer_id,ecom_order_id,ecom_order_payload,event_datetime,event_json,event_name,event_receive_datetime,event_receive_timestamp,event_timestamp,session_id,installation_id,appmetrica_device_id,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,original_device_model,os_name,os_version,profile_id,windows_aid,app_build_number,app_package_name,app_version_name,application_id
```

Purchase details

#|
|| **Field** | **Description** ||
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
|#

Event and session information

#|
|| **Field** | **Description** ||
|| `event_datetime` | {{ event_datetime }} ||
|| `event_name` | {{ event_name }} ||
|| `event_receive_datetime` | {{ event_receive_datetime }} ||
|| `event_receive_timestamp` | {{ event_receive_timestamp }} ||
|| `event_timestamp` | {{ event_timestamp }} ||
|| `session_id` | {{ session_id }} ||
|| `installation_id` | {{ installation_id }} ||
|| `certificate_verification_status` | {{ certificate_verification_status }} ||
|#

Device and operating system information

#|
|| **Field** | **Description** ||
|| `android_id` | {{ android_id }} ||
|| `appmetrica_device_id` | {{ appmetrica_device_id }} ||
|| `appmetrica_sdk_version` | {{ appmetrica_sdk_version }} ||
|| `country` | {{ country }} ||
|| `district` | {{ district }} ||
|| `area` | {{ area }} ||
|| `city` | {{ city }} ||
|| `connection_type` | {{ connection_type }} ||
|| `country_iso_code` | {{ country_iso_code }} ||
|| `device_ipv6` | {{ device_ipv6 }} ||
|| `device_locale` | {{ device_locale }} ||
|| `device_manufacturer` | {{ device_manufacturer }} ||
|| `device_model` | {{ device_model }} ||
|| `device_type` | {{ device_type }} ||
|| `event_source` | {{ event_source }} ||
|| `event_datetime` | {{ event_datetime }} ||
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
|#

App information

#|
|| **Field** | **Description** ||
|| `app_build_number` | {{ app_build_number }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|#

## Profiles {#profiles}

```
/logs/v1/export/profiles_v2.{csv | json}
```

See detailed description of the resource [in the reference](ref/profiles.md).

Available fields:

```no-highlight translate=no
profile_id,appmetrica_gender,appmetrica_birth_date,appmetrica_notifications_enabled,appmetrica_name,<any attribute name>,appmetrica_crashes,appmetrica_errors,appmetrica_first_session_date,appmetrica_last_start_date,appmetrica_push_opens,appmetrica_push_send_count,appmetrica_sdk_version,appmetrica_sessions,android_id,appmetrica_device_id,city,connection_type,country_iso_code,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,windows_aid,app_build_number,app_framework,app_package_name,app_version_name
```

Information about user attributes

#|
|| **Field** | **Description** ||
|| `profile_id` | {{ profile_id }} ||
|| `appmetrica_gender` | {{ appmetrica_gender }} ||
|| `appmetrica_birth_date` | {{ appmetrica_birth_date }} ||
|| `appmetrica_notifications_enabled` | {{ appmetrica_notifications_enabled }} ||
|| `appmetrica_name` | {{ appmetrica_name }} ||
|| `<any attribute name>` | {{ any-attribute-name }} ||
|#

Information about system attributes

#|
|| **Field** | **Description** ||
|| `appmetrica_crashes` | {{ appmetrica_crashes }} ||
|| `appmetrica_errors` | {{ appmetrica_errors }} ||
|| `appmetrica_first_session_date` | {{ appmetrica_first_session_date }} ||
|| `appmetrica_last_start_date` | {{ appmetrica_last_start_date }} ||
|| `appmetrica_push_opens` | {{ appmetrica_push_opens }} ||
|| `appmetrica_push_send_count` | {{ appmetrica_push_send_count }} ||
|| `appmetrica_sdk_version` | {{ appmetrica_sdk_version }} ||
|| `appmetrica_sessions` | {{ appmetrica_sessions }} ||
|#

Device and OS information

#|
|| **Field** | **Description** ||
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
|#

App information

#|
|| **Field** | **Description** ||
|| `app_build_number` | {{ app_build_number }} ||
|| `app_framework` | {{ app_framework }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|#

## Revenue {#revenue}

```
/logs/v1/export/revenue_events.{csv | json}
```

See detailed description of the resource [in the reference](ref/revenue_events.md).

Available fields:

```no-highlight translate=no
revenue_quantity,revenue_price,revenue_currency,revenue_product_id,revenue_order_id,revenue_order_id_source,is_revenue_verified,is_revenue_autocollected,revenue_inapp_type,revenue_event_type,event_datetime,event_name,event_receive_datetime,event_receive_timestamp,event_timestamp,session_id,installation_id,android_id,appmetrica_device_id,appmetrica_sdk_version,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,event_datetime,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,original_device_model,os_version,profile_id,windows_aid,app_build_number,app_package_name,app_version_name
```

Revenue information

#|
|| **Field** | **Description** ||
|| `revenue_quantity` | {{ revenue_quantity }} ||
|| `revenue_price` | {{ revenue_price }} ||
|| `revenue_currency` | {{ revenue_currency }} ||
|| `revenue_product_id` | {{ revenue_product_id }} ||
|| `revenue_order_id` | {{ revenue_order_id }} ||
|| `revenue_order_id_source` | {{ revenue_order_id_source }} ||
|| `is_revenue_verified` | {{ is_revenue_verified }} ||
|| `is_revenue_autocollected` | {{ is_revenue_autocollected }} ||
|| `revenue_inapp_type` | {{ revenue_inapp_type }} ||
|| `revenue_event_type` | {{ revenue_event_type }} ||
|#

Event and session information

#|
|| **Field** | **Description** ||
|| `event_datetime` | {{ event_datetime }} ||
|| `event_name` | {{ event_name }} ||
|| `event_receive_datetime` | {{ event_receive_datetime }} ||
|| `event_receive_timestamp` | {{ event_receive_timestamp }} ||
|| `event_timestamp` | {{ event_timestamp }} ||
|| `session_id` | {{ session_id }} ||
|| `installation_id` | {{ installation_id }} ||
|#

Device and OS information

#|
|| **Field** | **Description** ||
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
|| `event_datetime` | {{ event_datetime }} ||
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
|#

App information

#|
|| **Field** | **Description** ||
|| `app_build_number` | {{ app_build_number }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|#

## App openings via a deeplink {#deeplinks}

```
/logs/v1/export/deeplinks.{csv | json}
```

See detailed description of the resource [in the reference](ref/deeplinks.md).

Available fields:

```no-highlight translate=no
deeplink_url_host,deeplink_url_parameters,deeplink_url_path,deeplink_url_scheme,event_datetime,event_receive_datetime,event_receive_timestamp,event_timestamp,is_reengagement,profile_id,publisher_id,publisher_name,session_id,tracker_name,tracking_id,android_id,appmetrica_device_id,appmetrica_sdk_version,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,event_datetime,google_aid,ios_ifa,ios_ifv,mcc,mnc,original_device_model,os_version,windows_aid,app_build_number,app_package_name,app_version_name
```

Tracking information

#|
|| **Field** | **Description** ||
|| `deeplink_url_host` | {{ deeplink_url_host }} ||
|| `deeplink_url_parameters` | {{ deeplink_url_parameters }} For more information about passing parameters, see [Parameters of the tracking URL](../../mobile-tracking/tracking-specification.md#to-deeplink). ||
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
|#

Device and OS information

#|
|| **Field** | **Description** ||
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
|#

App information

#|
|| **Field** | **Description** ||
|| `app_build_number` | {{ app_build_number }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|#

## Push tokens {#push-tokens}

```
/logs/v1/export/push_tokens.{csv | json}
```

See detailed description of the resource [in the reference](ref/push_tokens.md).

Available fields:

```no-highlight translate=no
token,token_datetime,token_receive_datetime,token_receive_timestamp,token_timestamp,appmetrica_device_id,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,profile_id,windows_aid,app_package_name,app_version_name,application_id
```

Information about push tokens

#|
|| **Field** | **Description** ||
|| `token` | {{ token }} ||
|| `token_datetime` | {{ token_datetime }} ||
|| `token_receive_datetime` | {{ token_receive_datetime }} ||
|| `token_receive_timestamp` | {{ token_receive_timestamp }} ||
|| `token_timestamp` | {{ token_timestamp }} ||
|#

Device and OS information

#|
|| **Field** | **Description** ||
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
|#

App information

#|
|| **Field** | **Description** ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|| `application_id` | {{ application_id }} ||
|#

## Crashes {#crashes}

```
/logs/v1/export/crashes.{csv | json}
```

See detailed description of the resource [in the reference](ref/crashes.md).

Available fields:

```no-highlight translate=no
crash,crash_datetime,crash_group_id,crash_id,crash_name,crash_receive_datetime,crash_receive_timestamp,crash_timestamp,appmetrica_device_id,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,profile_id,windows_aid,app_package_name,app_version_name,application_id
```

Information about an app crash

#|
|| **Field** | **Description** ||
|| `crash` | {{ crash }} ||
|| `crash_datetime` | {{ crash_datetime }} ||
|| `crash_group_id` | {{ crash_group_id }} ||
|| `crash_id` | {{ crash_id }} ||
|| `crash_name` | {{ crash_name }} ||
|| `crash_receive_datetime` | {{ crash_receive_datetime }} ||
|| `crash_receive_timestamp` | {{ crash_receive_timestamp }} ||
|| `crash_timestamp` | {{ crash_timestamp }} ||
|#

Device and OS information

#|
|| **Field** | **Description** ||
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
|#

App information

#|
|| **Field** | **Description** ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|| `application_id` | {{ application_id }} ||
|#

## Errors {#errors}

```
/logs/v1/export/errors.{csv | json}
```

See detailed description of the resource [in the reference](ref/errors.md).

Available fields:

```no-highlight translate=no
error,error_datetime,error_id,error_name,error_receive_datetime,error_receive_timestamp,error_timestamp,appmetrica_device_id,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,profile_id,windows_aid,app_package_name,app_version_name,application_id
```

Information about app errors

#|
|| **Field** | **Description** ||
|| `error` | {{ error }} ||
|| `error_datetime` | {{ error_datetime }} ||
|| `error_id` | {{ error_id }} ||
|| `error_name` | {{ error_name }} ||
|| `error_receive_datetime` | {{ error_receive_datetime }} ||
|| `error_receive_timestamp` | {{ error_receive_timestamp }} ||
|| `error_timestamp` | {{ error_timestamp }} ||
|#

Device and OS information

#|
|| **Field** | **Description** ||
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
|#

App information

#|
|| **Field** | **Description** ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|| `application_id` | {{ application_id }} ||
|#

## Session starts {#sessions_starts}

```
/logs/v1/export/sessions_starts.{csv | json}
```

See detailed description of the resource [in the reference](ref/sessions_starts.md).

Available fields:

```no-highlight translate=no
session_id,session_start_datetime,session_start_receive_datetime,session_start_receive_timestamp,session_start_timestamp,appmetrica_device_id,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,profile_id,windows_aid,app_build_number,app_package_name,app_version_name,application_id
```

Session information

#|
|| **Field** | **Description** ||
|| `session_id` | {{ session_id }} ||
|| `session_start_datetime` | {{ session_start_datetime }} ||
|| `session_start_receive_datetime` | {{ session_start_receive_datetime }} ||
|| `session_start_receive_timestamp` | {{ session_start_receive_timestamp }} ||
|| `session_start_timestamp` | {{ session_start_timestamp }} ||
|#

Device and OS information

#|
|| **Field** | **Description** ||
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
|| `original_device_model` | {{ original_device_model }} ||
|| `os_name` | {{ os_name }} ||
|| `os_version` | {{ os_version }} ||
|| `profile_id` | {{ profile_id }} ||
|| `windows_aid` | {{ windows_aid }} ||
|#

#|
|| **Field** | **Description** ||
|| `app_build_number` | {{ app_build_number }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|| `application_id` | {{ application_id }} ||
|#

## Ad Revenue {#ad_revenue}

```
/logs/v1/export/ad_revenue_events.{csv | json}
```

```no-highlight translate=no
ad_revenue_datetime,ad_revenue_timestamp,ad_revenue_receive_datetime,ad_revenue_receive_timestamp,ad_revenue,ad_revenue_currency,ad_revenue_type,ad_revenue_data_source,ad_revenue_network,ad_revenue_placement_id,ad_revenue_placement_name,ad_revenue_unit_id,ad_revenue_unit_name,ad_revenue_precision,ad_revenue_payload,session_id,installation_id,android_id,appmetrica_device_id,appmetrica_sdk_version,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,original_device_model,os_version,profile_id,windows_aid,app_build_number,app_package_name,app_version_name
```

Ad Revenue information

#|
||
**Field** | **Description**
||
||
`ad_revenue_datetime`
|
Date and time of the event in `yyyy-mm-dd hh:mm:ss` format.
||
||
`ad_revenue_timestamp`
|
Time of the event in [UNIX timestamp](https://en.wikipedia.org/wiki/Unix_time) format.
||
||
`ad_revenue_receive_datetime`
|
Date and time the event was received on the server side. May differ from `ad_revenue_datetime` due to network delays or if the user's device was not connected at the time of the event.
||
||
`ad_revenue_receive_timestamp`
|
Time when the event was received on the server side, in [UNIX timestamp](https://en.wikipedia.org/wiki/Unix_time) format. May differ from `ad_revenue_timestamp` due to network delays or if the user's device was not connected at the time of the event.
||
||
`ad_revenue`
|
Ad Revenue amount.
||
||
`ad_revenue_currency`
|
Ad Revenue currency.
||
||
`ad_revenue_type`
|
Ad Revenue type. Possible values:

* `native`
* `banner`
* `rewarded`
* `interstitial`
* `mrec`
* `other`
||
||
`ad_revenue_data_source`
|
Flag indicating [that Ad Revenue was automatically collected](https://appmetrica.yandex.com/docs/en/sdk/android/off-adrevenue). Possible values:

* `autocollected`
* `manual`

||
||
`ad_revenue_network`
|
Advertising Network.
||
||
`ad_revenue_placement_id`
|
Ad placement ID.
||
||
`ad_revenue_placement_name`
|
Ad placement name.
||
||
`ad_revenue_unit_id`
|
Ad unit ID.
||
||
`ad_revenue_unit_name`
|
Ad unit name.
||
||
`ad_revenue_precision`
|
Accuracy of the Ad Revenue amount (as passed to the SDK). For example, "publisher_defined" or "estimated".
||
||
`ad_revenue_payload`
|
Additional data serialized into JSON.
||
|#

Event and session information

#|
|| **Field** | **Description** ||
|| `session_id` | {{ session_id }} ||
|| `installation_id` | {{ installation_id }} ||
|#

Device and operating system information

#|
|| **Field** | **Description** ||
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
|| `operator_name` | {{ operator_name }} ||
|| `original_device_model` | {{ original_device_model }} ||
|| `os_version` | {{ os_version }} ||
|| `profile_id` | {{ profile_id }} ||
|| `windows_aid` | {{ windows_aid }} ||
|#

App information

#|
|| **Field** | **Description** ||
|| `app_build_number` | {{ app_build_number }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|#

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
