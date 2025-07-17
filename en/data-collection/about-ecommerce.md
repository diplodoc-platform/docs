# E-commerce

When making in-app purchases, users perform various actions (E-commerce events). For example:

- Opening a page.
- Viewing a product profile and page.
- Adding and removing an item to/from the cart.
- Starting and completing a purchase.

AppMetrica lets you collect information about these actions and track statistics in the web interface, in the [E-commerce](../mobile-reports/ecommerce-report.md) report.

To collect statistics on E-commerce events, configure sending events in the app. For more information, see [{#T}](#send-ecommerce).

## Configuring dimensions and metrics {#metrics}

You can customize the "Purchase analysis" report using dimensions and metrics. For more information about available dimensions and metrics, see [E-commerce report](../mobile-reports/ecommerce-report.md).

For instance, you can estimate:
- The number of product profile and page views.
- The number of additions to the cart.
- The number of purchases.
- The amount of revenue, refunds, and discounted sales.
- Geography of purchases using a dimension with data grouped by city.

## Debugging E-commerce event sending {#debug}

In AppMetrica, it isn't possible to segment E-commerce events into "test" and "not test" ones. If you use the main API key for debugging purchases, the test events are included in general statistics. Therefore, to debug E-commerce event sending, use a reporter to send statistics to the additional API key. For more information, see examples in [{#T}](#send-ecommerce).

## Sending E-commerce events {#send-ecommerce}

Examples of sending an E-commerce event on various platforms:

- [Android](../sdk/android/analytics/android-operations.md#send-ecommerce)
- [iOS](../sdk/ios/analytics/ios-operations.md#send-ecommerce)
- [Flutter](../sdk/flutter/analytics/flutter-operations.md#send-ecommerce)
- [React Native](../sdk/react-native/analytics/react-native-operations.md#send-ecommerce)
- [Unity](../sdk/unity/analytics/unity-operations.md#send-ecommerce)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
