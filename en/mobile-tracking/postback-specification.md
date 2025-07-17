# Postback parameters

The details of postback support in AppMetrica are described below.

## General information {#general}

AppMetrica lets you assign postbacks for the tracker and specify when to send the postback. AppMetrica supports:

- Postback about app installations ([install postback](postback-quota.md#install-postback)).
- Postback about a specified event in the app that occurred after installation ([event postback](postback-quota.md#event-postback)).
- Postback when receiving an E-commerce event from the app ([ecommerce postback](postback-quota.md#ecommerce-postback)).
- Postback when receiving an event about in-app purchases ([purchase postback](postback-quota.md#inapp-postback)) from the app.
- Postback when receiving an ad impression event ([adrevenue postback](postback-quota.md#adrevenue-postback)) from the app.

The following rules apply:

- The postback is sent when the specified event or installation attribution appears. There is about a 5-minute delay when sending.
- When the HTTP status `200 OK` is received, it is considered successfully sent.
- If a different HTTP status is received, AppMetrica resends the postback over the next 24 hours. Resending is repeated every 5-10 minutes.
- An event postback is sent for events that occur within 6 months after installation.

## Transmitting tracking URL parameters {#trackingurl-params}

AppMetrica allows passing any [tracking URL parameters](tracking-specification.md) in a postback request. In the postback URL or postback body (for the POST method), specify the parameter name from the tracking URL in curly brackets: `{parameter_name}`.

For example, the following parameters are transmitted in the tracking URL:

```
https://redirect.appmetrica.yandex.com/serve/123456?custom_parameter=value1&another_param=value2
```

To pass the `value1` and `value2` parameters to the postback URL, write:

```
https://endpoint.myadnetwork.com?some_parameter={custom_parameter}&another_param={another_param}
```

To pass the `value1` and `value2` parameters using the POST method, write the following in the body:

```
{
  "some_parameter": "{custom_parameter}",
  "another_param": "{another_param}"
}
```

## List of postback macros {#macros}

AppMetrica supports a list of system macros that can be used in the postback URL or postback body (for the POST method). This list contains macros for device, attributed click, or in-app impression info. If AppMetrica can't determine the parameter value for a macro, the parameter will be empty.

### Information about clicks, installs, and events {#events}

`{adwords_link_id}` — Link ID for connecting Google Ads and AppMetrica. For more information, see [Setting up tracking for Google Ads campaigns](adwords-settings.md).

`{click_id}` — Unique click/impression ID. The macro is not available for unattributed postbacks.

`{match_type}` — How the click/impression was associated with the install. Possible values: `referrer` | `fingerprint` | `identifier`.

`{attributed_touch_type}` — Ad interaction type. Possible values: `click` | `impression`.

`{transaction_id}` — ID of this occurrence of the event or installation. For example, if the same device generates the same event, `transaction_id` changes.

`{click_user_agent}` — User-agent of the click/impression.

`{click_datetime}` — {% if locale == 'ru' %}[UTC](https://ru.wikipedia.org/wiki/Всемирное_координированное_время){% endif %}{% if locale == 'en' %}[UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time){% endif %} date and time of the click/impression in RFC3339 format.

`{click_timestamp}` — Time of the click/impression, Unix timestamp format, in seconds.

`{click_timezone}` — Time zone of the click/impression as the offset from UTC in seconds.

`{click_ipv6}` — IP address at the time of the click/impression, IPv6 format. For example, 2a02:6b8::40c:6676:baff:fea6:53d8, ::ffff:5.255.232.147.

`{conversion_datetime}` — UTC date and time of conversion (event on the device) in RFC3339 format.

`{conversion_timestamp}` — Time of conversion (event on the device) in Unix timestamp format, in seconds.

`{conversion_timezone}` — The time zone (user's location) for conversion. Formatted as the difference from UTC time in seconds.

`{conversion_event_name}` — Name of the event for registering the  conversion.

`{conversion_event_json}` — Nested event attributes in {% if locale == 'ru' %}[JSON](http://www.json.org/json-ru.html){% endif %}{% if locale == 'en' %}[JSON](http://www.json.org/){% endif %} format.

`{install_datetime}` — UTC date and time of installation in RFC3339 format.

`{install_timestamp}` — Time of installation in Unix timestamp format, in seconds.

`{install_timezone}` — Time zone (user's location) for the installation. Formatted as the difference from UTC time in seconds.

`{install_ipv6}` — The IP address at the time of installation, in IPv6 format (for example, 2a02:6b8::40c:6676:baff:fea6:53d8, ::ffff:5.255.232.147).

`{start_datetime}` — UTC date and time of session start in RFC3339 format.

`{start_timestamp}` — Time of session start in Unix timestamp format, in seconds.

`{start_timezone}` — Time zone of session start as the offset from UTC in seconds.

`{session_id}` — Session ID. Unique only within a specific app, `appmetrica_device_id`, installation, and session type (foreground/background).

### Device information {#device}

`{adwords_rdid}` — Google AID for Android or IFA for iOS. If Google AID or IFA are not available — the `"00000000-0000-0000-0000-000000000000"` value is sent.

`{appmetrica_device_id}` — Unique device identifier detected by the AppMetrica service.

`{profile_id}` — User profile ID. For more information, see [User profile](../data-collection/about-profiles.md).

`{limit_ad_tracking}` — Ad tracking is restricted on the device. It can take the values: 1 if the user disabled ad identification; 0 if the user didn't disable it. If the device supports multiple IDs, such as Google AID and Huawei OAID, the value is set to 0 if at least one of these IDs is available.

`{google_aid}` — The device's Google AID in the format it was received from the device in.

`{ios_ifa}` — The device's IFA in the format it was received from the device in.

`{ios_ifv}` — IFV for the device in the format it was received from the device in.

`{oaid}` — The device's Huawei OAID in the format it was received from the device in.

`{windows_aid}` — Windows AID in the format it was received from the device in.

`{device_manufacturer}` — The device manufacturer detected by the AppMetrica service (for example, Apple or Samsung).

`{device_model}` — The device model detected by the AppMetrica service (for example, Galaxy S6).

`{device_type}` — The device type detected by the AppMetrica service. Possible values: `PHONE` | `TABLET` | `PHABLET` | `TV`.

`{device_locale}` — The language on the device.

`{os_name}` — Operating system. Possible values: `ios` | `android` | `windows`.

`{os_version}` — The version of the operating system on the user's device.

`{operator_name}` — The name of the mobile operator.

`{mcc}` — Mobile country code.

`{mnc}` — Mobile network code.

### Information about the app and the OS {#app}

`{app_version_name}` — The app version in the format specified by the developer.

`{app_package_name}` — The package name for Android or the `Bundle ID` for iOS (for example, `ru.yandex.metro`).

`{appmetrica_sdk_version}` — The AppMetrica SDK version that has been integrated into the application.

`{store_app_id}` — Application ID in Google Play or App Store.

### Macros for ad revenue events {#adrevenue}

`{price}`: Ad revenue.

`{currency}`: Currency of ad revenue.

### Macros for any purchases {#purchases}

`{price}` — The purchase or product cost.

`{currency}` — The purchase currency.

`{product_id}` — The purchase `product_id`. For in-app purchases, the ID specified when creating a purchase in the App Store or Google Play. For E-commerce, the `product_id` specified for the product.

`{order_id}` — The order ID.

### Macros for in-app purchases only {#inapp}

`{inapp_transaction_id}` — The unique purchase ID.

`{inapp_validated}` — Shows whether the purchase is validated in the App Store or Google Play.

`{inapp_receipt}` — Purchase information from the App Store or Google Play.

### Macros for E-commerce purchases only {#ecommerce}

`{ecom_revenue}` — Full revenue from a completed purchase.

`{ecom_quantity}` — The number of units of a specific product.

`{ecom_product_name}` — The name of the product.

`{ecom_promocodes}` — Promo codes applied.

`{ecom_type}` — E-commerce event type. Possible values:

  - `1` — Viewed page.
  - `2` — Viewed a product from the list.
  - `3` — Viewed product details.
  - `4` — Added to cart.
  - `5` — Removed from cart.
  - `6` — Initiated checkout.
  - `7` — Purchased.

`{ecom_category_path_1}` — Product category.

`{ecom_category_path_2}` — Product category.

`{ecom_category_path_3}` — Product category.

`{ecom_category_path_4}` — Product category.

`{ecom_category_path_5}` — Product category.

`{ecom_category_path_6}` — Product category.

`{ecom_category_path_7}` — Product category.

`{ecom_category_path_8}` — Product category.

`{ecom_category_path_9}` — Product category.

`{ecom_category_path_10}` — Product category.

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
