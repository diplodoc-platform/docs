# Changelog

## AppMetrica SDK {#sdk}

### Version 5.11.0 {#v-5-11-0}

Released May 22, 2025

- Added support for double-escaping in reattribution parameters.
- Added support for future auto-collection of ad revenue data from plugins.
- Custom location passed via `AppMetrica.setCustomLocation(Location)` is now sent with events even if location tracking is disabled via `AppMetrica.setLocationTrackingEnabled(Boolean)` or `AppMetricaConfiguration.setLocationTracking(Boolean)`.

### Version 5.10.0 {#v-5-10-0}

Released April 21, 2025

- Added the ability to disable IDFA usage in `AppMetricaLibraryAdapter`.
- Updated KSCrash dependency to version 2.0.0.
- Added the module `AppMetricaScreenshot` to detect when a user takes a screenshot.
- Migrated hashing algorithm from MD5 to SHA256.
- Fixed an issue that caused session counter rollback during consecutive migration to version 5.0 and then to 5.8.0+.
- Fixed a bug in sending internal TransactionFailure events and improved crash delivery reliability.
- Increased deployment_target for iOS and tvOS to version 13.0.

### Version 5.9.0 {#v-5-9-0}

Released December 12, 2024

- Implemented identifier sharing between the application and its extension.
- Resolved a conflict between `AppMetricaProtobuf` and other libraries using `protobuf-c`.
- Enhanced internal error reporting with more detailed information.
- Improved validation of the application environment.

### Version 5.8.2 {#v-5-8-2}

Released October 25, 2024

- Technical release.

### Version 5.8.1 {#v-5-8-1}

Released October 3, 2024

- Fixed sending `EVENT_UPDATE` instead of `EVENT_INIT` for API key 42.

### Version 5.8.0 {#v-5-8-0}

Released September 12, 2024

- Updated `KSCrash` to version `2.0.0-rc.1`.
- Removed domains from NSPrivacyTrackingDomains in the privacy manifest of the AppMetricaCore dependency to comply with Apple's privacy guidelines.
- Added `AppMetricaLibraryAdapter` for integration with third-party libraries.
- Adding forced sending of certain types of events to the server (attributions from external SDKs, e-commerce, revenue, ad revenue (Impression Level Revenue Data), apple privacy).

### Version 5.7.1 {#v-5-7-1}

Released November 7, 2024

- Removed domains from NSPrivacyTrackingDomains in the privacy manifest of the AppMetricaCore dependency to comply with Apple's privacy guidelines.

### Version 5.7.0 {#v-5-7-0}

Released August 3, 2024

- Removed iAd support and references to this library.
- Added event parameters logging.

### Version 5.6.0 {#v-5-6-0}

Released June 27, 2024

- `AppMetricaConfiguration` now includes the `appEnvironment` property, which sets the app environment for all events from the moment of activation.

### Version 5.5.0 {#v-5-5-0}

Released June 26, 2024

- Extensions now use a background session by default.
- Added a dSYM upload tool to AppMetricaCrashes.

### Version 5.4.0 {#v-5-4-0}

Released May 24, 2024

- Fixed an error related to sending IDFA. IDFA was not always sent immediately after obtaining user consent for tracking. This could have affected the sending of test push notifications via IDFA.

### Version 5.3.2 {#v-5-3-2}

Released May 13, 2024

- Fixed a crash in `[AMAReportersContainer restartPrivacyTimer]`.
- File logging is disabled by default to prevent potential crashes caused by insufficient disk space.

### Version 5.3.1 {#v-5-3-1}

Released May 6, 2024

- Fixed module validation error for AppMetrica_FMDB, AppMetrica_Protobuf in the App Store when delivering data via SPM.

### Version 5.3.0 {#v-5-3-0}

Released April 26, 2024

- Singular support for external attributions: Added the functionality to send attributions from Singular:
   ```
   AppMetrica.reportExternalAttribution(attributionData, from: .singular) { error in
       print("AppMetrica reporting error: \(error)")
   }
   ```
- Assert correction: Removed internal asserts to optimize the code and prevent potential errors at development stage.
- KSCrash update: Changed the dependency on KSCrash version from a strict setting to a flexible range: ~> 1.17.0.

### Version 5.2.0 {#v-5-2-0}

Released April 16, 2024

- You can now [import attributions from other SDKs](../../data-collection/attribution-integration.yaml) for iOS in AppMetrica.
- Added the following for operations with external attributions: a method named `AppMetrica.reportExternalAttribution(_:from:onFailure:)` ([Swift](../ios/analytics/swift/AppMetrica.md#method_reportexternalattribution__from__onfailure), [Objective-C](../ios/analytics/objectivec/AMAAppMetrica.md#method_reportexternalattribution__source__onfailure)), struct/typedef `AttributionSource` ([Swift](../ios/analytics/swift/AttributionSource.md), [Objective-C](../ios/analytics/objectivec/AMAAttributionSource.md)).

### Version 5.1.0 {#v-5-1-0}

Released March 6, 2024

- Added support for the [Privacy Manifest](https://developer.apple.com/documentation/bundleresources/privacy_manifest_files).

### Version 5.0.0 {#v-5-0-0}

Released February 13, 2024

- Updated the library ID and API. For more information, see the [migration instructions](analytics/migration-io-5-0-0.md).

### Version 4.5.2 {#v-4-5-2}

Released May 22, 2023

- Fixed `posix_spawn` Xcode crash with sanitizer enabled.

### Version 4.5.0 {#v-4-5-0}

Released March 21, 2023

- Fixed the `locationServicesEnabled invoked on the main thread` error on iOS 16.

### Version 4.4.0 {#v-4-4-0}

Released September 19, 2022

- Added the AdRevenue API for transmitting advertising monetization revenue at the impression level (Impression-Level Revenue Data):
   - The `YMMAdRevenueInfo` and `YMMMutableAdRevenueInfo` classes.
   - The `reportAdRevenue` method in the `YMMYandexMetrica`, `reportAdRevenue` class in the `YMMYandexMetricaReporting` protocol.
   - The `YMMAdType` enumeration.

### Version 4.2.0 {#v-4-2-0}

Released February 18, 2022

- Added a new API to track crashes and errors from random plugins.

   Protocols:
   - `YMMYandexMetricaPlugins`.
   - `YMMYandexMetricaPluginReporting`.

   Classes:
   - `YMMPluginErrorDetails`.
   - `YMMStackTraceElement`.

- Added the API for the correct SDK functioning in the context of session auto-tracking if activated from plugins: `YMMYandexMetricaPlugins.handlePluginInitFinished`.
- Added the ability to send errors from reporters without activating the master key. In this case, meta information from KSCrash (system data) will be missing.

### Versions 4.0.0 — 3.0.0

{% cut "4.0.0 — 3.0.0" %}

#### Version 4.0.0 {#v-4-0-0}

Released September 20, 2021

- Supported the option to set the user profile ID when activating (`[YMMYandexMetricaConfiguration userProfileID]`) or before activating (`[YMMYandexMetrica setUserProfileID]`) the master key, as well as when activating the reporter (`[YMMReporterConfiguration userProfileID]`).
- Added the `appOpenTrackingEnabled` property for automatic tracking of app openings via a deeplink.
- Added the `revenueAutoTrackingEnabled` property for the automatic collection of data on In-App purchases.
- Added [managing the Conversion Value](../../mobile-tracking/conversion-value.md).

#### Version 3.17.0 {#v-3-17-0}

Released June 8, 2021

- Fixed a possible bug
   ```
   Main Thread Checker: UI API called on a background thread: -[WKUserScript initWithSource:injectionTime:forMainFrameOnly:]
   ```
- Added a library version for iOS simulators that are run on Apple Silicon M1 Macs (`ios-arm64-simulator`).
- The library is now delivered only as an XCFramework, which caused the following changes:
   - The minimum supported version of CocoaPods is 1.10 and Carthage is 0.38. These versions now support XCFrameworks.
   - The AppMetrica SDK is now connected on tvOS the same way as on iOS: the `YandexMobileMetrica/Dynamic-TV` and `YandexMobileMetrica/Static-TV` subspecs are no longer available.

#### Version 3.16.0 {#v-3-16-0}

Released May 27, 2021

- Added the `initWebViewReporting` method for sending events from the WebView's JS code.
- Fixed errors and improved stability.

#### Version 3.15.1 {#v-3-15-1}

Released April 20, 2021

- Improved Apple Search Ads attribution via AdServices Framework. Upgrade to this version to keep Apple Search Ads tracking on iOS 14.5+.

#### Version 3.15.0 {#v-3-15-0}

Released March 30, 2021

- Added support for attributing installs on devices running iOS version 14.5+ via [SKAdNetwork](https://developer.apple.com/documentation/storekit/skadnetwork). Upcoming versions of the SDK will make it possible to transmit conversion values.
- Data can now be received for attributing installs from Apple Search Ads via [AdServices Framework](https://developer.apple.com/documentation/adservices) (for devices running iOS 14.3+). Attribution is implemented in the AppMetrica backend and doesn't require further updates.
- Operator and Connection type collection is disabled.

#### Version 3.14.0 {#v-3-14-0}

Released 29 December 2020.

- Added AppMetrica distribution using Swift Package Manager. For more information, see [Installation and initialization](analytics/quick-start.md).
- The minimum supported iOS version is 9.0 or later.
- Fixed an issue in linking crashes to sessions.

#### Version 3.12.0 {#v-3-12-0}

Released 14 October 2020

- Added a new API for sending E-Commerce events:
   - Added the `+reportECommerce:onFailure:` method to the `YMMYandexMetrica` class and the `YMMYandexMetricaReporting` protocol.
   - Added new classes:
      - `YMMECommerce`.
      - `YMMECommerceAmount`.
      - `YMMECommerceCartItem`.
      - `YMMECommerceOrder`.
      - `YMMECommercePrice`.
      - `YMMECommerceProduct`.
      - `YMMECommerceReferrer`.
      - `YMMECommerceScreen`.

   For more information about E-Commerce events, see [E-commerce](../../data-collection/about-ecommerce.md).

- Improved the performance of the library and the quality of statistical data.

#### Version 3.11.1 {#v-3-11-1}

Released 8 July 2020

- Added a new API for sending crashes and errors:
   - The `YMMError` class.
   - The `YMMErrorRepresentable` protocol.
   - The `YMMErrorReportingOptions` enumeration.
   - The `YMMBacktraceErrorKey` constant.
   - Added the following methods to the `YMMYandexMetrica` class and `YMMYandexMetricaReporting` protocol:
      - `+reportError:onFailure:`.
      - `+reportError:options:onFailure:`.
      - `+reportNSError:onFailure:`.
      - `+reportNSError:options:onFailure:`.
      - `+setErrorEnvironmentValue:forKey:`.
   - Added the `maxReportsInDatabaseCount` property to the `YMMYandexMetricaConfiguration`, `YMMReporterConfiguration`, and `YMMMutableReporterConfiguration` classes.
- Stopped supporting the `+reportError:exception:onFailure` method. Use the new `+reportError:onFailure:`, `+reportError:options:onFailure:`, `+reportNSError:onFailure:`, or `+reportNSError:options:onFailure:` methods instead.
- Added support for children's apps. Use the `appForKids` property of the `YMMYandexMetricaConfiguration` configuration. For more information, see [Usage examples](analytics/ios-operations.md).
- Fixed support for tvOS.
- Improved the performance of the library and the quality of statistical data.

#### Version 3.9.4 {#v-3-9-4}

Released 3 February 2020

- Fixed possible crashes in AppMetrica SDK 3.9.1 and 3.9.2.

#### Version 3.9.2 {#v-3-9-2}

Released 27 December 2019

- Fixed incorrect `appmetrica_device_id` generation process.
- Fixed possible deadlock during the activation.
- The `reportReferralUrl` method is no longer deprecated.
- Fixed getting information about `code` and `sudcode` for Mach exceptions.
- Fixed framework for tvOS.
- Improved the performance of the library and the quality of statistical data.

#### Version 3.8.2 {#v-3-8-2}

Released 4 October 2019

- Fixed a `priceDecimal` serialization error that caused negative Revenue values.

#### Version 3.8.1 {#v-3-8-1}

Released 30 September 2019

- Fixed an issue in the dynamic framework.
- Fixed collection of information on location. When you set your own location, automatic detection is disabled.

#### Version 3.8.0 {#v-3-8-0}

Released 25 September 2019

- Added the `helper` command-line tool for [Uploading dSYM files on iOS](../../data-collection/upload-dsym.md).

#### Version 3.7.1 {#v-3-7-1}

Released 11 July 2019

- Added to the `YMMRevenueInfo` class:
   - The `-initWithPriceDecimal:currency:` method. Use it instead of the deprecated `‑initWithPrice:currency:` method.
   - The `-initWithPriceDecimal:currency:quantity:productID:transactionID:receiptData:payload:` method. Use it instead of the deprecated `-initWithPrice:currency:quantity:productID:transactionID:receiptData:payload:` method.
   - The `priceDecimal` property. Use it instead of the deprecated `price` property.

- Added methods for manual control of sessions to the `YMMYandexMetrica` class:
   - The `+pauseSession:` method.
   - The `+resumeSession:` method.

- Added properties for control of sessions to the `YMMYandexMetricaConfiguration` class:
   - The `handleActivationAsSessionStart` property.
   - The `sessionsAutoTracking` property.
- Stopped supporting the `+reportReferralUrl:` method. Deprecated method.
- Fixed the issue with additional information in crash logs: `active_time_since_launch`, `active_time_since_last_crash`, and others.

#### Version 3.6.0 {#v-3-6-0}

Released 18 February 2019

- Fixed possible loss of crash reports on devices with a 32-bit processor.
- Fixed possible crashes which affected the AppMetrica SDK versions 3.1.0 to 3.5.0.
- Improved the performance of the library and the quality of statistical data.

#### Version 3.5.0 {#v-3-5-0}

Released 25 December 2018

- Added support for tvOS 9 and higher.
- Improved the performance of the library and the quality of statistical data.

#### Version 3.4.1 {#v-3-4-1}

Released 15 November 2018

- Fixed the [issue](https://github.com/yandexmobile/metrica-sdk-ios/issues/76) when enabling the static framework in a project using Swift.

#### Version 3.4.0 {#v-3-4-0}

Released 2 November 2018

- Separated the library into two frameworks: core and crash-handling. For more information, see [Installation and initialization](../ios/analytics/quick-start.md).
- Fixed the `+sendEventsBuffer:` method to work correctly in the background.
- Improved the performance of the library and the quality of statistical data.

#### Version 3.3.0 {#v-3-3-0}

Released 6 September 2018

- Improved processing of information transmitted by the `+reportUserProfile:onFailure:` and `+reportRevenue:onFailure:` methods.
- Improved the performance of the library and the quality of statistical data.

#### Version 3.2.0 {#v-3-2-0}

Released 20 July 2018

- Added the `+setStatisticsSending:` method to disable statistics sending.
- Added the `+requestAppMetricaDeviceIDWithCompletionQueue:block:` method to retrieve the AppMetrica device ID (`appmetrica_device_id)`.
- Added the `+sendEventsBuffer:` method to force sending stored events from the buffer.
- Improved the performance of the library and the quality of statistical data.

#### Version 3.1.2 {#v-3-1-2}

Released 2 July 2018

- Changed the SDK to meet the requirements of the Apple App Store Review Team. Update the AppMetrica SDK to avoid any issues during the App Store moderation process.

   {% note alert %}

   Previous versions of iOS SDK (2.8.0–3.1.1) are not available for download. If you're using library version 2.9.x, update the SDK to version 2.9.8.

   {% endnote %}

#### Version 3.1.1 {#v-3-1-1}

Released 13 June 2018

- Fixed an issue in the AppMetrica SDK 3.1.0 related to internal data loss.

#### Version 3.1.0 {#v-3-1-0}

Released 8 June 2018

- Added deeplink attribution (Re-engagement).
- Fixed a possible deadlock affecting AppMetrica SDK versions 3.0.0 and 3.0.1.
- Improved the performance of the library and the quality of statistical data.

#### Version 3.0.1 {#v-3-0-1}

Released 21 May 2018

- Improved the stability of the library.

#### Version 3.0.0 {#v-3-0-0}

Released 18 April 2018

- Added methods for creating user profiles.
- Added revenue tracking.
- Unified and revised the API.
- Changed the app version and build number order in crash reports to match the Apple format.
- Extended logging of events flow.
- Stopped supporting iOS 6 and iOS 7.
- Improved the performance of the library and the quality of statistical data.

{% endcut %}

## Push SDK {#push}

### Version 3.1.0 {#v-push-3-1-0}

Released May 15, 2025

- Deployment target updated to iOS 13.

### Version 3.0.2 {#v-push-3-0-2}

Released February 27, 2025

- Fixed opening url.

### Version 3.0.0 {#v-push-3-0-0}

Released January 17, 2025

- The mode with storing notifications in shared App Group has been removed. Only the mode of operation in which events are sent directly to AppMetrica is supported (requires [setup](analytics/ios-appgroup.md)). 
- Dependency version updated: AppMetrica-5.9.0.

### Version 2.2.1 {#v-push-2-2-1}

Released November 1, 2024

- Technical release.

### Version 2.2.0 {#v-push-2-2-0}

Released October 10, 2024

- Added removal of delivered notifications via silent push.

### Version 2.1.0 {#v-push-2-1-0}

Released September 23, 2024

- Increased frequency of sending push delivery events.

### Version 2.0.0 {#v-push-2-0-0}

Released April 15, 2024

- Library ID and API updated. The library's been split into modules. For more information, see the [migration instructions](push/migration-io-push-2-0-0.md).
- Added support for the [Privacy Manifest](https://developer.apple.com/documentation/bundleresources/privacy_manifest_files).

### Version 1.3.0 {#v-push-1-3-0}

Released July 1, 2022

- Added the `YMPYandexMetricaPush.handleSceneWillConnectToSession` method to work with [UIScene](https://developer.apple.com/documentation/uikit/uiscene) (with iOS 13 or higher).

### Version 1.1.1 {#v-push-1-1-1}

Released September 29, 2021

- Added support for AppMetrica SDK [4.0.0](#v-4-0-0).

### Versions 1.0.0 — 0.3.0

{% cut "1.0.0 — 0.3.0" %}

#### Version 1.0.0 {#v-push-1-0-0}

Released 13 July 2021

- The minimum supported iOS version is 9.0 or later.
- The library is now delivered only as an XCFramework, which caused the following changes:
   - The minimum supported version of CocoaPods is 1.10 and Carthage is 0.38. These versions now support XCFrameworks.
- Added a library version for iOS simulators that are run on Apple Silicon M1 Macs (`ios-arm64-simulator`).
- Added Push SDK distribution using Swift Package Manager. For more information, see [Installation and initialization](push/quick-start.md).

#### Version 0.9.2 {#v-push--0-9-2}

Released 12 July 2021

- Added the feature to upload attached files in push notifications using the `downloadAttachmentsForNotificationRequest` method for iOS 10 and higher. See an example of integration in the article [Uploading attached files](push/ios-push-download-file.md).

#### Version 0.8.0 {#v-push-0-8-0}

Released 26 April 2019

- Added the feature for push notification tracking with the custom [UNUserNotificationCenterDelegate](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate?language=objc) implementation:
   - Added the `+userNotificationCenterHandler` method.
   - Added the `YMPUserNotificationCenterHandling` protocol.

#### Version 0.7.2 {#v-push-0-7-2}

Released 27 November 2018

- Fixed an issue in the dynamic framework.

#### Version 0.7.1 {#v-push-0-7-1}

Released 19 November 2018

- Added a proxy delegate for [userNotificationCenter:openSettingsForNotification:](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/2981869-usernotificationcenter?language=objc) (`YMPUserNotificationCenterDelegate`).
- Fixed crash on setting a `nil` token to the `+setDeviceTokenFromData:` method.
- Added support for [AppMetrica SDK 3.4.0](#v3-4-0).

#### Version 0.7.0 {#v-push-0-7-0}

Released 31 August 2018

- Added the tracking of the [shows/dismisses of the push notifications](push/ios-settings.md) for iOS 10 and higher.

#### Version 0.6.0 {#v-push-0-6-0}

Released 20 April 2018

- Added support for [AppMetrica SDK 3.0.0](#v-3-0-0).

#### Version 0.5.1 {#v-push-0-5-1}

Released 21 March 2018

- Fixed crash when opening URL from push notification.
- Fixed a bug that occurs when a URL of the same push notification is opened more than once.

#### Version 0.5.0 {#v-push-0-5-0}

Released 26 October 2017

- Added the in-app notifications support for iOS 10 and higher. Requires [additional integration](push/quick-start.md#opening).
- Added a method for identification of push notifications related to [AppMetrica Push SDK](push/quick-start.md).
- Added a method for sending an APNs (Apple Push Notifications service) environment with a [device token](push/quick-start.md#apns).

#### Version 0.4.0 {#v-push-0-4-0}

Released 24 November 2016

- Links from push notifications are now opened.
- Added a dynamic framework.
- The DynamicDependencies framework has been changed to Dynamic.
- The StaticDependencies framework has been changed to Static.

#### Version 0.3.0 {#v-push-0-3-0}

Released 10 October 2016

- Integrated with the AppMetrica Mobile SDK library.

{% endcut %}

