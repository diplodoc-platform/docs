# Changelog

## AppMetrica SDK {#sdk}

### Version 6.4.0 {#v-6-4-0}

Released March 4, 2025

- Updated the AppMetrica Android SDK version to [7.7.0](../../sdk/android/changelog-android.md#s-7-7-0).
  - Fixed a possible issue with statistics (installations and new users) when using the AppMetrica Plugins (Unity, Flutter, ReactNative) and Yandex Ads Plugins at the same time.
  - The referrer processing mechanism has been improved, which has allowed us to fix the error of receiving a deferred deeplink and its parameters when installing an application via a tracking link on the latest versions of the browser with the chromium engine (Google Chrome, Yandex Browser, etc.).
  - Fixed couple of possible ANR and crashes
- Updated the AppMetrica iOS SDK version to [5.9.0](../../sdk/ios/changelog-ios.md#v-5-9-0).
  - Resolved a conflict between AppMetricaProtobuf and other libraries using protobuf-c.
- Added AppHud intergration for subscription tracking

### Version 6.3.0 {#v-6-3-0}

Released September 19, 2024

- Updated the AppMetrica Android SDK version to [7.2.0](../../sdk/android/changelog-android.md#s-7-2-0).
  - Adding forced sending of certain types of events to the server (attributions from external SDKs, e-commerce, revenue, ad revenue (Impression Level Revenue Data)).
- Updated the AppMetrica iOS SDK version to [5.8.0](../../sdk/ios/changelog-ios.md#v-5-8-0).
  - Removed iAd support and references to this library.
  - Added event parameters logging [GitHub Issue #2](https://github.com/appmetrica/appmetrica-unity-plugin/issues/2).
  - Updated KSCrash to version `2.0.0-rc.1`.
  - Removed domains from `NSPrivacyTrackingDomains` in the privacy manifest of the `AppMetricaCore` dependency to comply with Apple's privacy guidelines. 
  - Adding forced sending of certain types of events to the server (attributions from external SDKs, e-commerce, revenue, ad revenue (Impression Level Revenue Data), apple privacy).

### Version 6.2.0 {#v-6-2-0}

Released July 9, 2024

- Updated the AppMetrica Android SDK version to [7.0.0](../../sdk/android/changelog-android.md#s-7-0-0).
  - The current `minSdkVersion` has been increased to `21` (Android 5.0).
  - The `sourceCompatibility` and `targetCompatibility` versions have been increased to Java 1.8.
  - A limit of 100 events to be sent in a single server request has been introduced. Implementing this limit will enhance the SDK's performance under conditions of an unstable network connection.
  - Optimized client-side threading and removed outdated SDK integration checks. The optimization will reduce the time of the synchronous part of SDK activation.
- Updated the AppMetrica iOS SDK version to [5.6.0](../../sdk/ios/changelog-ios.md#v-5-6-0).
  - Fixed an error related to sending IDFA. IDFA was not always sent immediately after obtaining user consent for tracking. This could have affected the sending of test push notifications via IDFA.
  - Extensions now use background sessions by default.
- Added support for sending attribution from [Singular](../../data-collection/attribution-integration-unity#singular).

### Version 6.1.0 {#v-6-1-0}

Released May 15, 2024

- Updated the SDK version for Android ([AppMetrica SDK 6.5.0](../../sdk/android/changelog-android.md#s-6-5-0)) and iOS ([AppMetrica SDK 5.3.2](../../sdk/ios/changelog-ios.md#v-5-3-2)).
- Added helper classes, methods, and fields for the AppMetrica Push Unity plugin:
   - Added the `ActivationListener` delegate and the `ActivationConfig` and `OnActivation` fields to the `AppMetrica` class.
   - Added the `ToJsonString` method to the `AppMetricaConfig` class.
   - Added the following inner classes: `AppMetricaPushHelper` for Android and `AMAUAppMetricaPushHelper` for iOS.

### Version 6.0.1 {#v-6-0-1}

Released April 25, 2024

- Fixed a crash on launching a stage from Unity Editor [GitHub Issue #1](https://github.com/appmetrica/appmetrica-unity-plugin/issues/1).

### Version 6.0.0 {#v-6-0-0}

Released April 10, 2024

- Global plugin update. For more information, see the [migration instructions](analytics/migration-io-6-0-0.md).
- Updated the AppMetrica SDK version ([Android 6.4.0](../../sdk/android/changelog-android.md#s-6-4-0), [iOS 5.2.0](../../sdk/ios/changelog-ios.md#v-5-2-0)).
  - Added support for the Privacy Manifest in iOS.
- Added support for the [Unity Package Manager](https://docs.unity3d.com/Manual/Packages.html).
- Added support for an [Assembly definition](https://docs.unity3d.com/Manual/cus-asmdef.html).
- Removed the prefab. We recommend activating AppMetrica with [RuntimeInitializeOnLoadMethodAttribute](https://docs.unity3d.com/ScriptReference/RuntimeInitializeOnLoadMethodAttribute.html) instead.
- Added a new API for sending E-Commerce events.
- Added a new API for sending events to an additional API key.
- Added support for sending attributions from external libraries. To learn more, see [Integrating attributions from other SDKs](../../data-collection/attribution-integration-unity.md).

### Versions 5.2.0–5.0.0

{% cut "5.2.0–5.0.0" %}

#### Version 5.2.0 {#v-5-2-0}

Released October 3, 2022

- Updated the AppMetrica SDK version ([Android 5.2.0](../../sdk/android/changelog-android.md), [iOS 4.4.0](../../sdk/ios/changelog-ios.md)).
- Added the AdRevenue API for transmitting advertising monetization revenue: the `YandexAppMetricaAdRevenue` class and the method for sending AdRevenue `ReportAdRevenue(YandexAppMetricaAdRevenue adRevenue)`.

#### Version 5.0.1 {#v-5-0-1}

Released September 1, 2022

- Updated the AppMetrica SDK version ([Android 5.0.1](../../sdk/android/changelog-android.md)).
- Exceptions from Application.logMessageReceived are sent as errors.

#### Version 5.0.0 {#v-5-0-0}

Released July 16, 2022

- Updated the Android AppMetrica SDK version to ([Android 5.0.0](../../sdk/android/changelog-android.md)).
- Removed the `LocationService.Start` call.
- Stopped using `APP_METRICA_TRACK_LOCATION_DISABLED`.

{% endcut %}

### Versions 4.3.0–4.0.0

{% cut "4.3.0–4.0.0" %}

#### Version 4.3.0 {#v-4-3-0}

Released May 19, 2022

- Updated versions of the AppMetrica SDK ([Android 4.2.0](../../sdk/android/changelog-android.md), [iOS 4.2.0](../../sdk/ios/changelog-ios.md)).
- Added support for the [External Dependency Manager for Unity](https://github.com/googlesamples/unity-jar-resolver) to resolve dependencies.
- Improved crash handling.
- Added methods for sending errors: `ReportError(Exception exception, string condition)` and `ReportErrorFromLogCallback(string condition, string stackTrace)`.
- Added a method for sending `ReportUnhandledException(Exception exception)` crashes.
- The `ReportError(string condition, string stackTrace)` method is deprecated. Use the `ReportError(Exception exception, string condition)` method.
- The `ReportError(string groupIdentifier, string condition, string stackTrace)` method is deprecated. Use the `ReportError(string groupIdentifier, string condition, Exception exception)` method.

#### Version 4.2.0 {#v-4-2-0}

- Fixed a problem with downloading the app in the AppStore:

  ```
  YandexMobileMetrica.framework/YandexMobileMetrica' is not permitted. Your app can’t contain standalone executables or libraries, other than a valid CFBundleExecutable of supported bundles
  ```

#### Version 4.1.0 {#v-4-1-0}

- Updated versions of the AppMetrica SDK ([Android 4.1.1](../../sdk/android/changelog-android.md)).

#### Version 4.0.0 {#v-4-0-0}

- Updated versions of the AppMetrica SDK ([iOS 4.0.0](../../sdk/ios/changelog-ios.md), [Android 4.0.0](../../sdk/android/changelog-android.md)).
- Removed the `YandexAppMetricaConfig.InstalledAppCollecting` property.
- Added the `RevenueAutoTrackingEnabled` property to the [YandexAppMetricaConfig](analytics/methods.md#ClassYandexAppMetricaConfig) class. This enables the automatic collection and sending of information about In-App purchases.
- Added a dependency on the [Install Referrer Library](https://developer.android.com/google/play/installreferrer/library) 2.2 to the AppMetrica SDK for Android.

{% endcut %}

### Versions 3.8.0–3.0.0

{% cut "3.8.0–3.0.0" %}

#### Version 3.8.0 {#v-3-8-0}

- Updated AppMetrica SDK versions ([iOS 3.16.0](../../sdk/ios/changelog-ios.md), [Android 3.21.1](../../sdk/android/changelog-android.md)).
- Added the [RequestTrackingAuthorization](analytics/methods.md#idfa-request) method to request IDFA access on iOS.

#### Version 3.7.0 {#v-3-7-0}

- Updated versions of the AppMetrica SDK ([iOS 3.14.0](../../sdk/ios/changelog-ios.md), [Android 3.18.0](../../sdk/android/changelog-android.md)).
- Added methods:
    1. [void ReportEvent(string message, string json)](analytics/methods.md#ReportEvent) – sends an event with a value as a json string.
    2. [void PutErrorEnvironmentValue(string key, string value)](analytics/methods.md#PutErrorEnvironmentValue) – sets the error environment.
    3. [void ReportError(string groupIdentifier, string condition, string stackTrace)](analytics/methods.md#ReportEvent) and [void ReportError(string groupIdentifier, string condition, Exception exception)](analytics/methods.md#ReportEvent) — Methods for sending errors with an ID for grouping.

#### Version 3.6.0 {#v-3-6-0}

- Updated AppMetrica SDK versions ([iOS 3.11.1](../../sdk/ios/changelog-ios.md), [Android 3.14.3](../../sdk/android/changelog-android.md)).
- Added support for children's apps. Use the `AppForKids` property of the [YandexAppMetricaConfig](analytics/methods.md#ClassYandexAppMetricaConfig) class.

#### Version 3.5.1 {#v-3-5-1}

- Added the [ReportReferralUrl](analytics/methods.md#ReportReferralUrl) method.
- Added the [ReportAppOpen](analytics/methods.md#ReportAppOpen) method.
- Added a simplified connection of the iAd framework for iOS. For more information, see [Tracking Apple Search Ads campaigns](../../mobile-tracking/searchads-settings.md).
- Added the PriceDecimal property to the [YandexAppMetricaRevenue](analytics/methods.md#YandexAppMetricaRevenue) class. Use it instead of the deprecated Price.

#### Version 3.5.0 {#v-3-5-0}

- Updated versions of the AppMetrica SDK ([iOS 3.9.4](../../sdk/ios/changelog-ios.md), [Android 3.13.1](../../sdk/android/changelog-android.md)).

#### Version 3.4.0 {#v-3-4-0}

- Updated versions of the AppMetrica SDK ([iOS 3.7.1](../../sdk/ios/changelog-ios.md), [Android 3.6.4](../../sdk/android/changelog-android.md)).

#### Version 3.3.0 {#v-3-3-0}

- Updated versions of the AppMetrica SDK ([iOS 3.6.0](../../sdk/ios/changelog-ios.md), [Android 3.6.0](../../sdk/android/changelog-android.md)).

#### Version 3.2.0 {#v-3-2-0}

- Updated versions of the AppMetrica SDK ([iOS 3.4.0](../../sdk/ios/changelog-ios.md), [Android 3.4.0](../../sdk/android/changelog-android.md)).
- Fixed an issue with AppMetrica Push SDK integration for iOS.

#### Version 3.1.0 {#v-3-1-0}

- Updated versions of the AppMetrica SDK ([iOS 3.2.0](../../sdk/ios/changelog-ios.md), [Android 3.2.2](../../sdk/android/changelog-android.md)).
- Added a method to disable sending statistics.
- Added a method to retrieve the AppMetrica device ID (`appmetrica_device_id`).
- Added a method to force sending stored events from the buffer.

#### Version 3.0.1 {#v-3-0-1}

- Updated the iOS AppMetrica SDK version ([iOS 3.1.1](../../sdk/ios/changelog-ios.md)).
- Changed the SDK to meet the requirements of the Apple App Store Review Team. Update the plugin to avoid any issues during the App Store moderation process.

#### Version 3.0.0 {#v-3-0-0}

- Updated AppMetrica SDK versions ([iOS 3.1.1](../../sdk/ios/changelog-ios.md), [Android 3.1.0](../../sdk/android/changelog-android.md)).
- Added methods for creating user profiles.
- Added in-app [purchase tracking](analytics/unity-operations.md#send-revenue).
- Unified and revised the API.

{% endcut %}

## Push SDK {#push}

### Version 2.0.0 {#p-2-0-0}

Released May 15, 2024

- Global plugin update. For more information, see the [migration instructions](push/migration-io-2-0-0.md).
- Updated versions of the AppMetrica Push SDK ([Android 3.3.0](../android/changelog-android.md#v-3-3-0), [iOS 2.0.0](../ios/changelog-ios.md#v-push-2-0-0)).
  - Added support for the Privacy Manifest in iOS.
- Discontinued support for the AppMetrica Unity plugin lower than version 6.1.0.
- Added support for the [Unity Package Manager](https://docs.unity3d.com/Manual/Packages.html).
- Added support for an [Assembly definition](https://docs.unity3d.com/Manual/cus-asmdef.html).
- Removed the prefab. To activate AppMetrica Push, you should use the [RuntimeInitializeOnLoadMethodAttribute](https://docs.unity3d.com/ScriptReference/RuntimeInitializeOnLoadMethodAttribute.html) attribute instead.

### Version 1.1.0 {#p-1-1-0}

Released August 15, 2022

- Updated versions of the AppMetrica Push SDK ([iOS 1.3.0](../ios/changelog-ios.md#push-sdk), [Android 2.2.0](../android/changelog-android.md)).
- Added support for Unity 2022.1.
- Fixed plugin operation on devices with Android 7 and below due to the `java.lang.NoClassDefFoundError: android.app.NotificationChannel` error.

### Versions 1.0.0–0.1.0

{% cut "1.0.0–0.1.0" %}

#### Version 1.0.0 {#p-1-0-0}

Released May 27, 2022

- Updated the AppMetrica Push SDK versions ([iOS 1.1.1](../ios/changelog-ios.md#push-sdk), [Android 2.1.1](../android/changelog-android.md)).
- Discontinued support for the AppMetrica Unity plugin lower than version 4.0.0.
- Added support for the [External Dependency Manager for Unity](https://github.com/googlesamples/unity-jar-resolver) to resolve dependencies.

#### Version 0.2.0 {#p-0-2-0}

Released 11 July 2018

- Updated AppMetrica Push SDK versions ([iOS 0.6.0](../ios/changelog-ios.md#push-sdk), [Android 1.1.0](../android/changelog-android.md)).
- Stopped supporting AppMetrica Unity plugin lower than version 3.0.0.
- Stopped supporting iOS 7.

#### Version 0.1.1 {#p-0-1-1}

Released 19 November 2017

- Updated AppMetrica Push SDK versions ([iOS 0.5.0](../ios/changelog-ios.md#push-sdk), [Android 0.6.1](../android/changelog-android.md)).
- Added support for Android 8.
- Added the in-app notifications support for iOS 10 and higher.
- Update the GCM and support libraries versions.
- The minimum version of the Android API is 14.

#### Version 0.1.0 {#p-0-1-0}

Released 31 January 2017

- Integration with the AppMetrica SDK for the iOS and Android platforms.

{% endcut %}
