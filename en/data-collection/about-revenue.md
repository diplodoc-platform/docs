# In-app purchases

<!-- {% if tld == "ru" %}

{% note warning %}

This feature is discontinued and will no longer receive updates. Data accuracy not guaranteed.

AppMetrica provides an [alternative tracking technology](https://appmetrica.yandex.com/docs/en/data-collection/apphud/apphud-about) available in certain regions.

{% endnote %}

{% endif %} -->

Mobile apps can earn revenue from ad impressions ([Ad Revenue](*Ad Revenue)) and in-app purchases ([IAP Revenue](*IAP Revenue)).

AppMetrica allows you to collect information about purchases in the app and track statistics in the [In-app and Ad Revenue](../mobile-reports/revenue-report.md)  report. For more information, see [{#T}](#send-revenue).

{% if tld == "com" %}

## Tracking via Apphud {#apphud}

{% note info "" %}

This feature is available with the Custom and Pro [plans](../common/pricing/uae-currency.md#apphud). [Learn more](apphud/apphud-about.md) about enabling Apphud.

{% endnote %}

With AppMetrica, you can set up purchase and subscription tracking through Apphud and gain access to advanced data collection capabilities. This integration allows you to:

- Track [Consumable](*consumable) and [Non-consumable](*non-consumable) purchases and their refunds.
- Calculate revenue, accounting for the App Store fee, VAT, and currency conversion rates.

{% endif %}

## Tracking via AppMetrica {#appmetrica}

{% if tld == "com" %}

This feature is discontinued and will no longer receive updates. Data accuracy not guaranteed. We recommend using [tracking via Apphud](#apphud) instead.

{% endif %}

#### Automatic tracking of in-app purchases {#in-app-tracking}

For iOS and Android, starting with SDK version 4.0, automatic data collection for in-app purchases is available. To enable and disable automatic statistics collection, use the `withRevenueAutoTrackingEnabled` SDK method for Android and the `revenueAutoTrackingEnabled` property for iOS. For more information, see [{#T}](#send-revenue).

If your app has manual collection of purchases set up and automatic collection enabled, then you can choose which data on purchases to show in reports in the AppMetrica settings in the Revenue section: collected manually, automatically collected, or both.

Changing these settings does not affect data collection itself. After you change these settings, the data in the reports for previous periods will also change.

{% note alert "" %}

To track subscription renewals, set up revenue sending at each renewal.

{% endnote %}

#### Sending in-app purchases {#send-revenue}

Examples of sending in-app purchases on different platforms:

- [Android](../sdk/android/analytics/android-operations.md#send-revenue)
- [iOS](../sdk/ios/analytics/ios-operations.md#send-revenue)
- [Flutter](../sdk/flutter/analytics/flutter-operations.md#send-revenue)
- [React Native](../sdk/react-native/analytics/react-native-operations.md#send-revenue)
- [Unity](../sdk/unity/analytics/unity-operations.md#send-revenue)

## Tracking metrics {#metrics}

You can use the **In App и Ad Revenue** report data to evaluate:
- The success of new app features using the [ARPU](*ARPU) metric.
- User reaction to price changes using the [ARPPU](*ARPPU) metric.
- Popular products in the app.
- Geography of purchases by grouping city.
- Profitability of individual ad networks and units.

## Currency conversion {#currency}

In-app purchases can be made in different currencies. For a list of all supported currencies, see [Supported currencies](currency-codes.md).

AppMetrica converts the purchase price to all report currencies: USD, EUR, RUB. AppMetrica uses an exchange rate that is provided from more than 15 sources, including the European Central Bank.

AppMetrica converts the currency using the previous day rate. For example, if the purchase was made on day N, the purchase price is converted at the exchange rate of day N − 1. Conversion takes place into EUR and RUB against USD.

{% note alert "" %}

The AppMetrica conversion rate may not coincide with Google Play Console and iTunes Connect rates.

{% endnote %}

## Validating purchases {#validation}

The service supports [validation of purchases](*validation of purchases) made through the App Store or Google Play. Purchases on iOS are validated using the iTunes API and on Android through local validation using a public key.

{% if tld == "com" %}

To validate purchases:

{% list tabs %}

- Apphud

   Add keys/certificates when enabling [Apphud](apphud/apphud-about.md).

- AppMetrica

   You can set up sending additional information with your revenue data by adding the required keys in your AppMetrica settings. For more information, see [{#T}](#send-revenue).

{% endlist %}

{% endif %}

{% if tld == "ru" %}

You can set up sending additional information with your revenue data by adding the required keys in your AppMetrica settings. For more information, see [{#T}](#send-revenue).

{% endif %}

With validation enabled:
- The report shows purchases that were validated or sent without any information for validation.
- All In-App Revenue metrics are counted based on validated purchases and purchases passed without parameters for validation.
- For invalid purchases, **Invalid revenue** and **Users with invalid revenue** metrics are counted.

<!--## Группировка покупок {#grouping}

ВОПРОС ОЛЕ!!!

Покупки в приложении группируются по идентификатору `OrderID`.

Для покупок c валидацией в качестве идентификатора используются:
- На iOS — идентификатор [transactionIdentifier](https://developer.apple.com/documentation/storekit/skpaymenttransaction/1411288-transactionidentifier). Он генерируется библиотекой [StoreKit](https://developer.apple.com/documentation/storekit).
- На Android — идентификатор [OrderId](https://developer.android.com/reference/com/android/billingclient/api/Purchase.html#getorderid). Он генерируется библиотекой [Google Play Billing](https://developer.android.com/google/play/billing/billing_overview).

Для покупок без валидации `OrderID` можно задать вручную. Его необходимо передавать в поле `payload`. Подробнее в разделе [{#T}](#send-revenue).

Если `OrderID` не передается, AppMetrica SDK генерирует идентификатор покупки автоматически. -->

<!--
{% if tld == "ru" %}

## Отладка отправки Revenue {#debug}

УДАЛИТЬ

В AppMetrica нет возможности сегментировать Revenue на "тестовые" и "не тестовые". Если для отладки покупок вы используете основной API key, то тестовые покупки будут попадать в общую статистику. Поэтому, чтобы отладить отправку Revenue, используйте отправку статистики на дополнительный API key с помощью репортера. Подробнее в разделе [{#T}](#send-revenue).

{% endif %} -->

{% if tld == "ru" %}

## Paid subscriptions in the App Store {#subscription}

In the AppMetrica SDK, you can track new paid subscriptions in the App Store. They are processed as regular purchases.

{% note alert "" %}

To track subscription renewals, configure revenue sending for each renewal.

{% endnote %}

{% endif %}

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*Ad Revenue]: {{ ad-revenue }}

[*IAP Revenue]: {{ iap }}

[*ARPU]: {{ arpu }}Learn more about [converting](#currency) currencies.

[*ARPPU]: {{ arppu }} Learn more about [converting](#currency) currencies.

[*consumable]: This type of purchase can be made multiple times. For example, this could be extra lives or energy points in a game.

[*non-consumable]: This type of purchase can only be made once. For example, this could be a character in a game or a movie on a streaming site.

[*validation of purchases]: Confirmation of purchases and payments made through Google Play or the App Store. Validation lets you filter purchases made from hacked apps. With validation enabled, all In-App Revenue metrics are counted based on validated purchases and purchases sent without validation parameters. For invalid purchases, **Invalid revenue** and **Users with invalid revenue**  metrics are counted.
For more information about configuring validation, see [{#T}](#send-revenue).
