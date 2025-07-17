# Доступные точки запроса

## Трекинговые клики и показы {#clicks}

```no-highlight translate=no
/logs/v1/export/clicks.{csv | json}
```

Подробное описание ресурса [в справочнике](ref/clicks.md).

Доступные поля:

```no-highlight translate=no
application_id,click_datetime,click_id,click_ipv6,click_timestamp,click_url_parameters,click_user_agent,publisher_id,publisher_name,tracker_name,tracking_id,touch_type,is_bot,city,country_iso_code,device_manufacturer,device_model,device_type,google_aid,oaid,ios_ifa,ios_ifv,os_name,os_version,windows_aid
```

Трекинговая информация

#|
|| **Поле** | **Описание** ||
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

Информация об устройстве (определенная по клику)

#|
|| **Поле** | **Описание** ||
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

## Установки приложения {#installations}

```no-highlight translate=no
/logs/v1/export/installations.{csv | json}
```

Подробное описание ресурса [в справочнике](ref/installations.md).

Доступные поля:

```no-highlight translate=no
application_id,installation_id,attributed_touch_type,click_datetime,click_id,click_ipv6,click_timestamp,click_url_parameters,click_user_agent,profile_id,publisher_id,publisher_name,tracker_name,tracking_id,install_datetime,install_ipv6,install_receive_datetime,install_receive_timestamp,install_timestamp,is_reattribution,is_reinstallation,match_type,appmetrica_device_id,city,connection_type,country_iso_code,device_locale,device_manufacturer,device_model,device_type,google_aid,oaid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,windows_aid,app_package_name,app_version_name
```

Трекинговая информация

#|
|| **Поле** | **Описание** ||
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

Информация об установке

#|
|| **Поле** | **Описание** ||
|| `install_datetime` | {{ install_datetime }} ||
|| `install_ipv6` | {{ install_ipv6 }} ||
|| `install_receive_datetime` | {{ install_receive_datetime }} ||
|| `install_receive_timestamp` | {{ install_receive_timestamp }} ||
|| `install_timestamp` | {{ install_timestamp }} ||
|| `is_reattribution` | {{ is_reattribution }} ||
|| `is_reinstallation` | {{ is_reinstallation }} ||
|| `match_type` | [Способ атрибуции](../../mobile-tracking/technology.md): `fingerprint` \| `referrer` \| `identifier` \| `''` (пустая строка). ||
|#

Информация об устройстве и ОС

#|
|| **Поле** | **Описание** ||
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

Информация о приложении

#|
|| **Поле** | **Описание** ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|#

## Постбеки {#postback}

```no-highlight translate=no
/logs/v1/export/postbacks.{csv | json}
```

Подробное описание ресурса [в справочнике](ref/postbacks.md).

Доступные поля:

```no-highlight translate=no
application_id,attributed_touch_type,click_datetime,click_id,click_ipv6,click_timestamp,click_url_parameters,click_user_agent,profile_id,publisher_id,publisher_name,tracker_name,tracking_id,install_datetime,install_ipv6,install_timestamp,match_type,identifier,appmetrica_device_id,city,country_iso_code,device_locale,device_manufacturer,device_model,device_type,google_aid,oaid,ios_ifa,os_name,os_version,windows_aid,app_package_name,app_version_name,conversion_datetime,conversion_timestamp,event_name,attempt_datetime,attempt_timestamp,cost_model (postback_type),notifying_status,postback_url,postback_url_parameters,response_body,response_code
```

Трекинговая информация

#|
|| **Поле** | **Описание** ||
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

Информация об установке и re-engagement

#|
|| **Поле** | **Описание** ||
|| `install_datetime` | {{ install_datetime }} ||
|| `install_ipv6` | {{ install_ipv6 }} ||
|| `install_timestamp` | {{ install_timestamp }} ||
|| `match_type` | [Способ атрибуции](../../mobile-tracking/technology.md): `fingerprint` \| `referrer` \| `identifier` \| `''` (пустая строка). ||
|| `identifier` | {{ identifier }} ||
|#

Информация об устройстве (определенная по клику)

#|
|| **Поле** | **Описание** ||
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

Информация о приложении

#|
|| **Поле** | **Описание** ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|#

Информация о событии

#|
|| **Поле** | **Описание** ||
|| `conversion_datetime` | {{ conversion_datetime }} ||
|| `conversion_timestamp` | {{ conversion_timestamp }} ||
|| `event_name` | {{ event_name }} ||
|#

Информация о postback

#|
|| **Поле** | **Описание** ||
|| `attempt_datetime` | {{ attempt_datetime }} ||
|| `attempt_timestamp` | {{ attempt_timestamp }} ||
|| `cost_model (postback_type)` | {{ cost_model }} ||
|| `notifying_status` | {{ notifying_status }} ||
|| `postback_url` | {{ postback_url }} ||
|| `postback_url_parameters` | {{ postback_url_parameters }} ||
|| `response_body` | {{ response_body }} ||
|| `response_code` | {{ response_code }} ||
|#

## События приложения {#events}

```no-highlight translate=no
/logs/v1/export/events.{csv | json}
```

Подробное описание ресурса [в справочнике](ref/events.md).

Доступные поля:

```no-highlight translate=no
event_datetime,event_json,event_name,event_receive_datetime,event_receive_timestamp,event_timestamp,session_id,installation_id,appmetrica_device_id,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,original_device_model,os_name,os_version,profile_id,windows_aid,app_build_number,app_package_name,app_version_name,application_id
```

Информация о событии и сессии

#|
|| **Поле** | **Описание** ||
|| `event_datetime` | {{ event_datetime }} ||
|| `event_json` | {{ event_json }} ||
|| `event_name` | {{ event_name }} ||
|| `event_receive_datetime` | {{ event_receive_datetime }} ||
|| `event_receive_timestamp` | {{ event_receive_timestamp }} ||
|| `event_timestamp` | {{ event_timestamp }} ||
|| `session_id` | {{ session_id }} ||
|| `installation_id` | {{ installation_id }} ||
|#

Информация об устройстве и ОС

#|
|| **Поле** | **Описание** ||
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

Информация о приложении

#|
|| **Поле** | **Описание** ||
|| `app_build_number` | {{ app_build_number }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|| `application_id` | {{ application_id }} ||
|#

## E-commerce {#ecommerce}

```no-highlight translate=no
/logs/v1/export/ecommerce_events.{csv | json}
```

Подробное описание ресурса [в справочнике](ref/ecommerce_events.md).

Доступные поля:

```no-highlight translate=no
ecom_type,ecom_screen_name,ecom_screen_search_query,ecom_screen_payload,ecom_screen_category_path_1,ecom_screen_category_path_2,ecom_screen_category_path_3,ecom_screen_category_path_4,ecom_screen_category_path_5,ecom_screen_category_path_6,ecom_screen_category_path_7,ecom_screen_category_path_8,ecom_screen_category_path_9,ecom_screen_category_path_10,ecom_product_name,ecom_product_sku,ecom_product_promocodes,ecom_product_payload,ecom_product_category_path_1,ecom_product_category_path_2,ecom_product_category_path_3,ecom_product_category_path_4,ecom_product_category_path_5,ecom_product_category_path_6,ecom_product_category_path_7,ecom_product_category_path_8,ecom_product_category_path_9,ecom_product_category_path_10,ecom_product_actual_price_fiat_unit_type,ecom_product_actual_price_fiat_value,ecom_product_actual_price_internal_components,ecom_product_original_price_fiat_unit_type,ecom_product_original_price_fiat_value,ecom_product_original_price_internal_components,ecom_cart_item_price_fiat_unit_type,ecom_cart_item_price_fiat_value,ecom_cart_item_quantity,ecom_cart_item_internal_components,ecom_referrer_type,ecom_referrer_id,ecom_order_id,ecom_order_payload,event_datetime,event_json,event_name,event_receive_datetime,event_receive_timestamp,event_timestamp,session_id,installation_id,appmetrica_device_id,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,original_device_model,os_name,os_version,profile_id,windows_aid,app_build_number,app_package_name,app_version_name,application_id
```

Информация о покупках

#|
|| **Поле** | **Описание** ||
|| `ecom_type` | {{ ecom-type }} ||
|| `ecom_screen_name` | Название экрана. ||
|| `ecom_screen_search_query` | Поисковый запрос. ||
|| `ecom_screen_payload` | Параметры экрана, как передали в SDK. Имеет формат объекта JSON “строковые ключ-значение”, например:

```
{
  "configuration": "landscape",
  "fullscreen": "true"
}

``` 
||
|| `ecom_screen_category_path_1` | Категория экрана. Уровень 1. ||
|| `ecom_screen_category_path_2` | Категория экрана. Уровень 2. ||
|| `ecom_screen_category_path_3` | Категория экрана. Уровень 3. ||
|| `ecom_screen_category_path_4` | Категория экрана. Уровень 4. ||
|| `ecom_screen_category_path_5` | Категория экрана. Уровень 5. ||
|| `ecom_screen_category_path_6` | Категория экрана. Уровень 6. ||
|| `ecom_screen_category_path_7` | Категория экрана. Уровень 7. ||
|| `ecom_screen_category_path_8` | Категория экрана. Уровень 8. ||
|| `ecom_screen_category_path_9` | Категория экрана. Уровень 9. ||
|| `ecom_screen_category_path_10` | Категория экрана. Уровень 10. ||
|| `ecom_product_name` | Название товара. ||
|| `ecom_product_sku` | ID товара. ||
|| `ecom_product_promocodes` | Промокоды товара. Имеет формат списка строк JSON, например:

```
["BT79IYX", "UT5412EP"]

```
||
|| `ecom_product_payload` | Параметры товара, как передали в SDK. Имеет формат объекта JSON “строковые ключ-значение”, например:

```
{
  "configuration": "landscape",
  "fullscreen": "true"
}

```
||
|| `ecom_product_category_path_1` | Категория товара. Уровень 1. ||
|| `ecom_product_category_path_2` | Категория товара. Уровень 2. ||
|| `ecom_product_category_path_3` | Категория товара. Уровень 3. ||
|| `ecom_product_category_path_4` | Категория товара. Уровень 4. ||
|| `ecom_product_category_path_5` | Категория товара. Уровень 5. ||
|| `ecom_product_category_path_6` | Категория товара. Уровень 6. ||
|| `ecom_product_category_path_7` | Категория товара. Уровень 7. ||
|| `ecom_product_category_path_8` | Категория товара. Уровень 8. ||
|| `ecom_product_category_path_9` | Категория товара. Уровень 9. ||
|| `ecom_product_category_path_10` | Категория товара. Уровень 10. ||
|| `ecom_product_actual_price_fiat_unit_type` | Валюта актуальной стоимости товара. ||
|| `ecom_product_actual_price_fiat_value` | Актуальная стоимость товара. ||
|| `ecom_product_actual_price_internal_components` | Составляющие актуальной стоимости товара. Имеет формат списка JSON-объектов-пар “ключ-значение”, например:

```
[
  { "wood": 25.01 },
  { "iron": 10 }
]

```
||
|| `ecom_product_original_price_fiat_unit_type` | Валюта базовой стоимости товара. ||
|| `ecom_product_original_price_fiat_value` | Базовая стоимость товара. ||
|| `ecom_product_original_price_internal_components` | Составляющие базовой стоимости товара. Имеет формат списка  JSON-объектов-пар “ключ-значение”, например:

```
[
  { "wood": 25.01 },
  { "iron": 10 }
]

```
||
|| `ecom_cart_item_price_fiat_unit_type` | Валюта стоимости товара в корзине. ||
|| `ecom_cart_item_price_fiat_value` | Стоимость товара в корзине. ||
|| `ecom_cart_item_quantity` | Количество товара в корзине. ||
|| `ecom_cart_item_internal_components` | Составляющие стоимости товара в корзине. Имеет формат списка JSON-объектов-пар “ключ-значение”, например:

```
[
  { "wood": 25.01 },
  { "iron": 10 }
]

```
||
|| `ecom_referrer_type` | Тип источника перехода. ||
|| `ecom_referrer_id` | ID источника перехода. ||
|| `ecom_order_id` | ID покупки. ||
|| `ecom_order_payload` | Параметры покупки, как передали в SDK. Имеет формат объекта JSON “строковые ключ-значение”, например:

```
{
  "configuration": "landscape",
  "fullscreen": "true"
}
```
||
|#

Информация о событии и сессии

#|
|| **Поле** | **Описание** ||
|| `event_datetime` | {{ event_datetime }} ||
|| `event_name` | {{ event_name }} ||
|| `event_receive_datetime` | {{ event_receive_datetime }} ||
|| `event_receive_timestamp` | {{ event_receive_timestamp }} ||
|| `event_timestamp` | {{ event_timestamp }} ||
|| `session_id` | {{ session_id }} ||
|| `installation_id` | {{ installation_id }} ||
|| `certificate_verification_status` | {{ certificate_verification_status }} ||
|#

Информация об устройстве и ОС

#|
|| **Поле** | **Описание** ||
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

Информация о приложении

#|
|| **Поле** | **Описание** ||
|| `app_build_number` | {{ app_build_number }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|#

## Профили {#profiles}

```
/logs/v1/export/profiles_v2.{csv | json}
```

Подробное описание ресурса [в справочнике](ref/profiles.md).

Доступные поля:

```no-highlight translate=no
profile_id,appmetrica_gender,appmetrica_birth_date,appmetrica_notifications_enabled,appmetrica_name,<any attribute name>,appmetrica_crashes,appmetrica_errors,appmetrica_first_session_date,appmetrica_last_start_date,appmetrica_push_opens,appmetrica_push_send_count,appmetrica_sdk_version,appmetrica_sessions,android_id,appmetrica_device_id,city,connection_type,country_iso_code,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,windows_aid,app_build_number,app_framework,app_package_name,app_version_name
```

Информация о пользовательских атрибутах

#|
|| **Поле** | **Описание** ||
|| `profile_id` | {{ profile_id }} ||
|| `appmetrica_gender` | {{ appmetrica_gender }} ||
|| `appmetrica_birth_date` | {{ appmetrica_birth_date }} ||
|| `appmetrica_notifications_enabled` | {{ appmetrica_notifications_enabled }} ||
|| `appmetrica_name` | {{ appmetrica_name }} ||
|| `<any attribute name>` | {{ any-attribute-name }} ||
|#

Информация о системных атрибутах

#|
|| **Поле** | **Описание** ||
|| `appmetrica_crashes` | {{ appmetrica_crashes }} ||
|| `appmetrica_errors` | {{ appmetrica_errors }} ||
|| `appmetrica_first_session_date` | {{ appmetrica_first_session_date }} ||
|| `appmetrica_last_start_date` | {{ appmetrica_last_start_date }} ||
|| `appmetrica_push_opens` | {{ appmetrica_push_opens }} ||
|| `appmetrica_push_send_count` | {{ appmetrica_push_send_count }} ||
|| `appmetrica_sdk_version` | {{ appmetrica_sdk_version }} ||
|| `appmetrica_sessions` | {{ appmetrica_sessions }} ||
|#

Информация об устройстве и ОС

#|
|| **Поле** | **Описание** ||
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

Информация о приложении

#|
|| **Поле** | **Описание** ||
|| `app_build_number` | {{ app_build_number }} ||
|| `app_framework` | {{ app_framework }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|#

## Revenue {#revenue}

```
/logs/v1/export/revenue_events.{csv | json}
```

Подробное описание ресурса [в справочнике](ref/revenue_events.md).

Доступные поля:

```no-highlight translate=no
revenue_quantity,revenue_price,revenue_currency,revenue_product_id,revenue_order_id,revenue_order_id_source,is_revenue_verified,is_revenue_autocollected,revenue_inapp_type,revenue_event_type,event_datetime,event_name,event_receive_datetime,event_receive_timestamp,event_timestamp,session_id,installation_id,android_id,appmetrica_device_id,appmetrica_sdk_version,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,event_datetime,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,original_device_model,os_version,profile_id,windows_aid,app_build_number,app_package_name,app_version_name
```

Информация о доходах

#|
|| **Поле** | **Описание** ||
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

Информация о событии и сессии

#|
|| **Поле** | **Описание** ||
|| `event_datetime` | {{ event_datetime }} ||
|| `event_name` | {{ event_name }} ||
|| `event_receive_datetime` | {{ event_receive_datetime }} ||
|| `event_receive_timestamp` | {{ event_receive_timestamp }} ||
|| `event_timestamp` | {{ event_timestamp }} ||
|| `session_id` | {{ session_id }} ||
|| `installation_id` | {{ installation_id }} ||
|#

Информация об устройстве и ОС

#|
|| **Поле** | **Описание** ||
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

Информация о приложении

#|
|| **Поле** | **Описание** ||
|| `app_build_number` | {{ app_build_number }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|#

## Открытия приложения через deeplink {#deeplinks}

```
/logs/v1/export/deeplinks.{csv | json}
```

Подробное описание ресурса [в справочнике](ref/deeplinks.md).

Доступные поля:

```no-highlight translate=no
deeplink_url_host,deeplink_url_parameters,deeplink_url_path,deeplink_url_scheme,event_datetime,event_receive_datetime,event_receive_timestamp,event_timestamp,is_reengagement,profile_id,publisher_id,publisher_name,session_id,tracker_name,tracking_id,android_id,appmetrica_device_id,appmetrica_sdk_version,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,event_datetime,google_aid,ios_ifa,ios_ifv,mcc,mnc,original_device_model,os_version,windows_aid,app_build_number,app_package_name,app_version_name
```

Трекинговая информация

#|
|| **Поле** | **Описание** ||
|| `deeplink_url_host` | {{ deeplink_url_host }} ||
|| `deeplink_url_parameters` | {{ deeplink_url_parameters }} Подробнее о передаче параметров в разделе [Параметры tracking URL](../../mobile-tracking/tracking-specification.md#to-deeplink). ||
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

Информация об устройстве и ОС

#|
|| **Поле** | **Описание** ||
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

Информация о приложении

#|
|| **Поле** | **Описание** ||
|| `app_build_number` | {{ app_build_number }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|#

## Push-токены {#push-tokens}

```
/logs/v1/export/push_tokens.{csv | json}
```

Подробное описание ресурса [в справочнике](ref/push_tokens.md).

Доступные поля:

```no-highlight translate=no
token,token_datetime,token_receive_datetime,token_receive_timestamp,token_timestamp,appmetrica_device_id,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,profile_id,windows_aid,app_package_name,app_version_name,application_id
```

Информация о push-токене

#|
|| **Поле** | **Описание** ||
|| `token` | {{ token }} ||
|| `token_datetime` | {{ token_datetime }} ||
|| `token_receive_datetime` | {{ token_receive_datetime }} ||
|| `token_receive_timestamp` | {{ token_receive_timestamp }} ||
|| `token_timestamp` | {{ token_timestamp }} ||
|#

Информация об устройстве и ОС

#|
|| **Поле** | **Описание** ||
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

Информация о приложении

#|
|| **Поле** | **Описание** ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|| `application_id` | {{ application_id }} ||
|#

## Крэши {#crashes}

```
/logs/v1/export/crashes.{csv | json}
```

Подробное описание ресурса [в справочнике](ref/crashes.md).

Доступные поля:

```no-highlight translate=no
crash,crash_datetime,crash_group_id,crash_id,crash_name,crash_receive_datetime,crash_receive_timestamp,crash_timestamp,appmetrica_device_id,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,profile_id,windows_aid,app_package_name,app_version_name,application_id
```

Информация об аварийной остановке приложения

#|
|| **Поле** | **Описание** ||
|| `crash` | {{ crash }} ||
|| `crash_datetime` | {{ crash_datetime }} ||
|| `crash_group_id` | {{ crash_group_id }} ||
|| `crash_id` | {{ crash_id }} ||
|| `crash_name` | {{ crash_name }} ||
|| `crash_receive_datetime` | {{ crash_receive_datetime }} ||
|| `crash_receive_timestamp` | {{ crash_receive_timestamp }} ||
|| `crash_timestamp` | {{ crash_timestamp }} ||
|#

Информация об устройстве и ОС

#|
|| **Поле** | **Описание** ||
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

Информация о приложении

#|
|| **Поле** | **Описание** ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|| `application_id` | {{ application_id }} ||
|#

## Ошибки {#errors}

```
/logs/v1/export/errors.{csv | json}
```

Подробное описание ресурса [в справочнике](ref/errors.md).

Доступные поля:

```no-highlight translate=no
error,error_datetime,error_id,error_name,error_receive_datetime,error_receive_timestamp,error_timestamp,appmetrica_device_id,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,profile_id,windows_aid,app_package_name,app_version_name,application_id
```

Информация об ошибках приложения

#|
|| **Поле** | **Описание** ||
|| `error` | {{ error }} ||
|| `error_datetime` | {{ error_datetime }} ||
|| `error_id` | {{ error_id }} ||
|| `error_name` | {{ error_name }} ||
|| `error_receive_datetime` | {{ error_receive_datetime }} ||
|| `error_receive_timestamp` | {{ error_receive_timestamp }} ||
|| `error_timestamp` | {{ error_timestamp }} ||
|#

Информация об устройстве и ОС

#|
|| **Поле** | **Описание** ||
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

Информация о приложении

#|
|| **Поле** | **Описание** ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|| `application_id` | {{ application_id }} ||
|#

## Начало сессий {#sessions_starts}

```
/logs/v1/export/sessions_starts.{csv | json}
```

Подробное описание ресурса [в справочнике](ref/sessions_starts.md).

Доступные поля:

```no-highlight translate=no
session_id,session_start_datetime,session_start_receive_datetime,session_start_receive_timestamp,session_start_timestamp,appmetrica_device_id,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,profile_id,windows_aid,app_build_number,app_package_name,app_version_name,application_id
```

Информация о сессиях

#|
|| **Поле** | **Описание** ||
|| `session_id` | {{ session_id }} ||
|| `session_start_datetime` | {{ session_start_datetime }} ||
|| `session_start_receive_datetime` | {{ session_start_receive_datetime }} ||
|| `session_start_receive_timestamp` | {{ session_start_receive_timestamp }} ||
|| `session_start_timestamp` | {{ session_start_timestamp }} ||
|#

Информация об устройстве и ОС

#|
|| **Поле** | **Описание** ||
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
|| **Поле** | **Описание** ||
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

Информация об Ad Revenue

#|
||
**Поле** | **Описание** 
||
||
`ad_revenue_datetime`
|
Дата и время события в формате `yyyy-mm-dd hh:mm:ss`.
||
||
`ad_revenue_timestamp`
|
Время события в формате [UNIX-time](https://en.wikipedia.org/wiki/Unix_time).
||
||
`ad_revenue_receive_datetime`
|
Дата и время получения сервером события. Может отличаться от `ad_revenue_datetime` из-за задержек в сети или отсутствия подключения у пользователя на момент события.
||
||
`ad_revenue_receive_timestamp`
|
Время получения сервером события в формате [UNIX-time](https://en.wikipedia.org/wiki/Unix_time). Может отличаться от `ad_revenue_timestamp` из-за задержек в сети или отсутствия подключения у пользователя на момент события.
||
||
`ad_revenue`
|
Сумма денег Ad Revenue.
||
||
`ad_revenue_currency`
|
Валюта Ad Revenue.
||
||
`ad_revenue_type`
|
Тип Ad Revenue. Возможные значения:

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
Признак [автособранного Ad Revenue](https://appmetrica.yandex.ru/docs/ru/sdk/android/off-adrevenue). Возможные значения:

* `autocollected`
* `manual`

||
||
`ad_revenue_network`
|
Рекламная сеть.
||
||
`ad_revenue_placement_id`
|
ID расположения рекламы.
||
||
`ad_revenue_placement_name`
|
Название расположения рекламы.
||
||
`ad_revenue_unit_id`
|
ID рекламной единицы.
||
||
`ad_revenue_unit_name`
|
Название рекламной единицы.
||
||
`ad_revenue_precision`
|
Точность суммы Ad Revenue, как передано в SDK. Например, "publisher_defined" или "estimated".
||
||
`ad_revenue_payload`
|
Дополнительные данные, сериализованные в JSON.
||
|#

Информация о событии и сессии

#|
|| **Поле** | **Описание** ||
|| `session_id` | {{ session_id }} ||
|| `installation_id` | {{ installation_id }} ||
|#

Информация об устройстве и ОС

#|
|| **Поле** | **Описание** ||
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

Информация о приложении

#|
|| **Поле** | **Описание** ||
|| `app_build_number` | {{ app_build_number }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|#

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
