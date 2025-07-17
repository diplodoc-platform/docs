# Getting started

## Step 1. Create an account and set up the app {#create-user}

{% note info %}

You need a Yandex ID account to use AppMetrica. If you don't have one, please [register](https://passport.yandex.{{ domain }}/passport?mode=register).

{% endnote %}

#|
|| **Action** | **Role** | **Estimated time** | **Comments** ||
|| Register and set up an AppMetrica account |
* Product manager
* Developer | 10 min |
* Provide details about your company and app. 

   If the company is not registered in the Russian Federation, use letters of the Latin alphabet.
* Save the API key from your account settings. You'll need to share it with your developer for SDK integration.

   {% cut "What is an API key?" %}

   {{ api-key }}

   {% endcut %} ||
   || Grant your team members access to AppMetrica |
* Product manager
* Developer | 1 min per user | AppMetrica offers multiple levels of access. For more information, see [Managing app access](access.md). ||
   |#

## Stage 2. Integrate the AppMetrica SDK {#integration-sdk}

#|
|| **Action** | **Role** | **Estimated time** | **Comments** ||
|| Choose a platform for AppMetrica SDK integration |
* Product manager
* Developer | 10 min | AppMetrica is available for native [Android](../sdk/android.yaml) and [iOS](../sdk/ios.yaml) apps. In addition, you can use plugins for [Unity](../sdk/unity.yaml) \| [Flutter](../sdk/flutter.yaml) \| [React Native](../sdk/react-native.yaml).

_Recommendation: Use the same API key for both versions of your app._ ||
|| Configure advanced SDK settings |
* Product manager
* Developer | 30 min | The AppMetrica team recommends taking advantage of these advanced features:
* [Importing attributions from other SDKs](../data-collection/attribution-integration.yaml).
* Tracking new users when integrating the SDK into an existing app ([Android](../sdk/android/analytics/android-operations.md#new-user) \| [iOS](../sdk/ios/analytics/ios-operations.md#new-user)).
* Configuring the use of GAID/IDFA advertising IDs ([Android](../sdk/android/get-ad-id.md) \| [iOS](../mobile-tracking/ios-tracking.md)).
* Configuring the use of [deeplinks](../sdk/android/analytics/android-operations.md#deeplink) and [universal links](../sdk/ios/analytics/ios-universal-links.md).

For more information, see the sections on [Android](../sdk/android.yaml), [iOS](../sdk/ios.yaml), [Unity](../sdk/unity.yaml), [Flutter](../sdk/flutter.yaml), and [React Native](../sdk/react-native.yaml).
||
|| Determine what basic app events you want to monitor |
* Product manager
* Developer | 30 min | AppMetrica supports [a number of event types](../data-collection/index.md). Some of the basic events are monitored automatically, while others require manual setup by the developer. For example:
* [E-commerce](../data-collection/about-ecommerce.md)
* [AdRevenue](../data-collection/about-adrevenue.md)
* [Errors](../data-collection/about-crashes-and-errors.md) ||
   || Determine what custom events you want to monitor |
* Product manager
* Developer | 30 min | With AppMetrica, you can collect statistics on [custom app events](../mobile-reports/events-report.md).

_Recommendation: Learn more about the [limits](../troubleshooting/limit-events.md) for custom events._ ||
|| Start sending the collected data to your developers |
* Developer | 3 hours | Useful resources for developers:
* [Integration for Android](../sdk/android/analytics/quick-start.md)
* [Integration for iOS](../sdk/ios/analytics/quick-start.md)
* [Integration for Unity](../sdk/unity/analytics/quick-start.md)
* [Integration for Flutter](../sdk/flutter/analytics/quick-start.md)
* [Integration for React Native](../sdk/react-native/analytics/quick-start.md)
* Method usage examples for [Android](../sdk/android/analytics/android-operations.md), [iOS](../sdk/ios/analytics/ios-operations.md), [Unity](../sdk/unity/analytics/unity-operations.md), [Flutter](../sdk/flutter/analytics/flutter-operations.md), and [React Native](../sdk/react-native/analytics/react-native-operations.md)
* [Setting up data collection](../data-collection/index.md) ||
   |#

## Additional tools {#advanced}

### Integrate the AppMetrica Push SDK {integration-push-sdk}

#|
|| **Action** | **Role** | **Estimated time** | **Comments** ||
|| Choose a platform for AppMetrica Push SDK integration |
* Product manager
* Developer | 10 min | The AppMetrica Push SDK is available for native [Android](../sdk/android.yaml) and [iOS](../sdk/ios.yaml) apps. In addition, you can use plugins for [Unity](../sdk/unity.yaml) \| [Flutter](../sdk/flutter.yaml). ||
   || Read about [integration](../sdk/android/push/android-other-push-services-settings.md) when using other push services |
* Developer | 30 min | Developers should learn how to redirect messages between integrated SDKs. ||
   || Read about the [Push API features](../mobile-api/push/about.md) |
* Product manager
* Developer | 20 min | AppMetrica supports sending push notifications both through the service interface and via API. ||
   |#

### Learn more about the AppMetrica analytics tools {#appmetrica-analytics}

#### Reports {#reports}

The [AppMetrica web interface](http://appmetrika.yandex.{{domain}}/) lets you view statistics on mobile app usage.

#|
|| **{{ reports }}** → **{{ report-product }}** | > ||
|| [Engagement](../mobile-reports/engagement-report.md) | With this report, you can:
* Evaluate the time spent by users in the app
* Determine the average duration of the session
* Evaluate the frequency of app use
* Compare engagement metrics across different user groups ||
   || [Retention analysis](../mobile-reports/retention-report.md) | With this report, you can assess:
* User demand for various features of your app
* How app updates affect user retention
* User LTV in the app ||
   || [Funnels](../mobile-reports/funnels-report.md) | With this report, you can:
* Compare conversion rates across different app versions
* Assess conversion dynamics for a user behavior scenario
* Identify an audience segment that needs a specific app feature ||
   || [Audience](../mobile-reports/audience-report.md) | With this report, you can assess:
* What audience the ad campaign attracts
* How changes to the app affect traffic from a specific region ||
   || [Cohort analysis](../mobile-reports/cohort-report.md) | With this report, you can assess:
* The quality of traffic sources
* The quality of the audience generated by partners
* How many users in the selected cohort have triggered an event ||
   || [Events](../mobile-reports/events-report.md) | With this report, you can:
* Assess the reach and popularity of app features
* Compare the behavior of multiple user groups
* Measure how often app features are used within sessions
* Analyze nested event parameters ||
   || [Profiles report](../mobile-reports/profile-report.md) | This report shows user distribution based on selected attributes, including custom ones. This is the only report that tracks users by `profile_id` ||
   || **{{ reports }}** → **{{ report-marketing }}** | > ||
   || [User Acquisition](../mobile-reports/user-acquisition-report.md) | This report shows information on app install sources ||
   || [User Acquisition SKAdNetwork](../mobile-reports/user-acquisition-skadnetwork.md) | This report shows statistics on app install sources obtained from SKAdNetwork, a campaign attribution system for iOS 14.5+ that ensures user privacy ||
   || [Push campaigns](../mobile-reports/push-campaign.md) | This report shows push campaign statistics, including the number of sent, delivered, and opened push notifications ||
   || [Remarketing](../mobile-reports/remarketing-report.md) | This report shows data on user re-engagement (users who returned to the app) and the target events they completed ||
   || **{{ reports }}** → **{{ report-monetization }}** | > ||
   || [E-commerce](../mobile-reports/ecommerce-report.md) | This report shows what actions users take when making purchases ||
   || [In-app and Ad Revenue](../mobile-reports/revenue-report.md) | With this report, you can:
* Measure the success of new features using ARPU
* Assess user reactions to price changes using ARPPU
* Discover your app's most popular products
* Determine the geography of purchases using a dimension with data grouped by city
* Assess the profitability of different ad networks and units ||
   || **{{ reports }}** → **{{ report-crashes-and-errors }}** | > ||
   || [Crashes and errors](../mobile-reports/crashes-and-errors.md) | With this report, you can determine which crashes and errors occur most often ||
   |#

#### API {#api}

- The [Management API](../mobile-api/management/intro.md) for adding, editing, and deleting apps.
- The [Reporting API](../mobile-api/api_v1/intro.md) for getting app statistics.
- The [Logs API](../mobile-api/logs/about.md) for getting raw data about your application.
- The [Data Stream API](../mobile-api/datastream/about.md) for exporting data as CSV or JSON files.
- [Post API](../mobile-api/post/about.md) for uploading event information.
- The [Push API](../mobile-api/push/about.md) for creating push campaigns.

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
