# Changelog

## Version 3.3.0 {#v-3-3-0}

Released October 4, 2024

- You can now [import attributions from other SDKs](../../data-collection/attribution-integration-react.md) to AppMetrica.

## Version 3.2.0 {#v-3-2-0}

Released September 25, 2024

- Updated the AppMetrica Android SDK version to [7.2.0](../../sdk/android/changelog-android.md#s-7-2-0).
  - Adding forced sending of certain types of events to the server (attributions from external SDKs, e-commerce, revenue, ad revenue (Impression Level Revenue Data)).
- Updated the AppMetrica iOS SDK version to [5.8.0](../../sdk/ios/changelog-ios.md#v-5-8-0).
  - Removed iAd support and references to this library.
  - Added event parameters logging.
  - Updated KSCrash to version `2.0.0-rc.1`.
  - Removed domains from `NSPrivacyTrackingDomains` in the privacy manifest of the `AppMetricaCore` dependency to comply with Apple's privacy guidelines [GitHub Issue #4](https://github.com/appmetrica/appmetrica-react-native-plugin/issues/4).
  - Adding forced sending of certain types of events to the server (attributions from external SDKs, e-commerce, revenue, ad revenue (Impression Level Revenue Data), apple privacy).

## Version 3.1.0 {#v-3-1-0}

Released July 11, 2024

- AppMetrica SDK for Android updated to version [7.0.0](../../sdk/android/changelog-android.md#s-7-0-0).
   - The current `minSdkVersion` has been upgraded to `21` (Android 5.0).
   - The `sourceCompatibility` and `targetCompatibility` versions have been upgraded to Java 1.8.
   - Added a limit of 100 events that can be sent to the server in a single request. The limit is imposed to improve the SDK performance when the network channel is unstable.
   - Optimized threading on the client side and removed deprecated SDK integration checks. The optimization is to reduce the time of synchronous SDK activation.
- AppMetrica SDK for iOS updated to version [5.6.0](../../sdk/ios/changelog-ios.md#v-5-6-0).
   - Extensions now use a background session by default.
- Added support for the API for sending [user profiles](analytics/react-native-operations.md#send-attribute-profile).
- Fixed `payload` sending to `ECommerce` and `AdRevenue` events, when it was set as `Map<string, string>`.
- Added support for the `Record<string, string>` type for `payload` in `ECommerce` and `AdRevenue` events.

## Version 3.0.0 {#v-3-0-0}

Released June 10, 2024

- Global plugin update. For more information, see the [migration instructions](analytics/migration-io-3-0-0.md).
- Added a description of the [integration of the AppMetrica SDK](../../sdk/react-native/analytics/quick-start.md#integration) into applications at React Native Expo.
- Updated the AppMetrica SDK version ([Android 6.5.0](../../sdk/android/changelog-android.md#s-6-5-0), [iOS 5.4.0](../../sdk/ios/changelog-ios.md#v-5-4-0)).
   - Added support for the Privacy Manifest in iOS.
- Added an API for sending E-commerce events.
- Added an API for sending Revenue events.
- Added an API for sending AdRevenue events.
- Fixed a bug that sometimes prevented the tracking of Android session startups.
- Added automatic tracking of deeplinks.

## Version 2.0.0 {#v-2-0-0}

Released 8 June 2020

- Integration with the AppMetrica SDK for the iOS and Android platforms.
