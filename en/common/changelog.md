# Changelog

## 2025 {#year-2025}

### June 2025 {#june-2025}

- We've opened the basics training course for AppMetrica in the [Telegram-bot](https://t.me/AppMetrica_training_bot).
- We've improved the [workspaces](../mobile-reports/workspaces.md) interface.
- You can now create [custom widgets](../mobile-reports/widgets.md#custom) using the widget builder.
- You can share your ideas and suggestions on how to improve reports through the feedback form on [every report page](../mobile-reports/index.md). 
- You can set [conversion rules](../mobile-tracking/conversions.md).
- We've changed the [RCPA postback sending rules](../mobile-tracking/postback-first-target-event-only.md).

### April 2025 {#april-2025}

- We've added a new report: [Conversions](../mobile-reports/conversions-report.md).
- You can now [compare any two segments or periods of time](../mobile-reports/segment-comparison.md) in the following reports:
   - [Audience](../mobile-reports/audience-report.md)
   - [Engagement](../mobile-reports/engagement-report.md)
   - [Profiles](../mobile-reports/profile-report.md).
   - [Ecommerce](../mobile-reports/ecommerce-report.md)
   - [In-app and Ad Revenue](../mobile-reports/revenue-report.md)
- A new method that [checks the availability of the Logs API](../mobile-api/management/logs-api-status.md) has been added to the Management API.

### March 2025 {#march-2025}

- A tracker is now automatically archived if it hasn't recorded any app installation or deeplink events within 365 days. Previously, this period was 180 days.
- We've added the minimum plugin version requirements for integration with the [Yandex Ads SDK](ads-sdk-integration.md):
   - Unity Ads SDK: version [7.10.0](https://ads.yandex.com/helpcenter/{{locale}}/dev/unity/changelog-unity#2025) or higher.
   - React Ads SDK: version [7.10.0](https://ads.yandex.com/helpcenter/{{locale}}/dev/react-native/changelog-react-native#2025) or higher.
   - Flutter Ads SDK: version {% if locale=="ru" %}[7.9.0](https://ads.yandex.com/helpcenter/ru/dev/flutter/changelog-flutter#versiya-790-12-fevralya,-2025){% elsif locale=="en" %}[7.9.0](https://ads.yandex.com/helpcenter/en/dev/flutter/changelog-flutter#version-790-february-12,-2025){% else %}7.9.0{% endif %} or higher.

### February 2025 {#february-2025}

- We've updated the [tracker list](../mobile-tracking/index.md#tracker-list) interface.
- In the [Remarketing](../mobile-reports/remarketing-report.md#deeplinks) report, you can now choose to display data for all deeplinks or for re-engagement deeplinks only.
{% if tld == "com" %}- We've implemented the [Apphud](../data-collection/apphud/apphud-about.md) integration for AppMetrica.{% endif %}
- The AppMetrica SDK for Android has been updated to version [7.7.0](../sdk/android/changelog-android.md#s-7-7-0).
- The AppMetrica Push SDK for iOS has been updated to version [3.0.2](../sdk/ios/changelog-ios.md#v-push-3-0-2).

### January 2025 {#january-2025}

- We've added a new dimension to the [Audience](../mobile-reports/audience-report.md), [E-commerce](../mobile-reports/ecommerce-report.md), [Engagement](../mobile-reports/engagement-report.md), [Profiles](../mobile-reports/profile-report.md), [Push campaigns](../mobile-reports/push-campaign.md), and [Revenue](../mobile-reports/revenue-report.md) reports — "Profile attributes".
- You can now export data directly from the Data Stream API:
   - [Conversions](../mobile-api/datastream/data-type-fields.md#attributed_event) (`attributed_event`)
   - [Deeplinks](../mobile-api/datastream/data-type-fields.md#deeplinks) (`deeplink`)
- The AppMetrica Push SDK for iOS has been updated to version [3.0.0](../sdk/ios/changelog-ios.md#v-push-3-0-0):
   - Support for the App Groups mode has been discontinued. The SDK now only supports sending events directly to AppMetrica ([setup](../sdk/ios/analytics/ios-appgroup.md) required).
   - Dependency update: AppMetrica-5.9.0.
- Setup instructions for tracking [unified performance campaigns](../mobile-tracking/yandex-direct-upc-tracking.md) and [Web+App](../mobile-tracking/yandex-direct-web-app-tracking.md) placements integrated with Yandex Direct are now available.
- AppMetrica Push SDK for Android updated to version [4.1.1](../sdk/android/changelog-android.md#v-4-1-1).
- AppMetrica SDK for Android updated to version [7.6.0](../sdk/android/changelog-android.md#s-7-6-0).

## 2024 {#year-2024}

### December 2024 {#december-2024}

- AppMetrica SDK for Android updated to version [7.5.0](../sdk/android/changelog-android.md#s-7-5-0). Added an API for managing access to advertising identifiers (GAID, Huawei OAID). For more information, see the [documentation](../sdk/android/analytics/android-operations.md#track-adv-identifiers).
- AppMetrica SDK for iOS updated to version [5.9.0](../sdk/ios/changelog-ios.md#v-5-9-0).
- AppMetrica Gradle Plugin updated to version [1.0.1](../sdk/android/changelog-android.md#c-1-0-1).
- The Data Stream API now includes [new export fields](../mobile-api/datastream/data-type-fields.md#installations) for fraud assessment status and installation updates.

### November 2024 {#november-2024}

- You can now [enable anti-fraud checks](../mobile-tracking/add-tracker.md) when creating or editing trackers.
- You can view assessments provided by FraudScore in the [User Acquisition](../mobile-reports/user-acquisition-report.md) report. To find them, use a dimension with segmentation by a new parameter named **Fraud assessment**.
- Added new metrics to the [Audience](../mobile-reports/audience-report.md) report:
   - **Dormant users**
   - **Resurrected users**
   - **Percentage of Dormant users**
   - **Percentage of Resurrected users**
- AppMetrica SDK for Android updated to version [7.3.0](../sdk/android/changelog-android.md#s-7-3-0).
- AppMetrica Push SDK for iOS updated to version [2.2.1](../sdk/ios/changelog-ios.md#v-push-2-2-1).
- You can now access instructions on how to [integrate the AppMetrica SDK](../sdk/react-native/analytics/quick-start.md#integration) into React Native/Expo apps.
- AppMetrica Gradle Plugin updated to version [1.0.0](../sdk/android/changelog-android.md#c-1-0-0).
- Added a new report on [ANR](../mobile-reports/anr.md) issues. This report helps you identify the most common scenarios where ANRs occur.

### October 2024 {#october-2024}

- AppMetrica SDK for iOS updated to version [5.8.2](../sdk/ios/changelog-ios.md#v-5-8-2).
- AppMetrica Push SDK for iOS updated to version [2.2.0](../sdk/ios/changelog-ios.md#v-push-2-2-0).
- AppMetrica SDK for Android updated to version [7.2.2](../sdk/android/changelog-android.md#s-7-2-2).
- AppMetrica SDK for React Native updated to version [3.3.0](../sdk/react-native/changelog.md#v-3-3-0).
- Added [integration with Yandex Ads SDK](ads-sdk-integration.md): automatic collection of basic and advertising events.
- Added the option to [import attributions from other SDKs](../data-collection/attribution-integration-react.md) for React Native to AppMetrica.
- You can now use postbacks to send [Ad Revenue events](../data-collection/about-adrevenue.md) to ad networks.

### September 2024 {#september-2024}

- Updated report interface.
- We've updated the list of metrics in the [Remarketing](../mobile-reports/remarketing-report.md) report:
   - The former **Deeplinks** metric has been renamed to **Re-engagement deeplinks**. This metric represents the number of clicks attributed to remarketing campaigns.
   - The **Re-engagements** metric has been renamed to **Re‑engaged users**. It represents the number of unique users with clicks attributed to remarketing campaigns.
   - A new metric has been added. It's called **Deeplinks** and displays the number of clicks on partner tracking URLs.
- In reports, you can now use grouping and segmentation by attribution source:
   - In dimensions: **Profile attributes** → **Install** → **Attribution source**.
   - In segments: **Users** → **Installation** → **Attribution source**.
- AppMetrica SDK for Android updated to version [7.2.0](../sdk/android/changelog-android.md#s-7-2-0).
- AppMetrica SDK for iOS updated to version [5.8.0](../sdk/ios/changelog-ios.md#v-5-8-0).
- AppMetrica Push SDK for iOS updated to version [2.1.0](../sdk/ios/changelog-ios.md#v-push-2-1-0).
- Updated the [{#T}](../mobile-api/logs/ref/profiles.md) resource in the Logs API. Added the required parameters `date_since` and `date_until` to resource version `profiles_v2`.
- [Added detection of deeplink attribution sources](../mobile-tracking/auto-create-tracking.md) based on data from URL parameters.
- AppMetrica Flutter SDK updated to version [3.1.0](../sdk/flutter/changelog.md#v-3-1-0).
- AppMetrica Flutter Push SDK updated to version [2.0.0](../sdk/flutter/changelog.md#v-push-2-0-0).
- AppMetrica SDK for Unity updated to version [6.3.0](../sdk/unity/changelog.md#v-6-3-0).
- AppMetrica SDK for React Native updated to version [3.2.0](../sdk/react-native/changelog.md#v-3-2-0).

{% cut "August–January 2024" %}

#### August 2024 {#august-2024}

- Added the [E-commerce](../mobile-api/logs/ref/ecommerce_events.md) data type to the Logs API.
- AppMetrica SDK for iOS updated to version [5.7.0](../sdk/ios/changelog-ios.md#v-5-7-0).
- Added [event verification](../data-collection/index.md#verification-events) for Android.
- Added a new parameter to the Data Stream API, `certificate_verification_status`, which returns the result of matching the target certificate footprint with the certificate footprint that came with the event.
- AppMetrica SDK for Android updated to version [7.1.0](../sdk/android/changelog-android.md#s-7-1-0). Added an [API for simplified sending of ILRD](../sdk/android/analytics/android-operations.md#send-adrevenue) (Impression Level Revenue Data) from Applovin MAX, Digital Turbine, and Google AdMob.
- AppMetrica Flutter SDK updated to version [3.0.0](../sdk/flutter/changelog.md#v-3-0-0).

#### July 2024 {#july-2024}

- Added the [Ad Revenue](../mobile-api/logs/ref/ad_revenue_events.md) data type to the Logs API.
- Added the [Ad Revenue](../mobile-api/datastream/data-type-fields.md#ad_revenue) and [ecommerce](../mobile-api/datastream/data-type-fields.md#ecommerce) data types to the Data Stream API.
- Added the `district` export field to the Data Stream API.
- Introduced a [limit](limits.md#limit-profile) of 500 profiles per device in AppMetrica.
- AppMetrica SDK for Unity updated to version [6.2.0](../sdk/unity/changelog.md#v-6-2-0).
- AppMetrica Push SDK for Android updated to version [4.0.0](../sdk/android/changelog-android.md#v-4-0-0).
- AppMetrica SDK React Native updated to version [3.1.0](../sdk/react-native/changelog.md#v-3-1-0).

#### June 2024 {#june-2024}

- Added new [macros](../mobile-tracking/postback-specification.md): `{start_datetime}`, `{start_timestamp}`, `{start_timezone}`, `{session_id}`, `{profile_id}`, `{ecom_type}`.
- AppMetrica SDK React Native updated to version [3.0.0](../sdk/react-native/changelog.md#v-3-0-0). Global plugin update. For more information, see the [migration instructions](../sdk/react-native/analytics/migration-io-3-0-0.md).
- Added the [Session end](../mobile-api/datastream/data-type-fields.md#session_end) data type to the Data Stream API.
- AppMetrica SDK for iOS updated to version [5.6.0](../sdk/ios/changelog-ios.md#v-5-6-0).
- AppMetrica SDK for Android updated to version [7.0.0](../sdk/android/changelog-android.md#s-7-0-0).

#### May 2024 {#may-2024}

- You can now [import attributions from other SDKs for Flutter](../data-collection/attribution-integration-flutter.md) to AppMetrica.
- Crash plugin updated to version [0.11.0](../sdk/android/changelog-android.md#c-0-11-0).
- AppMetrica Flutter SDK updated to version [2.1.1](../sdk/flutter/changelog.md#v-2-1-1).
- AppMetrica Flutter Push SDK updated to version [1.0.0](../sdk/flutter/changelog.md#v-push-1-0-0).
- AppMetrica SDK for Unity updated to version [6.1.0](../sdk/unity/changelog.md#v-6-1-0).
- AppMetrica Push SDK for Unity updated to version [2.0.0](../sdk/unity/changelog.md#p-2-0-0). Global plugin update. For more information, see the [migration instructions](../sdk/unity/push/migration-io-2-0-0.md).
- AppMetrica SDK for iOS updated to version [5.4.0](../sdk/ios/changelog-ios.md#v-5-4-0).
- AppMetrica Push SDK for Android updated to version [3.3.0](../sdk/android/changelog-android.md#v-3-3-0).

#### April 2024 {#april-2024}

- AppMetrica SDK for Android updated to version [6.5.0](../sdk/android/changelog-android.md#s-6-5-0).
- AppMetrica SDK for iOS updated to version [5.2.0](../sdk/ios/changelog-ios.md#v-5-2-0).
- AppMetrica SDK for Unity updated to version [6.0.1](../sdk/unity/changelog.md#v-6-0-1). Global plugin update. For more information, see the [migration instructions](../sdk/unity/analytics/migration-io-6-0-0.md).
- You can now [import attributions from other SDKs](../data-collection/attribution-integration.yaml) for iOS and Unity in AppMetrica.
- Added the [Revenue](../mobile-api/datastream/data-type-fields.md#revenue) data type to the Data Stream API.
- Added new export fields to the Data Stream API: `huawei_oaid`, `country`, `area`, `event_source`, and `appmetrica_sdk_version`.
- Added new export fields to the Logs API: `is_revenue_autocollected`, `revenue_event_type`, and `revenue_inapp_type` for Revenue.
- AppMetrica Push SDK for Android updated to version [3.2.0](../sdk/android/changelog-android.md#v-3-2-0).
- Crash plugin updated to version [0.10.0](../sdk/android/changelog-android.md#c-0-10-0).
- AppMetrica Push SDK for iOS updated to version [2.0.0](../sdk/ios/changelog-ios.md#v-push-2-0-0). Library ID and API updated. The library's been split into modules. For more information, see the [migration instructions](../sdk/ios/push/migration-io-push-2-0-0.md).

#### March 2024 {#march-2024}

- Added [tracking for Petal Ads campaigns](../mobile-tracking/petalads-settings.md).
- Added a new app pre-install type: PAI (Google Play Auto Install). Read more in [Pre-installing apps with PAI](../mobile-tracking/preinstalled-app-attr.md#pai).
- [Added detection of install attribution sources](../mobile-tracking/auto-create-tracking.md) based on data from URL parameters.
- AppMetrica SDK for Android updated to version [6.3.0](../sdk/android/changelog-android.md#s-6-3-0).
- AppMetrica SDK for iOS updated to version [5.1.0](../sdk/ios/changelog-ios.md#v-5-1-0).

#### February 2024 {#february-2024}

- AppMetrica SDK for iOS updated to version [5.0.0](../sdk/ios/changelog-ios.md#v-5-0-0). Library ID and API updated. Replaced the `com.yandex.mobile.appmetrica` package with `io.appmetrica`. For more information, see the [migration instructions](../sdk/ios/analytics/migration-io-5-0-0.md).
- Added information about [partners](../ad-network/partner-directory/performance-agencies.md) and [integrations](../ad-network/integrations/engines-and-environments.md).
- Crash plugin updated to version [0.9.0](../sdk/android/changelog-android.md#c-0-9-0).

#### January 2024 {#january-2024}

- AppMetrica SDK for Android updated to version [6.2.1](../sdk/android/changelog-android.md#s-6-2-1).
- You can now [import attributions from other SDKs](../data-collection/attribution-integration.yaml) for Android in AppMetrica.

{% endcut %}

## 2023 {#year-2023}

{% cut "November–March 2023" %}

#### November 2023 {#november-2023}

- You can now [attribute installs to impressions](../mobile-tracking/vta-tracking-specification.md).
- Data Stream API: added the `session_id` and `installation_id` export fields. Added a new data type: clicks and impressions.
- Reports now show more precise locations based on available IP addresses.
- Added new [parameters](../mobile-tracking/tracking-specification.md) and [macros](../mobile-tracking/postback-specification.md) for OAID-based attribution: `{oaid}`, `{oaid_sha1}`, `{oaid_md5}`.
- AppMetrica SDK for Android updated to version [6.1.0](../sdk/android/changelog-android.md#s-6-1-0).

#### October 2023 {#october-2023}

- Added interface notifications about changes in metrics. There are two types of notifications: timespent in new app versions and changes in the share of paying users.

#### September 2023 {#september-2023}

- [Data Stream API](../mobile-api/datastream/about.md): you can now view statistics in your organization account. You can also enable [payments for exceeding your selected quota](../mobile-api/datastream/limits.md).
- [Post API](../mobile-api/post/about.md) now offers several new features, including updating profile properties and transmitting in-app purchases and subscriptions, advertising revenue, and e-commerce events.
- - AppMetrica SDK for Android updated to version [6.0.0](../sdk/android/changelog-android.md#v-6-0-0). Updated the library ID, root package, and API. For more information, see the [migration instructions](../sdk/android/analytics/migration-io-6-0-0.md).

#### August 2023 {#august-2023}

- Introduced [Varioqub](../common/varioqub-app-about.md) experiments. You can now run A/B tests and remotely manage your app configuration. The SDK is now available for iOS and Android.
- Organization account updated. You can now flexibly adjust your pricing plan so you're only paying for the features you need. You can enable [workspaces](../mobile-reports/workspaces.md) (including saved reports), the advanced [experiment](../common/varioqub-app-about.md) plan, and the [Data Stream API](../mobile-api/datastream/about.md).

#### July 2023 {#july-2023}

- Push SDK for Android updated to version [2.3.1](../sdk/android/changelog-android.md#v-2-3-1).
- Organization account updated. You can now view subscription statistics and transfer apps to other organizations.
- [Custom events are now limited](../troubleshooting/limit-events.md) based on your pricing plan.
- Added the `device_latitude` and `device_longitude` parameters to the [Data Stream API](../mobile-api/datastream/about.md).
- Custom widgets for Cohort and Retention analyses added to [workspaces](../mobile-reports/workspaces.md).
- [Subscriptions](../data-collection/about-subscription.md): you can now configure postbacks for different subscription events.

#### June 2023 {#june-2023}

- Flutter SDK updated to version [1.3.0](../sdk/flutter/changelog.md#v-1-3-0).
- Flutter Push SDK updated to version [0.3.0](../sdk/flutter/changelog.md#v-push-0-3-0).
- Added the [organization account](../troubleshooting/troubleshooting.md#value-events), where you can view general statistics, extend custom event limits, and enable additional options.
- An organization account provides convenient tools to manage employees and access to your organization's apps.
- Extended pricing plans now include options for [workspaces](../mobile-reports/workspaces.md) and [saving reports](../mobile-reports/save-reports.md).

#### May 2023 {#may-2023}

- You can now beta test tracking the status and revenue of in-app subscriptions purchased through Google Play and the App Store. {% if tld == "ru" %}Learn more about this [feature](../data-collection/about-subscription.md) and how to configure it for [Google Play](../data-collection/subscription-android.md) and the [App Store](../data-collection/subscription-ios.md). {% endif %}
- AppMetrica SDK for iOS updated to version [4.5.2](../sdk/ios/changelog-ios.md#v-4-5-2).

#### April 2023 {#april-2023}

- Crash plugin updated to version [0.8.2](../sdk/android/changelog-android.md#c-0-8-2).

#### March 2023 {#march-2023}

- AppMetrica SDK for Android updated to version [5.3.0](../sdk/android/changelog-android.md#s-5-3-0).
- AppMetrica SDK for iOS updated to version [4.5.0](../sdk/ios/changelog-ios.md#v-4-5-0).

{% endcut %}

## 2022 {#2022}

{% cut "October–February 2022" %}

#### October 2022 {#october-2022}

- Unity SDK updated to version [5.2.0](../sdk/unity/changelog.md#v-5-2-0). Now supports the Ad Revenue API.
- Added a [dashboard](../mobile-reports/dashboard.md) with key app metrics in the interface.
- In [Smart Link](../mobile-tracking/add-tracker.md), added support for redirects in AppGallery and GetApps.
- Flutter SDK updated to version [1.1.0](../sdk/flutter/changelog.md#v-1-1-0). Now supports the Ad Revenue API.

#### September 2022 {#september-2022}

- Unity SDK updated to version [5.0.1](../sdk/unity/changelog.md#v-5-0-1).
- AppMetrica SDK for Android updated to version [5.2.0](../sdk/android/changelog-android.md#s-5-2-0).
- AppMetrica SDK for iOS updated to version [4.4.0](../sdk/ios/changelog-ios.md#v-4-4-0).
- [Revenue](../mobile-reports/revenue-report.md) reports now have metrics to track revenue from advertising monetization.

#### August 2022 {#august-2022}

- AppMetrica Push Unity updated to version [1.1.0](../sdk/unity/changelog.md#p-1-1-0).
- AppMetrica Push Flutter plugin updated to version [0.2.0](../sdk/flutter/changelog.md#v-push-0-2-0).

#### July 2022 {#july-2022}

- Push SDK for iOS updated to version [1.3.0](../sdk/ios/changelog-ios.md#v-push-1-3-0).
- Unity SDK updated to version [5.0.0](../sdk/unity/changelog.md#v-5-0-0).
- Flutter SDK updated to version [1.0.1](../sdk/flutter/changelog.md#v-1-0-1).
- Crash plugin updated to version [0.6.2](../sdk/android/changelog-android.md#c-0-6-2).
- AppMetrica SDK for Android updated to version [5.0.1](../sdk/android/changelog-android.md#s-5-0-1).

#### June 2022 {#june-2022}

- Push SDK for Android updated to version [2.2.0](../sdk/android/changelog-android.md#v-2-2-0).

#### May 2022 {#may-2022}

{% note info %}

Starting from Android AppMetrica SDK 5.0.0 and higher, `appmetrica_device_id` changes when the app is reinstalled on a mobile phone. This is due to new Google policies. For more information, see the [documentation](../troubleshooting/troubleshooting.md#change-device-id).

{% endnote %}

- AppMetrica SDK for Android updated to version [5.0.0](../sdk/android/changelog-android.md#s-5-0-0).
- Unity SDK updated to version [4.3.0](../sdk/unity/changelog.md#v-4-3-0).
- Crash plugin updated to version [0.6.1](../sdk/android/changelog-android.md#c-0-6-1).
- AppMetrica Push Unity updated to version [1.0.0](../sdk/unity/changelog.md#p-1-0-0).

#### April 2022 {#april-2022}

Updated the [Events](../mobile-reports/events-report.md) report:

- Dimension and metric builder now available.
- Added new metrics to analyze event parameters (sum, average, median, and unique values).
- Session type filter updated. The report now shows events from all sessions by default. Previously, background sessions were only counted in metrics for devices.

#### March 2022 {#march-2022}

- The [In-app and Ad Revenue](../mobile-reports/revenue-report.md) report has been updated. It's more of a builder now: you can combine various dimensions and display several metrics on the chart at the same time.
- Events sent using [Post API](../mobile-api/post/about.md) are now displayed in the [profile card](../mobile-reports/profile-list.md#profile-card).
- Push SDK for Android updated to version [2.1.1](../sdk/android/changelog-android.md#v-2-1-1).

#### February 2022 {#february-2022}

- AppMetrica SDK for Android updated to version [4.2.0](../sdk/android/changelog-android.md#s-4-2-0).
- AppMetrica SDK for iOS updated to version [4.2.0](../sdk/ios/changelog-ios.md#v-4-2-0).
- Unity SDK updated to version [4.2.0](../sdk/unity/changelog.md#v-4-2-0).
- Push SDK for Android updated to version [2.1.0](../sdk/android/changelog-android.md#v-2-1-0).
- Flutter SDK [0.1.0](../sdk/flutter/changelog.md#v-0-1-0) released.

{% endcut %}

## 2021 {#2021}

{% cut "December–April 2021" %}

#### December 2021 {#december-2021}

- Unity SDK updated to version [4.0.0](../sdk/unity/changelog.md#v-4-0-0).
- AppMetrica SDK for Android updated to version [4.1.1](../sdk/android/changelog-android.md#s-4-1-1).
- Unity SDK updated to version [4.1.0](../sdk/unity/changelog.md#v-4-1-0).
- [Engagement](../mobile-reports/engagement-report.md) reports now available.

#### November 2021 {#november-2021}

- Added Facebook* [tracking](../mobile-tracking/facebook-tracking.md) (Facebook is prohibited in the Russian Federation) for Android via Google Play Install Referrer.
- [Cohort analysis](../mobile-reports/cohort-report.md) and [Retention analysis](../mobile-reports/retention-report.md) reports now include geography, gender, age, operating system, and app version dimensions.
- [Cohort analysis](../mobile-reports/cohort-report.md) reports now include ARPU, number of purchases, and number of paying users metrics.
- Added new segmentation parameters for in-app purchases: purchase date, product, amount, currency, validation status, geography, and payload.
- [Unattributed postbacks](../mobile-tracking/postback-quota.md) can now be sent.
- You can now add [images to push notifications on iOS](../mobile-api/push/file-type.md) from AppMetrica.

#### October 2021 {#october-2021}

- Push SDK for Android updated to version [2.0.0](../sdk/android/changelog-android.md#v-2-0-0).
- [Funnels](../mobile-reports/funnels-report.md) reports now include events: installation, session start, deep link opening, in-app purchases, push notifications, e-commerce events, crashes, and errors.
- You can now specify the funnel window between the first and last event in the [Funnels](../mobile-reports/funnels-report.md) report.
- The [Data Export](../mobile-api/logs/about.md#export-data) tool now features a `profile_id` export field.

#### September 2021 {#september-2021}

- You can now [manage the conversion value](../mobile-tracking/conversion-value.md).
- Added automatic data collection for [in-app purchases](../data-collection/about-revenue.md) and [app openings via a deep link](../data-collection/deeplinks.md) with SDK 4.0.
- Push SDK for iOS updated to version [1.1.1](../sdk/ios/changelog-ios.md#v-push-1-1-1).

#### August 2021 {#august-2021}

- Added {% if locale == "ru" %}[email notifications](https://appmetrica.yandex.ru/blog/ru-email-notifications-about-app-errors-and-crashes){% endif %}{% if locale == "en" %}[email notifications](https://appmetrica.yandex.com/about/blog/en-email-notifications-about-app-errors-and-crashes){% endif %} about new crashes and app errors.
- You can now [export data](../common/cloud.md) from Yandex Cloud.
- You can now send [push notifications with file attachments](../sdk/ios/push/ios-push-download-file.md) on iOS.
- Added postbacks for in-app purchase events and new [advanced settings](../mobile-tracking/postback-specification.md#macros) to manage purchases data.

#### July 2021 {#july-2021}

- Added [instructions](../sdk/flutter/index.md) on how to enable AppMetrica analytics in apps built with Flutter.
- Users with Read access can now create and edit their own funnels.
- [User Acquisition by SKAdNetwork](../mobile-reports/user-acquisition-skadnetwork.md) reports are now available.
- Resolved the potential cause for apps being rejected from publishing to Google Play due to Implicit PendingIntent (Push SDK, Android 1.12.0).
- You can now add a test device for push notifications by IDFV and `appmetrica-device_id`.
- Updated Push SDK for iOS 0.9.2, iOS 1.0.0, and Android 1.13.0.

#### June 2021 {#june-2021}

- AppMetrica SDK for Unity (Unity 3.8.0) updated to iOS 3.16.0 and Android 3.21.1 versions.
- Added the `RequestTrackingAuthorization` method to request an IDFA on iOS (Unity 3.8.0).
- The reports table now features period dimensions: UA, Remarketing, and Purchase analysis.
- Now supports gradle 7 (AppMetrica Build Plugin 0.3.0).
- Now supports M1 (AppMetrica SDK, iOS 3.17.0).

#### May 2021 {#may-2021}

- Added [Apple Search Ads tracking](../mobile-tracking/searchads-settings.md) for iOS 14.5+ (AppMetrica SDK, iOS 3.15.1).
- Added the initWebViewReporting method for sending events from the WebView's JS code (AppMetrica SDK, iOS 3.16/Android 3.21).
- Now supports AGP 4.2 with errors fixed and stability improved (AppMetrica Build Plugin 0.2.4).

#### April 2021 {#april-2021}

- Tracking via SKAdNetwork now available (AppMetrica SDK, iOS 3.15).
- Added the option to set user profile IDs during activation (`YandexMetricaConfig.Builder#withUserProfileID`) or before activation (`YandexMetrica#setUserProfileID`) (AppMetrica SDK, Android 3.20.1).
- Incorrect deep link processing fixed (AppMetrica SDK, Android 3.20.1).

{% endcut %}

