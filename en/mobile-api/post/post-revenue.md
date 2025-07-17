# Uploading In-App Revenue events

Transmits data about purchases.

Usage example: You can send In-App Revenue events to AppMetrica via the Post API if purchases in your app are not made through Google Play or AppStore and are not tracked on the client side. If you track subscription data inside the app on your own or use a third-party service, you can transmit subscription data via the Post API.

Purchase events received via the Post API are used when calculating all metrics and are also available in funnels and cohorts.

{% note info %}

Revenue events received via the Post API are not validated and are always considered valid.

{% endnote %}

Event properties can be passed in parameters or in the body of the request. When you pass data in the body, you should add `.csv` to the URL of the request. For more information, see [Sample request](#sample).

To bind an event to a user, you should use one of the following fields in the API request:

- `profile_id`
- `appmetrica_device_id`

{% note alert %}

The Post API has restrictions on loading data. For more information, see [Restrictions](restrictions.md).

{% endnote %}

## Request format

```
POST {{ api-url }}/logs/v1/import/revenue
  ? post_api_key=<string>
  & application_id=<int>
  & profile_id=<string>
  & appmetrica_device_id=<int>
  & revenue_event_type=<string>
  & event_timestamp=<int>
  & price=<decimal>
  & currency=<string>
  & product_id=<string>
  & [quantity=<int>]
  & [payload=<string>]
  & [transaction_id=<int>]
  & [order_id=<int>]
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
|| `revenue_event_type`* | {{ post-revenue_event_type }} ||
|| `event_timestamp`* | {{ event_timestamp }} ||
|| `price`* | {{ post-price }} ||
|| `currency` | {{ post-currency }} [List of available currencies](../../data-collection/currency-codes.md). ||
|| `product_id` | {{ revenue_product_id }} ||
|| `quantity` | {{ revenue_quantity }} Default value: `1`. ||
|| `payload` | {{ post-payload }} ||
|| `transaction_id` | {{ post-transaction_id }} ||
|| `order_id` | {{revenue_order_id }} ||
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
  POST /logs/v1/import/revenue.csv?post_api_key=0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ012 HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Content-Length: 540i
  Connection: close

  appmetrica_device_id,device_model,device_type,google_aid,app_package_name,operator_name,mnc,application_id,account_id,event_timestamp,price,currency,product_id,quantity,transaction_id,order_id,revenue_event_type
  1757762239877245682,iPhone X,phone,01234567-890a-bcde-f012-3456789abcde,com.yandex.sample.metrica,MegaFon,2,1111,1234567890123456789,1689943892,0.0001,usd,some_product1,1,transact1,8101,promo_started
  1757762239877245682,iPhone X,phone,76543210-890a-bcde-f012-3456789abcde,com.yandex.sample.metrica,MegaFon,2,1111,9876543210987654321,1689943892,0.0001,usd,some_product2,2,transact2,1234,expired

  ```

- Sending data in request parameters

  ```http translate=no
  POST /logs/v1/import/revenue.csv?post_api_key=0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ012&appmetrica_device_id=1757762239877245682&device_model=iPhoneX&device_type=phone&google_aid=01234567-890a-bcde-f012-3456789abcde&app_package_name=com.yandex.sample.metrica&operator_name=MegaFon&mnc=2&application_id=1111&account_id=1234567890123456789&event_timestamp=1689943892&price=0.0001&currency=usd&product_id=some_product1&quantity=1&transaction_id=transact1&order_id=8101&revenue_event_type=promo_started HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Content-Length: 0
  Connection: close
  ```

{% endlist %}

## Other Post API methods {#other-methods}

- [Uploading events](post-import-events.md)
- [Uploading Ad Revenue events](post-adrevenue.md)
- [Uploading E-commerce events](post-ecommerce.md)
- [Profile attributes](post-profile-attributes.md)

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
