# Ad revenue

One of the types of mobile app monetization is in-app ad impressions (ad revenue). You can transmit ad revenue info to AppMetrica.

## What is Ad Revenue data used for? {#resolve-tasks}

- Estimating the overall profitability of your app, including in-app purchases and ad monetization.
- Identifying the best-performing ad units, formats, and screens.
- Measuring the user acquisition metric to identify partners who bring you the most revenue and evaluate the effectiveness of their traffic.
- Identifying the most profitable user segments.
- Optimizing user scenarios and increasing ad monetization.

## How is Ad Revenue calculated? {#calculation}

Data is transmitted from the SDK for each ad impression that generates ad revenue (impression-level revenue data).

All Ad Revenue events in AppMetrica are linked to users and the Ad Revenue metrics are calculated based on this data:

| **Metric** | **Description** |
| ----------- | ----------- |
| Ad Revenue events | The number of Ad Revenue events for the reporting period. |
| Ad revenue | Total revenue from advertising monetization for the reporting period. |
| Ad ARPU | The ratio of app revenue from advertising monetization for the reporting period to the number of app users for the same period. Learn more about [converting currencies](#currency). |
| eCPM | The ratio of the total revenue from advertising monetization to the number of Ad Revenue events for the reporting period multiplied by 1000. |
| Users with Ad Revenue | The number of users with Ad Revenue events for the reporting period. |
| Ad Revenue events per user | The ratio of the number of Ad Revenue events to the number of users for the reporting period. |
| Sessions with Ad Revenue | The number of sessions during which Ad Revenue events were committed for the reporting period. |
| Ad Revenue events per session | The ratio of the number of Ad Revenue events to the total number of sessions for the reporting period. |
| % of users with Ad Revenue | The ratio of the number of users with Ad Revenue events to all users for the reporting period. |

Based on the Ad Revenue data, total revenue metrics are calculated:

| **Metric** | **Description** |
| ----------- | ----------- |
| Total revenue | Total revenue from advertising monetization, in-app purchases, and in-app subscriptions for the reporting period. Learn more about [converting currencies](#currency). |
| Total ARPU | The ratio of the total app revenue from advertising monetization, in-app purchases, and subscriptions for the reporting period to the number of app users for the same period. Learn more about [converting currencies](#currency). |

## Data sources {#src-data}

AppMetrica supports multiple methods of integration with ad monetization and mediation services.

### AppLovin MAX

- Android: [Simplified integration](../sdk/android/analytics/android-operations.md#send-adrevenue-simple-integration-applovin-max)
- iOS: [Manual setup](../sdk/ios/analytics/ios-operations.md#send-adrevenue)
- Flutter: [Manual setup](../sdk/flutter/analytics/flutter-operations.md#send-adrevenue)
- Unity: [Simplified integration](../sdk/unity/analytics/unity-operations.md#adrevenue-autocollection)

### Digital Turbine

- Android: [Simplified integration](../sdk/android/analytics/android-operations.md#send-adrevenue-simple-integration-digital-turbine)
- iOS: [Manual setup](../sdk/ios/analytics/ios-operations.md#send-adrevenue)
- Flutter: [Manual setup](../sdk/flutter/analytics/flutter-operations.md#send-adrevenue)
- Unity: [Manual setup](../sdk/unity/analytics/unity-operations.md#adrevenue-autocollection)

### Google AdMob

- Android: [Simplified integration](../sdk/android/analytics/android-operations.md#send-adrevenue-simple-integration-google-admob)
- iOS: [Manual setup](../sdk/ios/analytics/ios-operations.md#send-adrevenue)
- Flutter: [Manual setup](../sdk/flutter/analytics/flutter-operations.md#send-adrevenue)
- Unity: [Manual setup](../sdk/unity/analytics/unity-operations.md#send-adrevenue)

### ironSource

- Android: [Automatic integration](../sdk/android/analytics/android-operations.md#send-adrevenue-automatic-integration-ironsource)
- iOS: [Manual integration](../sdk/ios/analytics/ios-operations.md#send-adrevenue)
- Flutter: [Manual setup](../sdk/flutter/analytics/flutter-operations.md#send-adrevenue)
- Unity: [Manual setup](../sdk/unity/analytics/unity-operations.md#adrevenue-autocollection)

### Mobile Ads

- Android: [Manual setup](../sdk/android/analytics/android-operations.md#send-adrevenue-manual-integration)
- iOS: [Manual integration](../sdk/ios/analytics/ios-operations.md#send-adrevenue)
- Flutter: [Manual setup](../sdk/flutter/analytics/flutter-operations.md#send-adrevenue)
- Unity: [Manual setup](../sdk/unity/analytics/unity-operations.md#send-adrevenue)

You can transmit data of any other ad monetization service that provides impression-level revenue data.

## Where to find Ad Revenue metrics in the AppMetrica reports {#metrics}

**[In-app and Ad Revenue](../mobile-reports/revenue-report.md) report**

:   Use the **In-app and Ad Revenue** report to estimate the app's total revenue, revenue from different types of monetization (advertising and in-app), and revenue from different advertising networks and different types of ads.

**[User Acquisition](../mobile-reports/user-acquisition-report.md) and [Remarketing](../mobile-reports/remarketing-report.md) reports**

:   Use these reports to evaluate the effectiveness of sources for user acquisition and remarketing in terms of ARPU and other advertising and in-app monetization metrics. Please note that the metrics in the report are summed up over the user's entire lifetime.

**[Cohort analysis](../mobile-reports/cohort-report.md)**

:   Using the cohort analysis report, you can estimate how much revenue you receive from users over time and what ARPU is on a certain day.

**[Funnels](../mobile-reports/funnels-report.md)**

:   In the funnels report, you can estimate the ratio of users who end up viewing ads in general or, for example, rewarded ads.

**Segmentation**

:   To build each report, you can select only those users who, for example, interacted with ads from a certain advertising network or of a certain advertising format.

## Currency conversion {#currency}

You can transfer Ad Revenue data in different currencies. For a list of all supported currencies, see [Supported currencies](currency-codes.md).

Ad Revenue is converted into any currency the report supports: USD, EUR, or RUB. AppMetrica uses an exchange rate that is provided from more than 15 sources, including the European Central Bank.

AppMetrica converts the currency using the previous day rate. For example, if the Ad Revenue event occurred on day N, the revenue is converted at the exchange rate of day N − 1. Conversion takes place into EUR and RUB against USD.

## Debugging of Ad Revenue data sending {#test-send}

In AppMetrica, you can't segment Ad Revenue data into "test" and "not test" data. If you use the main API key for debugging the collection of data on advertising monetization, the test events are included in general statistics. If you need to debug the sending of Ad Revenue data, use a reporter to send statistics to an additional API key. For more information, see [{#T}](#send-adrevenue).

## Sending Ad Revenue events {#send-adrevenue}

Examples of sending Ad Revenue events on different platforms:

- [Android](../sdk/android/analytics/android-operations.md#send-adrevenue)
- [iOS](../sdk/ios/analytics/ios-operations.md#send-adrevenue)
- [Flutter](../sdk/flutter/analytics/flutter-operations.md#send-adrevenue)
- [React Native](../sdk/react-native/analytics/react-native-operations.md#send-adrevenue)
- [Unity](../sdk/unity/analytics/unity-operations.md#send-adrevenue)

{% if locale == "ru" %}

## Learn more {#learn-more}

- [Ad monetization: how to analyze ad revenue in AppMetrica](https://appmetrica.yandex.ru/about/blog/ad-revenue-release)

{% endif %}


{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
