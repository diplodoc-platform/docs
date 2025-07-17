# E-commerce

{{ ecommerce_events }}

## Формат запроса {#request-format}

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
|| `fields`* | Разделенный запятой [список полей](../endpoints.md) для выборки.

Список, который содержит все доступные поля (для быстрого копирования):

```objectivec translate=no
ecom_type,ecom_screen_name,ecom_screen_search_query,ecom_screen_payload,ecom_screen_category_path_1,ecom_screen_category_path_2,ecom_screen_category_path_3,ecom_screen_category_path_4,ecom_screen_category_path_5,ecom_screen_category_path_6,ecom_screen_category_path_7,ecom_screen_category_path_8,ecom_screen_category_path_9,ecom_screen_category_path_10,ecom_product_name,ecom_product_sku,ecom_product_promocodes,ecom_product_payload,ecom_product_category_path_1,ecom_product_category_path_2,ecom_product_category_path_3,ecom_product_category_path_4,ecom_product_category_path_5,ecom_product_category_path_6,ecom_product_category_path_7,ecom_product_category_path_8,ecom_product_category_path_9,ecom_product_category_path_10,ecom_product_actual_price_fiat_unit_type,ecom_product_actual_price_fiat_value,ecom_product_actual_price_internal_components,ecom_product_original_price_fiat_unit_type,ecom_product_original_price_fiat_value,ecom_product_original_price_internal_components,ecom_cart_item_price_fiat_unit_type,ecom_cart_item_price_fiat_value,ecom_cart_item_quantity,ecom_cart_item_internal_components,ecom_referrer_type,ecom_referrer_id,ecom_order_id,ecom_order_payload,event_datetime,event_name,event_receive_datetime,event_receive_timestamp,event_timestamp,session_id,installation_id,android_id,appmetrica_device_id,appmetrica_sdk_version,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,event_datetime,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,original_device_model,os_version,profile_id,windows_aid,app_build_number,app_package_name,app_version_name
```
||
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

## Пример {#example}

Запрос:

```bash translate=no
curl -X GET \
  'https://api.appmetrica.yandex.ru/logs/v1/export/ecommerce_events.json?application_id=2421017&date_since=2023-01-04+00%3A00%3A00&date_until=2023-01-04+23%3A59%3A59&date_dimension=receive&use_utf8_bom=true&fields=ecom_type,ecom_screen_name,ecom_screen_search_query,ecom_screen_payload,ecom_screen_category_path_1,ecom_screen_category_path_2,ecom_screen_category_path_3,ecom_screen_category_path_4,ecom_screen_category_path_5,ecom_screen_category_path_6,ecom_screen_category_path_7,ecom_screen_category_path_8,ecom_screen_category_path_9,ecom_screen_category_path_10,ecom_product_name,ecom_product_sku,ecom_product_promocodes,ecom_product_payload,ecom_product_category_path_1,ecom_product_category_path_2,ecom_product_category_path_3,ecom_product_category_path_4,ecom_product_category_path_5,ecom_product_category_path_6,ecom_product_category_path_7,ecom_product_category_path_8,ecom_product_category_path_9,ecom_product_category_path_10,ecom_product_actual_price_fiat_unit_type,ecom_product_actual_price_fiat_value,ecom_product_actual_price_internal_components,ecom_product_original_price_fiat_unit_type,ecom_product_original_price_fiat_value,ecom_product_original_price_internal_components,ecom_cart_item_price_fiat_unit_type,ecom_cart_item_price_fiat_value,ecom_cart_item_quantity,ecom_cart_item_internal_components,ecom_referrer_type,ecom_referrer_id,ecom_order_id,ecom_order_payload,event_datetime,event_json,event_name,event_receive_datetime,event_receive_timestamp,event_timestamp,session_id,installation_id,appmetrica_device_id,city,connection_type,country_iso_code,device_ipv6,device_locale,device_manufacturer,device_model,device_type,google_aid,ios_ifa,ios_ifv,mcc,mnc,operator_name,original_device_model,os_name,os_version,profile_id,windows_aid,app_build_number,app_package_name,app_version_name,application_id' \
  -H 'Authorization: OAuth oauth_token'
```

Ответ:

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

### См. также

- [Как определить источник события по сырым данным?](../../../troubleshooting/troubleshooting.md#raw-data)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}

