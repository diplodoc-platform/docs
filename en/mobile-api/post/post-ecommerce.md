# Uploading E-commerce events

Transmits data about E-commerce events.

Usage example: You can transmit all E-commerce events via the Post API to collect data about user purchases in one place, including those made in the app, offline store, or on a website.

Event properties can be passed in parameters or in the body of the request. When you pass data in the body, you should add `.csv` to the URL of the request. For more information, see [Sample request](#sample).

To bind an event to a user, you should use one of the following fields in the API request:

- `profile_id`
- `appmetrica_device_id`

{% note alert %}

The Post API has restrictions on loading data. For more information, see [Restrictions](restrictions.md).

{% endnote %}

## Request format

```
POST {{ api-url }}/logs/v1/import/ecommerce
  ? post_api_key=<string>
  & application_id=<int>
  & profile_id=<string>
  & appmetrica_device_id=<int>
  & event_timestamp=<int>
  & ecom_event_type=<string>
  & order_id=<string>
  & product_name=<string>
  & cart_item_quantity=<int>
  & [cart_item_price_currency=<string>]
  & [cart_item_price_value=<int>]
  & [cart_item_price_internal_currency=<array>]
  & [cart_item_price_internal_value=<array>]
  & [actual_price_currency=<string>]
  & [actual_price_value=<int>]
  & [actual_price_internal_currency=<array>]
  & [actual_price_internal_value=<array>]
  & [payload=<string>]
  & [product_category_path_1=<string>]
  & [product_category_path_2=<string>]
  & [product_category_path_3=<string>]
  & [product_category_path_4=<string>]
  & [product_category_path_5=<string>]
  & [product_category_path_6=<string>]
  & [product_category_path_7=<string>]
  & [product_category_path_8=<string>]
  & [product_category_path_9=<string>]
  & [product_category_path_10=<string>]
  & original_price_currency=<string>
  & original_price_value=<int>
  & [original_price_internal_currency=<array>]
  & [original_price_internal_value=<array>]
  & [product_payload=<string>]
  & [product_promo_codes=<array>]
  & [product_sku=<string>]
  & [screen_category_path_1=<string>]
  & [screen_category_path_2=<string>]
  & [screen_category_path_3=<string>]
  & [screen_category_path_4=<string>]
  & [screen_category_path_5=<string>]
  & [screen_category_path_6=<string>]
  & [screen_category_path_7=<string>]
  & [screen_category_path_8=<string>]
  & [screen_category_path_9=<string>]
  & [screen_category_path_10=<string>]
  & [screen_name=<string>]
  & [screen_payload=<string>]
  & [session_type=<string>]
  & [ios_ifa=<string>]
  & [ios_ifv=<string>]
  & [google_aid=<string>]
  & [windows_aid=<string>]
  & [os_name=<string>]
  & [os_version=<string>]
  & [device_manufacturer=<string>]
  & [device_model=<string>]
  & [device_type=<string>]
  & [device_locale=<string>]
  & [app_version_name=<string>]
  & [app_package_name=<string>]
  & [connection_type=<string>]
  & [operator_name=<string>]
  & [mcc=<int>]
  & [mnc=<int>]
  & [device_ipv6=<string>]
```

#|
|| `post_api_key`* | {{ post_api_key }} ||
|| `application_id`* | {{ application_id }} ||
|| `profile_id`* | {{ post-profile_id }}

{% note alert %}

Do not pass the value with the `appmetrica_device_id` parameter. The server accepts only one of these parameters.

{% endnote %}

||
|| `appmetrica_device_id`* | {{ post-appmetrica_device_id }}

{% note alert %}

Do not pass the value with the `profile_id` parameter. The server accepts only one of these parameters.

{% endnote %}

||
|| `event_timestamp`* | {{ event_timestamp }} ||
|| `ecom_event_type`* | {{ post-ecom_event_type }} ||
|| `order_id`* | {{ revenue_order_id }} ||
|| `product_name`* | {{ post-product_name }} ||
|| `cart_item_quantity`* | The number of items in the cart. ||
|| `cart_item_price_currency` | The price currency of the product in the cart. If omitted, the `actual_price_currency` value is used. [List of available currencies](../../data-collection/currency-codes.md). ||
|| `cart_item_price_value` | The price of the product in the cart. This is the final price, including all promotions, promo codes, bonus points, and other discounts that the user applied. If omitted, the `actual_price_value` value is used.||
|| `cart_item_price_internal_currency` | The internal currency type for the product in the cart. If omitted, the `actual_price_internal_currency` value is used. ||
|| `cart_item_price_internal_value` | The price of the product in the cart specified in the internal currency. This is the final price, including all promotions, promo codes, bonus points, and other discounts that the user applied. If omitted, the `actual_price_internal_value` value is used. ||
|| `actual_price_currency` | The currency of the actual product price. If omitted, the `original_price_currency` value is used. [List of available currencies](../../data-collection/currency-codes.md). ||
|| `actual_price_value` | Actual product price. This is the current product price, including discounts. If omitted, the `original_price_value` value is used. ||
|| `actual_price_internal_currency` | The internal currency of the actual product price. If omitted, the `original_price_internal_currency` value is used. ||
|| `actual_price_internal_value` | Actual product price in the internal currency. This is the current product price, including discounts. If omitted, the `original_price_internal_value` value is used. ||
|| `payload` | {{ post-payload }} ||
|| `product_category_path_1` | Level 1 product category. ||
|| `product_category_path_2` | Level 2 product category. ||
|| `product_category_path_3` | Level 3 product category. ||
|| `product_category_path_4` | Level 4 product category. ||
|| `product_category_path_5` | Level 5 product category. ||
|| `product_category_path_6` | Level 6 product category. ||
|| `product_category_path_7` | Level 7 product category. ||
|| `product_category_path_8` | Level 8 product category. ||
|| `product_category_path_9` | Level 9 product category. ||
|| `product_category_path_10` | Level 10 product category. ||
|| `original_price_currency`* | The currency of the initial product price. [List of available currencies](../../data-collection/currency-codes.md). ||
|| `original_price_value`* | Initial product price before any discounts.||
|| `original_price_internal_currency` | The internal currency of the initial product price. ||
|| `original_price_internal_value` | Initial product price in the internal currency. ||
|| `product_payload` | {{ post-payload }} ||
|| `product_promo_codes` | Array of applied promo codes. ||
|| `product_sku` | Product ID. ||
|| `screen_category_path_1` | Level 1 product category page. ||
|| `screen_category_path_2` | Level 2 product category page. ||
|| `screen_category_path_3` | Level 3 product category page. ||
|| `screen_category_path_4` | Level 4 product category page. ||
|| `screen_category_path_5` | Level 5 product category page. ||
|| `screen_category_path_6` | Level 6 product category page. ||
|| `screen_category_path_7` | Level 7 product category page. ||
|| `screen_category_path_8` | Level 8 product category page. ||
|| `screen_category_path_9` | Level 9 product category page. ||
|| `screen_category_path_10` | Level 10 product category page. ||
|| `screen_name` | The name of the page or screen viewed. ||
|| `screen_payload` | {{ post-payload }} ||
|| `session_type` | The type of session. Possible values:

- `foreground` — In the [Events](../../mobile-reports/events-report.md) report AppMetrica increases the **Users** metric.
- `background` — In the [Events](../../mobile-reports/events-report.md) report AppMetrica increases the **Devices** metric. Such events are not included to the report with grouping by users, and into the profile card.

Default value is `background`. ||
|| `ios_ifa` | {{ ios_ifa }} ||
|| `ios_ifv` | {{ ios_ifv }} ||
|| `google_aid` | {{ google_aid }} ||
|| `windows_aid` | {{ windows_aid }} ||
|| `os_name` | {{ os_name }} ||
|| `os_version` | {{ os_version }} ||
|| `device_manufacturer` | {{ device_manufacturer }} ||
|| `device_model` | {{ device_model }} ||
|| `device_type` | {{ device_type }} ||
|| `device_locale` | {{ device_locale }} ||
|| `app_version_name` | {{ app_version_name }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `connection_type` | {{ connection_type }} ||
|| `operator_name` | {{ operator_name }} ||
|| `mcc` | {{ mcc }} ||
|| `mnc` | {{ mnc }} ||
|| `device_ipv6` | {{ device_ipv6 }} ||
|#

## Response codes

| Code | Description |
| ----- | ----- |
| 200 | Data has been uploaded successfully. |
| 403 | The request omitted an authorization header, or an invalid token was specified. |
| 400 | One or more required parameters were missing in the request. |

## Sample request {#sample}

{% list tabs %}

- Sending data in the request body

  ```http translate=no
  POST /logs/v1/import/ecommerce.csv?post_api_key=0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ012 HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Content-Length: 540i
  Connection: close

  application_id,profile_id,appmetrica_device_id,event_timestamp,ecom_event_type,order_id,product_name,cart_item_quantity,cart_item_price_currency,cart_item_price_value,cart_item_price_internal_currency
  cart_item_price_internal_value,actual_price_currency,actual_price_value,actual_price_internal_currency,actual_price_internal_value,payload,product_category_path_1,product_category_path_2,product_category_path_3,product_category_path_4,product_category_path_5,product_category_path_6,product_category_path_7,product_category_path_8,product_category_path_9,product_category_path_10,original_price_currency,original_price_value,original_price_internal_currency,original_price_internal_value,product_payload,product_promo_codes,product_sku,screen_category_path_1,screen_category_path_2,screen_category_path_3,screen_category_path_4,screen_category_path_5,screen_category_path_6,screen_category_path_7,screen_category_path_8,screen_category_path_9,screen_category_path_10,screen_name,screen_payload,session_type,ios_ifa,ios_ifv,google_aid,windows_aid,os_name,os_version,device_manufacturer,device_model,device_type,device_locale,app_version_name,app_package_name,connection_type,operator_name,mcc,mnc,device_ipv6
  1234567890,1234567890abcdef,1234567890abcdef,1757762239877245682,1689943892,ADD_TO_CART,a1b2c3d4,some_product,1,usd,0.5,some_currency,1.43,usd,0.7,some_currency,2,"{""key"":""value_1""}",product_path_1,product_path_2,product_path_3,product_path_4,product_path_5,product_path_6,product_path_7,product_path_8,product_path_9,product_path_10,usd,1.05,some_currency,3,"{""key"":""value_1""}","[promo_code_1,promo_code_2]",012345abc,screen_path_1,screen_path_2,screen_path_3,screen_path_4,screen_path_5,screen_path_6,screen_path_7,screen_path_8,screen_path_9,screen_path_10,some_screen,"{""key"":""value_1""}",foreground,123456abcde,567890abcde,ios,16.6,Apple,iPhone14Pro,phone,en_US,some_version_name,some_package_name,wifi,MegaFon,250,2,2a02:6b8::40c:6676:baff:fea6:53d8
  ```

- Sending data in request parameters

  ```http translate=no
  POST /logs/v1/import/ecommerce.csv?post_api_key=0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ012&application_id=1234567890&profile_id=1234567890abcdef&appmetrica_device_id=1757762239877245682&event_timestamp=1689943892&ecom_event_type=ADD_TO_CART&order_id=a1b2c3d4&product_name=some_product&cart_item_quantity=1&cart_item_price_currency=usd&cart_item_price_value=0.5&cart_item_price_internal_currency=some_currency&cart_item_price_internal_value=1.43&actual_price_currency=usd&actual_price_value=0.7&actual_price_internal_currency=some_currency&actual_price_internal_value=2&payload="{""key"":""value_1""}"&product_category_path_1=product_path_1&product_category_path_2=product_path_2&product_category_path_3=product_path_3&product_category_path_4=product_path_4&product_category_path_5=product_path_5&product_category_path_6=product_path_6&product_category_path_7=product_path_7&product_category_path_8=product_path_8&product_category_path_9=product_path_9&product_category_path_10=product_path_10&original_price_currency=usd&original_price_value=1.05&original_price_internal_currency=some_currency&original_price_internal_value=3&product_payload="{""key"":""value_1""}"&product_promo_codes="[promo_code_1,promo_code_2]"&product_sku=012345abc&screen_category_path_1=screen_path_1&screen_category_path_2=screen_path_2&screen_category_path_3=screen_path_3&screen_category_path_4=screen_path_4&screen_category_path_5=screen_path_5&screen_category_path_6=screen_path_6&screen_category_path_7=screen_path_7&screen_category_path_8=screen_path_8&screen_category_path_9=screen_path_9&screen_category_path_10=screen_path_10&screen_name=some_screen&screen_payload="{""key"":""value_1""}"&session_type=foreground&ios_ifa=123456abcde&ios_ifv=54321edcba&google_aid=098765abcde&windows_aid=567890abcde&os_name=ios&os_version=16.6&device_manufacturer=Apple&device_model=iPhone14Pro&device_type=phone&device_locale=en_US&app_version_name=some_version_name&app_package_name=some_package_name&connection_type=wifi&operator_name=MegaFon&mcc=250&mnc=2&device_ipv6=2a02:6b8::40c:6676:baff:fea6:53d8 HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Content-Length: 0
  Connection: close
  ```

{% endlist %}

## Other Post API methods {#other-methods}

- [Uploading events](post-import-events.md)
- [Uploading In-App Revenue events](post-revenue.md)
- [Uploading Ad Revenue events](post-adrevenue.md)
- [Profile attributes](post-profile-attributes.md)

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
