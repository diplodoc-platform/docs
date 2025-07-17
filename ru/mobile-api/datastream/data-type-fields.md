# Типы данных для экспорта

## Установки приложения [installation] {#installations}

Доступные поля:

```no-highlight translate=no
application_id,attributed_touch_type,click_datetime,click_id,click_ipv6,click_timestamp,click_url_parameters,click_user_agent,profile_id,publisher_id,publisher_name,tracker_name,tracking_id,installation_id,certificate_verification_status,fraud_status,version,sign,install_datetime,install_ipv6,install_receive_datetime,install_receive_timestamp,install_timestamp,is_reattribution,is_reinstallation,match_type,appmetrica_device_id,appmetrica_sdk_version,country,district,area,city,connection_type,country_iso_code,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,windows_aid,huawei_oaid,app_build_number,app_package_name,app_version_name
```

Трекинговая информация

#|
|| **Поле** | **Описание** ||
|| `attributed_touch_type` | {{ attributed_touch_type }} ||
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
|#

Информация об установке

#|
|| **Поле** | **Описание** ||
|| `app_installer` | {{ app_installer }} ||
|| `certificate_verification_status` | {{ certificate_verification_status }} ||
|| `fraud_status` | {{ fraud_status }} ||
|| `install_datetime` | {{ install_datetime }} ||
|| `install_ipv6` | {{ install_ipv6 }} ||
|| `install_receive_datetime` | {{ install_receive_datetime }} ||
|| `install_receive_timestamp` | {{ install_receive_timestamp }} ||
|| `install_timestamp` | {{ install_timestamp }} ||
|| `installation_id` | {{ installation_id }} ||
|| `is_reattribution` | {{ is_reattribution }} ||
|| `is_reinstallation` | {{ is_reinstallation }} ||
|| `match_type` | [Способ атрибуции](../../mobile-tracking/technology.md): `fingerprint` \| `referrer` \| `identifier` \| `''` (пустая строка). ||
|| `sign` | {{ event_sign }} Например, одно обновление установки с изменением `fraud_status` будет представлено тремя записями в экспорте, а сумма `sign` равна 1 (одна реальная установка):

```
installation_id           sign   version   fraud_status
0c08ef45-...-fc43f0c989c3   1       1        unknown
0c08ef45-...-fc43f0c989c3  -1       1        unknown
0c08ef45-...-fc43f0c989c3   1       2          high
```

||
|| `version` | {{ event_version }} ||
|#

Информация об устройстве и ОС

#|
|| **Поле** | **Описание** ||
|| `appmetrica_device_id` | {{ appmetrica_device_id }} ||
|| `appmetrica_sdk_version` | {{ appmetrica_sdk_version }} ||
|| `area` | {{ area }} ||
|| `city` | {{ city }} ||
|| `connection_type` | {{ connection_type }} ||
|| `country` | {{ country }} ||
|| `country_iso_code` | {{ country_iso_code }} ||
|| `device_locale` | {{ device_locale }} ||
|| `device_manufacturer` | {{ device_manufacturer }} ||
|| `device_model` | {{ device_model }} ||
|| `device_type` | {{ device_type }} ||
|| `district` | {{ district }} ||
|| `google_aid` | {{ google_aid }} ||
|| `huawei_oaid` | {{ huawei_oaid }} ||
|| `ios_ifa` | {{ ios_ifa }} ||
|| `ios_ifv` | {{ ios_ifv }} ||
|| `mcc` | {{ mcc }} ||
|| `mnc` | {{ mnc }} ||
|| `operator_name` | {{ operator_name }} ||
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

## События приложения [event] {#events}

Доступные поля:

```no-highlight translate=no
android_id,app_build_number,app_package_name,app_version_name,application_id,appmetrica_device_id,appmetrica_sdk_version,country,district,area,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,event_source,event_datetime,event_json,event_name,event_receive_datetime,event_receive_timestamp,event_timestamp,google_aid,installation_id,testids,certificate_verification_status,ios_ifa,ios_ifv,mcc,mnc,operator_name,original_device_model,os_name,os_version,profile_id,session_id,session_type,windows_aid,huawei_oaid
```

Информация о событии и сессии

#|
|| **Поле** | **Описание** ||
|| `certificate_verification_status` | {{ certificate_verification_status }} ||
|| `event_datetime` | {{ event_datetime }} ||
|| `event_json` | {{ event_json }} ||
|| `event_name` | {{ event_name }} ||
|| `event_receive_datetime` | {{ event_receive_datetime }} ||
|| `event_receive_timestamp` | {{ event_receive_timestamp }} ||
|| `event_timestamp` | {{ event_timestamp }} ||
|| `session_id` | {{ session_id }} ||
|| `session_type` | {{ session_type }} ||
|| `installation_id` | {{ installation_id }} ||
|| `testids` | {{ testids }} ||
|#

Информация об устройстве и ОС

#|
|| **Поле** | **Описание** ||
|| `appmetrica_device_id` | {{ appmetrica_device_id }} ||
|| `appmetrica_sdk_version` | {{ appmetrica_sdk_version }} ||
|| `area` | {{ area }} ||
|| `city` | {{ city }} ||
|| `connection_type` | {{ connection_type }} ||
|| `country` | {{ country }} ||
|| `country_iso_code` | {{ country_iso_code }} ||
|| `device_ipv6` | {{ device_ipv6 }} ||
|| `device_locale` | {{ device_locale }} ||
|| `device_manufacturer` | {{ device_manufacturer }} ||
|| `device_model` | {{ device_model }} ||
|| `device_type` | {{ device_type }} ||
|| `district` | {{ district }} ||
|| `event_source` | {{ event_source }} ||
|| `google_aid` | {{ google_aid }} ||
|| `huawei_oaid` | {{ huawei_oaid }} ||
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

## Push-токены [push_token] {#push-tokens}

Доступные поля:

```no-highlight translate=no
token,token_datetime,token_receive_datetime,token_receive_timestamp,token_timestamp,session_id,session_type,installation_id,certificate_verification_status,appmetrica_device_id,appmetrica_sdk_version,country,district,area,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,event_source,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,profile_id,windows_aid,huawei_oaid,app_package_name,app_version_name,application_id
```

Информация о push-токене

#|
|| **Поле** | **Описание** ||
|| `certificate_verification_status` | {{ certificate_verification_status }} ||
|| `installation_id` | {{ installation_id }} ||
|| `token` | {{ token }} ||
|| `token_datetime` | {{ token_datetime }} ||
|| `token_receive_datetime` | {{ token_receive_datetime }} ||
|| `token_receive_timestamp` | {{ token_receive_timestamp }} ||
|| `token_timestamp` | {{ token_timestamp }} ||
|| `session_id` | {{ session_id }} ||
|| `session_type` | {{ session_type }} ||
|#

Информация об устройстве и ОС

#|
|| **Поле** | **Описание** ||
|| `appmetrica_device_id` | {{ appmetrica_device_id }} ||
|| `appmetrica_sdk_version` | {{ appmetrica_sdk_version }} ||
|| `area` | {{ area }} ||
|| `city` | {{ city }} ||
|| `connection_type` | {{ connection_type }} ||
|| `country` | {{ country }} ||
|| `country_iso_code` | {{ country_iso_code }} ||
|| `device_ipv6` | {{ device_ipv6 }} ||
|| `device_locale` | {{ device_locale }} ||
|| `device_manufacturer` | {{ device_manufacturer }} ||
|| `device_model` | {{ device_model }} ||
|| `device_type` | {{ device_type }} ||
|| `district` | {{ district }} ||
|| `event_source` | {{ event_source }} ||
|| `google_aid` | {{ google_aid }} ||
|| `huawei_oaid` | {{ huawei_oaid }} ||
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

## Крэши [crash] {#crashes}

Доступные поля:

```no-highlight translate=no
crash,crash_datetime,crash_group_id,crash_id,crash_name,crash_receive_datetime,crash_receive_timestamp,crash_timestamp,session_id,session_type,installation_id,certificate_verification_status,appmetrica_device_id,appmetrica_sdk_version,country,district,area,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,event_source,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,profile_id,windows_aid,huawei_oaid,app_package_name,app_version_name,application_id
```

Информация об аварийной остановке приложения

#|
|| **Поле** | **Описание** ||
|| `certificate_verification_status` | {{ certificate_verification_status }} ||
|| `crash` | {{ crash }} ||
|| `crash_datetime` | {{ crash_datetime }} ||
|| `crash_group_id` | {{ crash_group_id }} ||
|| `crash_id` | {{ crash_id }} ||
|| `crash_name` | {{ crash_name }} ||
|| `crash_receive_datetime` | {{ crash_receive_datetime }} ||
|| `crash_receive_timestamp` | {{ crash_receive_timestamp }} ||
|| `crash_timestamp` | {{ crash_timestamp }} ||
|| `installation_id` | {{ installation_id }} ||
|| `session_id` | {{ session_id }} ||
|| `session_type` | {{ session_type }} ||
|#

Информация об устройстве и ОС

#|
|| **Поле** | **Описание** ||
|| `appmetrica_device_id` | {{ appmetrica_device_id }} ||
|| `appmetrica_sdk_version` | {{ appmetrica_sdk_version }} ||
|| `area` | {{ area }} ||
|| `city` | {{ city }} ||
|| `connection_type` | {{ connection_type }} ||
|| `country` | {{ country }} ||
|| `country_iso_code` | {{ country_iso_code }} ||
|| `device_ipv6` | {{ device_ipv6 }} ||
|| `device_locale` | {{ device_locale }} ||
|| `device_manufacturer` | {{ device_manufacturer }} ||
|| `device_model` | {{ device_model }} ||
|| `device_type` | {{ device_type }} ||
|| `district` | {{ district }} ||
|| `event_source` | {{ event_source }} ||
|| `google_aid` | {{ google_aid }} ||
|| `huawei_oaid` | {{ huawei_oaid }} ||
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

## Ошибки [error] {#errors}

Доступные поля:

```no-highlight translate=no
error,error_datetime,error_id,error_name,error_receive_datetime,error_receive_timestamp,error_timestamp,session_id,session_type,installation_id,certificate_verification_status,appmetrica_device_id,appmetrica_sdk_version,country,district,area,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,event_source,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,profile_id,windows_aid,huawei_oaid,app_package_name,app_version_name,application_id
```

Информация об ошибках приложения

#|
|| **Поле** | **Описание** ||
|| `certificate_verification_status` | {{ certificate_verification_status }} ||
|| `installation_id` | {{ installation_id }} ||
|| `error` | {{ error }} ||
|| `error_datetime` | {{ error_datetime }} ||
|| `error_id` | {{ error_id }} ||
|| `error_name` | {{ error_name }} ||
|| `error_receive_datetime` | {{ error_receive_datetime }} ||
|| `error_receive_timestamp` | {{ error_receive_timestamp }} ||
|| `error_timestamp` | {{ error_timestamp }} ||
|| `session_id` | {{ session_id }} ||
|| `session_type` | {{ session_type }} ||
|#

Информация об устройстве и ОС

#|
|| **Поле** | **Описание** ||
|| `appmetrica_device_id` | {{ appmetrica_device_id }} ||
|| `appmetrica_sdk_version` | {{ appmetrica_sdk_version }} ||
|| `area` | {{ area }} ||
|| `city` | {{ city }} ||
|| `connection_type` | {{ connection_type }} ||
|| `country` | {{ country }} ||
|| `country_iso_code` | {{ country_iso_code }} ||
|| `device_ipv6` | {{ device_ipv6 }} ||
|| `device_locale` | {{ device_locale }} ||
|| `device_manufacturer` | {{ device_manufacturer }} ||
|| `device_model` | {{ device_model }} ||
|| `device_type` | {{ device_type }} ||
|| `district` | {{ district }} ||
|| `event_source` | {{ event_source }} ||
|| `google_aid` | {{ google_aid }} ||
|| `huawei_oaid` | {{ huawei_oaid }} ||
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

## Начало сессий [session_start] {#sessions_starts}

Доступные поля:

```no-highlight translate=no
session_id,session_type,session_start_datetime,session_start_receive_datetime,session_start_receive_timestamp,session_start_timestamp,installation_id,certificate_verification_status,appmetrica_device_id,appmetrica_sdk_version,country,district,area,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,event_source,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,original_device_model,os_name,os_version,profile_id,windows_aid,huawei_oaid,app_build_number,app_package_name,app_version_name,application_id
```

Информация о сессиях

#|
|| **Поле** | **Описание** ||
|| `certificate_verification_status` | {{ certificate_verification_status }} ||
|| `installation_id` | {{ installation_id }} ||
|| `session_id` | {{ session_id }} ||
|| `session_type` | {{ session_type }} ||
|| `session_start_datetime` | {{ session_start_datetime }} ||
|| `session_start_receive_datetime` | {{ session_start_receive_datetime }} ||
|| `session_start_receive_timestamp` | {{ session_start_receive_timestamp }} ||
|| `session_start_timestamp` | {{ session_start_timestamp }} ||
|#

Информация об устройстве и ОС

#|
|| **Поле** | **Описание** ||
|| `appmetrica_device_id` | {{ appmetrica_device_id }} ||
|| `appmetrica_sdk_version` | {{ appmetrica_sdk_version }} ||
|| `area` | {{ area }} ||
|| `city` | {{ city }} ||
|| `country` | {{ country }} ||
|| `connection_type` | {{ connection_type }} ||
|| `country_iso_code` | {{ country_iso_code }} ||
|| `device_ipv6` | {{ device_ipv6 }} ||
|| `device_locale` | {{ device_locale }} ||
|| `device_manufacturer` | {{ device_manufacturer }} ||
|| `device_model` | {{ device_model }} ||
|| `device_type` | {{ device_type }} ||
|| `district` | {{ district }} ||
|| `event_source` | {{ event_source }} ||
|| `google_aid` | {{ google_aid }} ||
|| `huawei_oaid` | {{ huawei_oaid }} ||
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

Информация о приложении

#|
|| **Поле** | **Описание** ||
|| `app_build_number` | {{ app_build_number }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|| `application_id` | {{ application_id }} ||
|#

## Завершение сессий [session_end] {#session_end}

Доступные поля:

```no-highlight translate=no
session_id,session_type,session_end_datetime,session_end_receive_datetime,session_end_receive_timestamp,session_end_timestamp,installation_id,certificate_verification_status,appmetrica_device_id,appmetrica_sdk_version,country,district,area,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,event_source,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,original_device_model,os_name,os_version,profile_id,windows_aid,huawei_oaid,app_build_number,app_package_name,app_version_name,application_id
```

Информация о сессиях

#|
|| **Поле** | **Описание** ||
|| `certificate_verification_status` | {{ certificate_verification_status }} ||
|| `installation_id` | {{ installation_id }} ||
|| `session_id` | {{ session_id }} ||
|| `session_type` | {{ session_type }} ||
|| `session_end_datetime` | {{ session_end_datetime }} ||
|| `session_end_receive_datetime` | {{ session_end_receive_datetime }} ||
|| `session_end_receive_timestamp` | {{ session_end_receive_timestamp }} ||
|| `session_end_timestamp` | {{ session_end_timestamp }} ||
|#

Информация об устройстве и ОС

#|
|| **Поле** | **Описание** ||
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
|| `google_aid` | {{ google_aid }} ||
|| `huawei_oaid` | {{ huawei_oaid }} ||
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

Информация о приложении

#|
|| **Поле** | **Описание** ||
|| `app_build_number` | {{ app_build_number }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|| `application_id` | {{ application_id }} ||
|#

## Клики и показы [click] {#click}

Доступные поля:

```no-highlight translate=no
application_id,click_datetime,click_id,click_ipv6,click_timestamp,click_url_parameters,click_user_agent,publisher_id,publisher_name,tracker_name,tracking_id,touch_type,is_bot,country,district,area,city,country_iso_code,device_type,device_model,device_manufacturer,os_version,os_name,windows_aid,huawei_oaid,google_aid,ios_ifv,ios_ifa
```

Данные о трекинговых кликах и показах

#|
|| **Поле** | **Описание** ||
|| `application_id` | {{ application_id }} ||
|| `area` | {{ area }} ||
|| `city` | {{ city_click }} ||
|| `click_datetime` | {{ click_datetime }} ||
|| `click_id` | {{ click_id }} ||
|| `click_ipv6` | {{ click_ipv6 }} ||
|| `click_timestamp` | {{ click_timestamp }} ||
|| `click_url_parameters` | {{ click_url_parameters }} ||
|| `click_user_agent` | {{ click_user_agent }} ||
|| `country` | {{ country }} ||
|| `country_iso_code` | {{ country_iso_code }} ||
|| `device_type` | {{ device_type }} ||
|| `device_model` | {{ device_model }} ||
|| `device_manufacturer` | {{ device_manufacturer }} ||
|| `district` | {{ district }} ||
|| `google_aid` | {{ google_aid }} ||
|| `huawei_oaid` | {{ huawei_oaid }} ||
|| `ios_ifv` | {{ ios_ifv }} ||
|| `ios_ifa` | {{ ios_ifa }} ||
|| `is_bot` | {{ is_bot }} ||
|| `os_version` | {{ os_version}} ||
|| `os_name` | {{ os_name }} ||
|| `publisher_id` | {{ publisher_id }} ||
|| `publisher_name` | {{ publisher_name }} ||
|| `tracker_name` | {{ tracker_name }} ||
|| `tracking_id` | {{ tracking_id }} ||
|| `touch_type` | {{ touch_type }} ||
|| `windows_aid` | {{ windows_aid }} ||
|#

## Revenue [revenue] {#revenue}

Доступные поля:

```no-highlight translate=no
revenue_quantity,revenue_price,revenue_currency,revenue_product_id,revenue_order_id,revenue_order_id_source,is_revenue_verified,is_revenue_autocollected,revenue_inapp_type,revenue_event_type,event_datetime,event_name,event_receive_datetime,event_receive_timestamp,event_timestamp,session_id,installation_id,certificate_verification_status,android_id,appmetrica_device_id,appmetrica_sdk_version,country,district,area,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,event_source,event_datetime,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,original_device_model,os_version,profile_id,windows_aid,app_build_number,app_package_name,app_version_name
```

Информация о доходах

#|
|| **Поле** | **Описание** ||
|| `is_revenue_verified` | {{ is_revenue_verified }} ||
|| `is_revenue_autocollected` | {{ is_revenue_autocollected }} ||
|| `revenue_quantity` | {{ revenue_quantity }} ||
|| `revenue_price` | {{ revenue_price }} ||
|| `revenue_currency` | {{ revenue_currency }} ||
|| `revenue_product_id` | {{ revenue_product_id }} ||
|| `revenue_order_id` | {{ revenue_order_id }} ||
|| `revenue_order_id_source` | {{ revenue_order_id_source }} ||
|| `revenue_inapp_type` | {{ revenue_inapp_type }} ||
|| `revenue_event_type` | {{ revenue_event_type }} ||
|#

Информация о событии и сессии

#|
|| **Поле** | **Описание** ||
|| `certificate_verification_status` | {{ certificate_verification_status }} ||
|| `event_datetime` | {{ event_datetime }} ||
|| `event_name` | {{ event_name }} ||
|| `event_receive_datetime` | {{ event_receive_datetime }} ||
|| `event_receive_timestamp` | {{ event_receive_timestamp }} ||
|| `event_timestamp` | {{ event_timestamp }} ||
|| `installation_id` | {{ installation_id }} ||
|| `session_id` | {{ session_id }} ||
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
|| `huawei_oaid` | {{ huawei_oaid }} ||
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

## Покупки [ecommerce] {#ecommerce}

Позволяет выгрузить данные, переданные через вызов `reportECommerce` (см. [Android](../../sdk/android/analytics/android-operations#send-ecommerce) и [iOS](../../sdk/ios/analytics/ios-operations#send-ecommerce)). Один вызов `reportECommerce` может быть представлен несколькими событиями в экспорте (см. поле `ecom_type`).

Доступные поля:

```no-hihglight translate=no
ecom_type,ecom_screen_name,ecom_screen_search_query,ecom_screen_payload,ecom_screen_category_path_1,ecom_screen_category_path_2,ecom_screen_category_path_3,ecom_screen_category_path_4,ecom_screen_category_path_5,ecom_screen_category_path_6,ecom_screen_category_path_7,ecom_screen_category_path_8,ecom_screen_category_path_9,ecom_screen_category_path_10,ecom_product_name,ecom_product_sku,ecom_product_promocodes,ecom_product_payload,ecom_product_category_path_1,ecom_product_category_path_2,ecom_product_category_path_3,ecom_product_category_path_4,ecom_product_category_path_5,ecom_product_category_path_6,ecom_product_category_path_7,ecom_product_category_path_8,ecom_product_category_path_9,ecom_product_category_path_10,ecom_product_actual_price_fiat_unit_type,ecom_product_actual_price_fiat_value,ecom_product_actual_price_internal_components,ecom_product_original_price_fiat_unit_type,ecom_product_original_price_fiat_value,ecom_product_original_price_internal_components,ecom_cart_item_price_fiat_unit_type,ecom_cart_item_price_fiat_value,ecom_cart_item_quantity,ecom_cart_item_internal_components,ecom_referrer_type,ecom_referrer_id,ecom_order_id,ecom_order_payload,event_datetime,event_name,event_receive_datetime,event_receive_timestamp,event_timestamp,session_id,installation_id,certificate_verification_status,android_id,appmetrica_device_id,appmetrica_sdk_version,country,district,area,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,event_source,event_datetime,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,original_device_model,os_version,profile_id,windows_aid,app_build_number,app_package_name,app_version_name
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
|| `huawei_oaid` | {{ huawei_oaid }} ||
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

## Ad Revenue [ad_revenue] {#ad_revenue}

Доступные поля:

```no-highlight translate=no
ad_revenue_datetime,ad_revenue_timestamp,ad_revenue_receive_datetime,ad_revenue_receive_timestamp,ad_revenue,ad_revenue_currency,ad_revenue_type,ad_revenue_data_source,ad_revenue_network,ad_revenue_placement_id,ad_revenue_placement_name,ad_revenue_unit_id,ad_revenue_unit_name,ad_revenue_precision,ad_revenue_payload,session_id,installation_id,certificate_verification_status,android_id,appmetrica_device_id,appmetrica_sdk_version,country,district,area,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,event_source,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,original_device_model,os_version,profile_id,windows_aid,app_build_number,app_package_name,app_version_name
```

Информация об Ad Revenue

#|
|| **Поле** | **Описание** || 
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
|#

Информация о событии и сессии

#|
|| **Поле** | **Описание** ||
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

## Конверсии [attributed_event] {#attributed_event}

Позволяет выгрузить события различных типов, атрибутированные источникам трафика согласно выбранной модели атрибуции `event_attribution` в [настройках Data Stream](ref/settings-post.md).

*Beta*: конверсии как тип данных находятся в стадии разработки и в будущем могут быть расширены новыми возможными значениями полей. На текущий момент правила конверсий автоматически создаются вместе с настройкой отправки постбеков в трекерах.

Доступные поля:

```no-highlight translate=no
ad_revenue,ad_revenue_currency,ad_revenue_data_source,ad_revenue_datetime,ad_revenue_network,ad_revenue_payload,ad_revenue_placement_id,ad_revenue_placement_name,ad_revenue_precision,ad_revenue_receive_datetime,ad_revenue_receive_timestamp,ad_revenue_timestamp,ad_revenue_type,ad_revenue_unit_id,ad_revenue_unit_name,android_id,app_build_number,app_framework,app_package_name,app_version_name,application_id,appmetrica_device_id,appmetrica_sdk_version,area,attributed_event_type,attributed_touch_type,certificate_verification_status,city,click_date,click_datetime,click_id,click_ipv6,click_timestamp,click_url_parameters,click_user_agent,connection_type,conversion_attribution_window_size,conversion_id,conversion_name,country,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,district,ecom_cart_item_internal_components,ecom_cart_item_price_fiat_unit_type,ecom_cart_item_price_fiat_value,ecom_cart_item_quantity,ecom_order_id,ecom_order_payload,ecom_product_actual_price_fiat_unit_type,ecom_product_actual_price_fiat_value,ecom_product_actual_price_internal_components,ecom_product_category_path_1,ecom_product_category_path_10,ecom_product_category_path_2,ecom_product_category_path_3,ecom_product_category_path_4,ecom_product_category_path_5,ecom_product_category_path_6,ecom_product_category_path_7,ecom_product_category_path_8,ecom_product_category_path_9,ecom_product_name,ecom_product_original_price_fiat_unit_type,ecom_product_original_price_fiat_value,ecom_product_original_price_internal_components,ecom_product_payload,ecom_product_promocodes,ecom_product_sku,ecom_referrer_id,ecom_referrer_type,ecom_screen_category_path_1,ecom_screen_category_path_10,ecom_screen_category_path_2,ecom_screen_category_path_3,ecom_screen_category_path_4,ecom_screen_category_path_5,ecom_screen_category_path_6,ecom_screen_category_path_7,ecom_screen_category_path_8,ecom_screen_category_path_9,ecom_screen_name,ecom_screen_payload,ecom_screen_search_query,ecom_type,event_attribution_model,event_date,event_datetime,event_initial_event_type,event_json,event_name,event_receive_datetime,event_receive_timestamp,event_source,event_timestamp,google_aid,huawei_oaid,installation_id,ios_ifa,ios_ifv,is_reattribution,is_reinstallation,is_revenue_autocollected,is_revenue_verified,match_type,mcc,mnc,operator_name,original_device_model,os_name,os_version,profile_id,publisher_id,publisher_name,revenue_currency,revenue_event_type,revenue_inapp_type,revenue_order_id,revenue_order_id_source,revenue_price,revenue_product_id,revenue_quantity,session_id,session_type,sign,testids,touch_type,tracker_name,tracking_id,version,windows_aid
```

Информация о конверсии. Значения зависят от модели атрибуции.

#|
|| **Поле** | **Описание** ||
|| `attributed_event_type` | {{ attributed_event_type }} ||
|| `event_attribution_model` | {{ event_attribution_model }} ||
|| `event_initial_event_type` | {{ event_initial_event_type }} ||
|| `conversion_id` | {{ conversion_id }} ||
|| `conversion_name` | {{ conversion_name }} ||
|| `conversion_attribution_window_size` | {{ conversion_attribution_window_size }} ||
|#

Трекинговая информация. Значения зависят от модели атрибуции.

#|
|| **Поле** | **Описание** ||
|| `attributed_touch_type` | {{ attributed_touch_type }} ||
|| `click_datetime` | {{ click_datetime }} ||
|| `click_id` | {{ click_id }} ||
|| `click_ipv6` | {{ click_ipv6 }} ||
|| `click_timestamp` | {{ click_timestamp }} ||
|| `click_url_parameters` | {{ click_url_parameters }} ||
|| `click_user_agent` | {{ click_user_agent }} ||
|| `publisher_id` | {{ publisher_id }} ||
|| `publisher_name` | {{ publisher_name }} ||
|| `tracking_id` | {{ tracking_id }} ||
|| `tracker_name` | {{ tracker_name }} ||
|# 

## Открытия приложения через deeplink [deeplink] {#deeplinks}

Доступные поля:

```
deeplink_url_host,deeplink_url_parameters,deeplink_url_path,deeplink_url_scheme,event_datetime,event_receive_datetime,event_receive_timestamp,event_timestamp,is_reengagement,profile_id,publisher_id,publisher_name,session_id,tracker_name,tracking_id,android_id,appmetrica_device_id,appmetrica_sdk_version,country,district,area,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,event_datetime,google_aid,ios_ifa,ios_ifv,mcc,mnc,original_device_model,os_version,windows_aid,huawei_oaid,app_build_number,app_package_name,app_version_name,installation_id,certificate_verification_status
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
|| `area` | {{ area }} ||
|| `certificate_verification_status` | {{ certificate_verification_status }} ||
|| `city` | {{ city }} ||
|| `connection_type` | {{ connection_type }} ||
|| `country` | {{ country }} ||
|| `country_iso_code` | {{ country_iso_code }} ||
|| `device_ipv6` | {{ device_ipv6 }} ||
|| `device_locale` | {{ device_locale }} ||
|| `device_manufacturer` | {{ device_manufacturer }} ||
|| `device_model` | {{ device_model }} ||
|| `device_type` | {{ device_type }} ||
|| `district` | {{ district }} ||
|| `google_aid` | {{ google_aid }} ||
|| `huawei_oaid` | {{ huawei_oaid }} ||
|| `installation_id` | {{ installation_id }} ||
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

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
