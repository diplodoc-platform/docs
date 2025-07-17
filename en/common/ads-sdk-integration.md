# Integration with Yandex Ads SDK

You can use the analytical capabilities of AppMetrica without separately initializing the AppMetrica SDK, if you have Yandex Mobile Ads SDK version 7.6.0 or higher, or one of the plugins:

- Unity Ads SDK version 7.10.0 or higher; 
- React Ads SDK version 7.10.0 or higher;
- Flutter Ads SDK version 7.9.0 or higher.

You can also access the automatically collected ad interaction events.

Key features:

1. Automatic tracking of [basic events](../data-collection/index.md): installations, session starts and ends, deeplinks, in-app purchases.

    Event tracking will start automatically when you initialize the Yandex Mobile Ads SDK in the app. To do this, activate the integration in the AppMetrica interface. You don't need to update the app code.

2. Automatic tracking of Yandex Mobile Ads SDK interaction events: ad requests, responses, impressions, clicks.

    Apps synchronized with the Yandex Mobile Ads SDK will automatically send data to AppMetrica.

    If you manually initialize the AppMetrica SDK in your app, data will start flowing automatically, as long as the Yandex Mobile Ads SDK is also initialized and synchronization with Yandex Mobile Ads is enabled in the AppMetrica settings.

## If you are using AppMetrica in the app {#already-using}

1. Update the platform Yandex Mobile Ads SDK to version 7.6.0 or higher, or one of the plugins you need:

    - Unity Ads SDK — to version [7.10.0](https://ads.yandex.com/helpcenter/{{locale}}/dev/unity/changelog-unity#2025) or higher;
    - React Ads SDK — to version [7.10.0](https://ads.yandex.com/helpcenter/{{locale}}/dev/react-native/changelog-react-native#2025) or higher;
    - Flutter Ads SDK — to version {% if locale=="ru" %}[7.9.0](https://ads.yandex.com/helpcenter/ru/dev/flutter/changelog-flutter#versiya-790-12-fevralya,-2025){% elsif locale=="en" %}[7.9.0](https://ads.yandex.com/helpcenter/en/dev/flutter/changelog-flutter#version-790-february-12,-2025){% else %}7.9.0{% endif %} or higher. 

1. Go to **{{ settings }}** and add the connection with the Yandex Mobile Ads app under **{{ syncing-the-ads-sdk }}**.

    - Use the same Yandex ID you used to [register](https://appmetrica.yandex.com/application/new) your app in Yandex Mobile Ads.

    - Make sure that you have completed the [app ownership verification]({{ helpcenter-quickstart-step3 }}) process.

1. New data on the interaction with Yandex Mobile Ads SDK will appear in the **{{ report-events }}** report within a few minutes. These events don't count towards the [event limits](limits.md#limit-events).

If necessary, you can disable data collection using the method [setAppAdAnalyticsReporting](https://yastatic.net/s3/doc-binary/src/dev/mobile-ads/ru/javadoc/com/yandex/mobile/ads/common/MobileAds.html#setAppAdAnalyticsReporting(java.lang.Boolean)) for Android and method [setAppAdAnalyticsReportingEnabled](https://yastatic.net/s3/doc-binary/src/dev/mobile-ads/ru/jazzy/Classes/MobileAds.html#/c:@M@YandexMobileAds@objc(cs)YMAMobileAds(cm)setAppAdAnalyticsReportingEnabled) for iOS in the Yandex Mobile Ads SDK configuration or remove the connection in the synchronization settings.

## If you haven't used AppMetrica before {#not-using}

Activate integration when registering in the AppMetrica interface.

1. Update the platform Yandex Mobile Ads SDK to version 7.6.0 or higher, or one of the plugins you need:

    - Unity Ads SDK — to version [7.10.0](https://ads.yandex.com/helpcenter/{{locale}}/dev/unity/changelog-unity#2025) or higher;
    - React Ads SDK — to version [7.10.0](https://ads.yandex.com/helpcenter/{{locale}}/dev/react-native/changelog-react-native#2025) or higher;
    - Flutter Ads SDK — to version {% if locale=="ru" %}[7.9.0](https://ads.yandex.com/helpcenter/ru/dev/flutter/changelog-flutter#versiya-790-12-fevralya,-2025){% elsif locale=="en" %}[7.9.0](https://ads.yandex.com/helpcenter/en/dev/flutter/changelog-flutter#version-790-february-12,-2025){% else %}7.9.0{% endif %} or higher.   

1. Make sure that you have completed the [app ownership verification]({{ helpcenter-quickstart-step3 }}) process.

1. Register in AppMetrica with the same Yandex ID you used to [register](https://appmetrica.yandex.com/application/new) your app in Yandex Mobile Ads.

    At step 1, you'll see a notification telling you that you can connect the Yandex Ads SDK. If you don't see it, check if you're using a different username or if the app wasn't verified.

1. At step 3 **{{ syncing-the-ads-sdk }}**, specify from which apps with Ads SDK you want to send statistics to AppMetrica.

    We recommend selecting all platforms (for example, iOS and Android) for your app. You can add more apps at step 5.

1. Once you've registered, AppMetrica will start collecting statistics within a few minutes. You don't need to update the app code.

1. If you want to send [additional data](../data-collection/index.md) to AppMetrica, such as custom [events](../data-collection/about-events.md), use the corresponding methods. You don't need to initialize AppMetrica to do this.

1. If you want to use the advanced configuration capabilities of AppMetrica, [initialize AppMetrica](../common/quick-start.md#integration-sdk) manually using the API Key specified in the **{{ settings }}** → **{{ main }}** section.

## Yandex Mobile Ads SDK automatic events {#auto-events}

Available events and their parameters:

- `ad_request`: Ad request from an app.

  - `ad_type`: Ad type, such as `banner`, `interstitial`, `native`, or `rewarded`.
  - `block_id`: Ad space ID.
  - `sdk_version`: Yandex Mobile Ads SDK version.

- `ad_attempt`: Successful ad request to the ad network.

  - `ad_type`: Ad type, such as `banner`, `interstitial`, `native`, or `rewarded`.
  - `block_id`: Ad space ID.
  - `sdk_version`: Yandex Mobile Ads SDK version.
  - `ad_network`: Ad network that provides ads.

- `ad_filled_request`: Ad request that resulted in ad selection.

  - `ad_type`: Ad type, such as `banner`, `interstitial`, `native`, or `rewarded`.
  - `block_id`: Ad space ID.
  - `sdk_version`: Yandex Mobile Ads SDK version.
  - `ad_network`: Ad network that provides ads.
  - `banner_id`: Banner ID.

- `ad_impression`: Ad impression.

  - `ad_type`: Ad type, such as `banner`, `interstitial`, `native`, or `rewarded`.
  - `block_id`: Ad space ID.
  - `sdk_version`: Yandex Mobile Ads SDK version.
  - `ad_network`: Ad network that provides ads.
  - `banner_id`: Banner ID.
  - `ad_revenue`: Revenue for ad impressions in the advertising network's currency.
  - `currency`: Advertising network's currency.
  - `precision`: The accuracy of `ad_revenue` value. Acceptable values: `publisher_defined`, which is a value based on the CPM threshold from the mediation interface, and `estimated`, which is a value based on automated strategies.

- `ad_click`: Click on an ad.

  - `ad_type`: Ad type, such as `banner`, `interstitial`, `native`, or `rewarded`.
  - `block_id`: Ad space ID.
  - `sdk_version`: Yandex Mobile Ads SDK version.
  - `ad_network`: Ad network that provides ads.
  - `banner_id`: Banner ID.

- `ad_reward`: Accrual of rewards for viewing "rewarded" ads.

  - `ad_type`: Ad type, such as `banner`, `interstitial`, `native`, or `rewarded`.
  - `block_id`: Ad space ID.
  - `sdk_version`: Yandex Mobile Ads SDK version.
  - `ad_network`: Ad network that provides ads.

## Learn more {#learn-more}

- [How do I use the advanced configuration features of the AppMetrica SDK?](../troubleshooting/troubleshooting.md#yads-sdk-extended)
- [Should I make any changes to the integration if I'm already using the AppMetrica SDK in the app?](../troubleshooting/troubleshooting.md#yads-sdk-already-using)
- [How do I disable Yandex Ads SDK automatic events?](../troubleshooting/troubleshooting.md#yads-sdk-disable-auto)
- [How to initialize the AppMetrica SDK using logic that's different from the Yandex Mobile Ads SDK initialization?](../troubleshooting/troubleshooting.md#yads-sdk-other-logic)

{% include notitle [feedback](../_includes/feedback-button.md) %}
