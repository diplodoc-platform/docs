# Changelog

## AppMetrica SDK

### Version 7.9.0 {#s-7-9-0}

Release May 8, 2025

- The main components of the AppMetrica SDK have been moved to the main application process. The AppMetrica SDK is now fully operational in the main application process. Avoiding a separate process completely removes possible integration problems with other libraries like Firebase Perfomance. 
- Added support for future auto-collection of ad revenue data from plugins.
- Fixed a possible ANR's:
   - `at com.android.billingclient.api.BillingClientImpl.zzaJ(BillingClientImpl.java:1)` ([issue#19](https://github.com/appmetrica/appmetrica-sdk-android/issues/19)).
   - `at io.appmetrica.analytics.impl.Uf.onInstallReferrerSetupFinished(Uf.java:3)` ([issue#20](https://github.com/appmetrica/appmetrica-sdk-android/issues/20)).

### Version 7.8.0 {#s-7-8-0}

Release April 9, 2025

- Added optional module `io.appmetrica.analytics:analytics-screenshot`. It detects the fact that the user has taken a screenshot. When detected, the client event `appmetrica_system_event_screenshot` is sent. For correct working required permission [android.permission.DETECT_SCREEN_CAPTURE](https://developer.android.com/reference/android/Manifest.permission#DETECT_SCREEN_CAPTURE) to AndroidManifest.xml.
- Fixed an issue that could result in duplicate auto-collected inapp purchase data.
- Fixed an issue that could result in very old inapp purchases being automatically collected with current date, potentially distorting reports.
- **Dependencies updates:**
   - Google Play Services Location to `com.google.android.gms:play-services-location:21.0.1`;
   - Google Play Billing to `com.android.billingclient:billing:7.1.1`;
   - Google Play Ads to `com.google.android.gms:play-services-ads:24.1.0`;
   - AppLovin SDK to `com.applovin:applovin-sdk:13.1.0`;
   - FairBid SDK to `com.fyber:fairbid-sdk:3.59.0`;
   - AppHud SDK to `com.apphud:ApphudSDK-Android:2.9.1`;
   - Google Play Services AppSet ID to `com.google.android.gms:play-services-appset:16.1.0`;
   - Google Play Services Ads Identifiers to `com.google.android.gms:play-services-ads-identifier:18.2.0`.
- Added ability to manage access to advertising identifiers to `AppMetricaLibraryAdapter`.

### Version 7.7.0 {#s-7-7-0}

Release Fabruary 14, 2025

- Updated the Apphud SDK to version 2.8.4 in the ad revenue module.
- Information about the original ad type added to the ad revenue events.
- Added the `APP_OPEN` type for ad revenue events from AdMob SDK.
- Fixed a possible ANR's:
   - `at io.appmetrica.analytics.impl.nm.onDestroy(nm.java:1)` ([issue#16](https://github.com/appmetrica/appmetrica-sdk-android/issues/16)).
   - `at io.appmetrica.analytics.networktasks.internal.NetworkCore.stopTasks(NetworkCore.java:1)` ([issue#17](https://github.com/appmetrica/appmetrica-sdk-android/issues/17)).

### Version 7.6.0 {#s-7-6-0}

Released January 23, 2025

- Fixed a possible issue with statistics (installations and new users) when using the AppMetrica Plugins (Unity, Flutter, ReactNative) and Yandex Ads Plugins at the same time.
- Fixed a possible ANR when accessing the AppMetrica API before activation.

### Version 7.5.0 {#s-7-5-0}

Released December 5, 2024

* Added API for managing access to advertising identifiers (GAID, Huawei OAID). See the [documentation](analytics/android-operations.md#track-adv-identifiers).

### Version 7.4.0 {#s-7-4-0}

Released November 29, 2024

* The referrer processing mechanism has been improved, which has allowed us to fix the error of receiving a deferred deeplink and its parameters when installing an application via a tracking link on the latest versions of the browser with the chromium engine (Google Chrome, Yandex Browser, etc.).

### Version 7.3.0 {#s-7-3-0}

Released November 5, 2024

* Added the `AppMetrica#reportAnr()` and `IReporter#reportAnr()` methods that allow you to send ANR data manually.
* Fixed a possible `java.lang.IllegalArgumentException:... at io.appmetrica.analytics.impl.K7.a(K7.java:27)` crash.
* Fixed the `Missing class com.google.android.gms.ads.AdValue` warning that appeared during the app build ([issue#10](https://github.com/appmetrica/appmetrica-sdk-android/issues/10)).

### Version 7.2.2 {#s-7-2-2}

Released October 23, 2024

* Added an extra check to verify that the AppMetrica SDK initialization is complete.

### Version 7.2.1 {#s-7-2-1}

Released October 3, 2024

* Improved the detection of non-first app launches when activating the AppMetrica SDK via a third-party library adapter.
* If you send events using a third-party library adapter before its activation or with invalid parameters, these events are now ignored instead of throwing an exception.

### Version 7.2.0 {#s-7-2-0}

Released September 11, 2024

* Removed the local mechanism for detecting internal crashes of AppMetrica SDK and AppMetrica Push SDK in favor of a backend solution.
* Added the `io.appmetrica.analytics:analytics-apphud` module for Apphud integration.
* Added an API to streamline sending impression-level revenue data (ILRD) from [Google AdMob](../../sdk/android/analytics/android-operations.md#google-admob) for the "App open ad" advertising format.
* Improved event logging.

### Version 7.1.0 {#s-7-1-0}

Released August 21, 2024

- Added an API to facilitate sending of ILRD (impression-level revenue data) from:
  - [Digital Turbine](../../sdk/android/analytics/android-operations.md#digital-turbine)
  - [Google AdMob](../../sdk/android/analytics/android-operations.md#google-admob)
  - [Applovin MAX](../../sdk/android/analytics/android-operations.md#applovin)
- Added support for accelerated sending of some events (attributions from external SDKs, `e-commerce`, `revenue`, and `ad revenue` (impression-level revenue data)) to the server.

### Version 7.0.0 {#s-7-0-0}

Released June 28, 2024

**Breaking changes:**

* The current `minSdkVersion` has been upgraded to `21` (Android 5.0).
* The `sourceCompatibility` and `targetCompatibility` versions have been upgraded to Java 1.8.

**Additional changes:**

* Added invalid format correction for crash and error reports. This change resolves a potential crash

   ```java translate=no
   java.lang.IllegalArgumentException: Unpaired surrogate at index 14 at io.appmetrica.analytics.protobuf.nano.CodedOutputByteBufferNano.encodedLengthGeneral(Unknown Source)
   ```

* Fixed a possible ANR `at io.appmetrica.analytics.impl.sk.a(sk.java:1)`.
* Fixed a possible crash

   ```java translate=no
   java.lang.NullPointerException: Attempt to invoke virtual method 'void io.appmetrica.analytics.impl.Nb.a(io.appmetrica.analytics.impl.ie)' on a null object reference at io.appmetrica.analytics.impl.Qb.b(SourceFile:10)
   ```

* Introduced a limit of 100 events per server request. The limit is imposed to improve the SDK performance when the network channel is unstable.
* Optimized threading on the client side and removed deprecated SDK integration checks. This optimization will reduce the time of synchronous SDK activation.

### Version 6.5.0 {#s-6-5-0}

Released April 26, 2024

* Added sending of attributions from Singular (the required API is available in [Singular SDK 12.5.1 and higher](https://support.singular.net/hc/en-us/articles/360041068651-Android-SDK-Change-Log)). To learn more, see [Importing attributions from other SDKs](../../data-collection/attribution-integration.yaml).
* Removed name obfuscation for method arguments in the API.

### Version 6.4.0 {#s-6-4-0}

Released April 11, 2024

* You can now receive `impression-level revenue data` automatically from the following sources: [Ironsource V7](https://developers.is.com/) and [Fyber V3](https://developer.digitalturbine.com/hc/en-us).
* Fixed the error that was logged to the system log:
   ```
   E ActivityThread: Failed to find provider info for com.yandex.preinstallsatellite.appmetrica.provider
   ```

### Version 6.3.0 {#s-6-3-0}

Released March 18, 2024

* `UUID` format validation and recovery of invalid `UUID` values are now available.
* ANR detection algorithm improved. Now, ANR is only registered if a single `Runnable` couldn't be executed within the allotted time on the main thread. The algorithm identifies heavy tasks that cause the main thread to freeze. Previously, ANR detection triggered when a large number of small `Runnables` were executed on the main thread. In such situations, the ANR stack trace was typically non-informative and quite useless.
* Now, if a single `Runnable` freezes, a single ANR report is generated. This reduces the number of ANR reports, but increases their usefulness.
* Fixed a possible ANR `at io.appmetrica.analytics.internal.AppMetricaService.onCreate` ([issue#3](https://github.com/appmetrica/appmetrica-sdk-android/issues/3)).
* Fixed potential crashing of `org.json.JSONException: Forbidden numeric value: NaN` when sending external attributions (`AppMetrica#reportExternalAttribution(...)`).

### Version 6.2.1 {#s-6-2-1}

Released January 26, 2024

* Fixed an error in external attribution serialization.

### Version 6.2.0 {#s-6-2-0}

Released January 22, 2024

* Added the `AppMetrica.reportExternalAttribution` method for sending attributions from external libraries. To learn more, see [Importing attributions from other SDKs](../../data-collection/attribution-integration.yaml).
* Fixed an issue that prevented logging of saving and sending events to the server.

### Version 6.1.0 {#s-6-1-0}

Released November 28, 2023

* Increased `buildToolsVersion` to `34.0.0`.
* Increased `targetSdkVersion` and `compileSdkVersion` to `34`.
* Kotlin plugin updated to version `org.jetbrains.kotlin:kotlin-gradle-plugin:1.6.21`.
* Now supports automatically collecting purchases and subscriptions made using the `com.android.billingclient:billing:6.0.0` library. Automated collection of purchases and subscriptions using the `com.android.billingclient:billing:4.+` library is no longer supported. Automated collection of purchases and subscriptions is now available for `com.android.billingclient:billing:5.0.0` and higher.
* Fixed a possible deadlock `at io.appmetrica.analytics.networktasks.internal.NetworkCore.onDestroy`.

### Version 6.0.0 {#s-6-0-0}

Released September 13, 2023

* Updated the library ID, root package, and API. For more details, see the [migration instructions](analytics/migration-io-6-0-0.md).
* Removed Breakpad integration. Only Crashpad is currently used. To catch native crashes, use the `io.appmetrica.analytics:analytics-ndk-crashes:3.0.0` dependency. For more details, see the section about [native crashes](analytics/android-operations.md#native-crashes).
* Updated Crashpad to the `9158eb7caa811b684c6bec7f9e9b5f52389d0ce0` commit in the `io.appmetrica.analytics:analytics-ndk-crashes` module.
* Moved the `com.google.android.gms.permission.AD_ID` permission to the `io.appmetrica.analytics:analytics-identifiers` module.
* Fixed the `Class io.appmetrica.analytics.impl.ob.Zh failed lock verification and will run slower` warning (and similar ones) that could have arisen when installing and starting the app.
* Fixed a possible ANR error at `io.appmetrica.analytics.impl.ob.p3$b.onServiceConnected(SourceFile:2)`.
* Moved geo features to a separate dependency: `io.appmetrica.analytics:analytics-location`. You can now opt out of the AppMetrica SDK collecting location coordinates at the app build stage when needed. This may be needed for certain app categories to comply with Google Play policies. For more information, see the [documentation](geo-exclude.md).
* Now supports API for obtaining the AppMetrica SDK IDs (`DeviceId`, `DeviceIdHash`, `UUID`) with the `AppMetrica#requestStartupParams` method. For more information, see the [documentation](analytics/android-operations.md#get-ids).
* Now supports the API for specifying the device type (phone, tablet, TV, car). For more information, see the [documentation](analytics/android-operations.md#device-type).

### Version 5.3.0 {#s-5-3-0}

Released March 3, 2023.

* Fixed the `Class com.yandex.metrica.impl.ob.Zh failed lock verification and will run slower` warning (and similar ones) that could have arisen at app installation and launch.
* Fixed a possible ANR `at com.yandex.metrica.impl.ob.p3$b.onServiceConnected(SourceFile:2)`.
* Fixed errors and improved stability.

### Version 5.2.0 {#s-5-2-0}

Released September 19, 2022

* Added the AdRevenue API for transmitting advertising monetization revenue at the impression level (Impression-Level Revenue Data):
   * `AdRevenue` and `AdRevenue.Builder` classes.
   * `reportAdRevenue(AdRevenue adRevenue)` methods in the `YandexMetrica` class and `reportAdRevenue(AdRevenue adRevenue)` methods in the `IReporter` interface.
   * The `AdType` enumeration.
* targetSdkVersion = 33.

### Version 5.0.1 {#s-5-0-1}

Released July 29, 2022

* Fixed an issue that could cause repeated false installations.

### Versions 5.0.0–4.0.0

{% cut "5.0.0–4.0.0" %}

#### Version 5.0.0 {#s-5-0-0}

Released May 20, 2022

{% note info %}

Starting from Android AppMetrica SDK 5.0.0 and later, appmetrica_device_id changes when the app is reinstalled. This is due to new Google policies. For more information, see the [documentation](../../troubleshooting/troubleshooting.md#change-device-id).

{% endnote %}

* Moved the feature of getting advertising IDs to a separate library named `com.yandex.android:mobmetricalib-identifiers`. For more information, see [Getting advertising IDs](get-ad-id.md).
* The flag to send information about the device location is disabled by default. To enable sending location data along with events, use one of the following methods: `withLocationTracking(boolean enabled)` or `setLocationTracking(boolean enabled)`.
* Added @NonNull annotations for the arguments of the `DeferredDeeplinkParametersListener` interface methods.
* The `reportNativeCrash` method is deprecated and will be removed in future versions.

#### Version 4.2.0 {#s-4-2-0}

Released February 17, 2022

* Added a new API to track crashes and errors from random plugins.

   Interfaces:
   * YandexMetricaPlugins;
   * IPluginReporter.

   Classes:
   * PluginErrorDetails;
   * PluginErrorDetails.Builder;
   * StackTraceItem;
   * StackTraceItem.Builder.

* Now supports downgrade to version 4.2.0 and higher with saving important data, such as the device ID. It is not recommended to use downgrade, as it can cause data loss and corruption. Repeated attribution for such users will not be supported.
* Now supports Google Play Billing Library version 4.0.0. Support is still provided for versions 3.x.
* In the `DeferredDeeplinkParametersListener` method, the `referrer` argument became `@NonNull`. If it is missing, you will get an empty string.
* Removed ROOT status detection on devices running Android 12 and higher. Now all devices running Android 12 will be considered devices without ROOT access.

* Fixed errors and improved stability:

   * Fixed a crash that could have occurred when trying to connect to MetricaService:
      ```
      Process: com.yandex :Metrica java.lang.RuntimeException: Unable to bind to service com.yandex.metrica.MetricaService Caused by: java.lang.IllegalArgumentException at android.os.Parcel.nativeAppendFrom(Native Method).
      ```
   * Fixed a possible ANR in the process:
      ```
      Metrica: at com.yandex.metrica.impl.ob.jg.a (jg.java) at com.yandex.metrica.MetricaService.onConfigurationChanged(MetricaService.java:2)
      ```
   * Fixed a possible crash:
      ```
      java.lang.NullPointerException: Attempt to read from null array at com.yandex.metrica.impl.ob.tz.a
      ```

#### Version 4.1.1 {#s-4-1-1}

Released December 17, 2021

* Added [com.google.android.gms.permission.AD_ID](https://support.google.com/googleplay/android-developer/answer/6048248#zippy%3D%252Cpersistent-identifiers-including-android-id%252Ctargeting-devices-without-an-advertising-id%252Cadvertising-id-violations%252Chow-to-opt-out-of-personalized-ads) permission. For more information, see the [documentation](get-ad-id.md).
* In `DeferredDeeplinkListener.Error` and `DeferredDeeplinkParametersListener.Error`, added `NO_REFERRER` value.
Added preliminary support for [App Set ID](https://developer.android.com/training/articles/app-set-id) to receive a referrer from Google Play (dependency `com.google.android.gms:play-services-appset:16.0.0`).
* SDK optimization is supported due to the correction of possible [VerifyError](https://source.chromium.org/chromium/chromium/src/+/master:build/android/docs/class_verification_failures.md;bpv=1;bpt=0) when initializing classes.
* Mac address collection is disabled.

#### Version 4.0.0 {#s-4-0-0}

Released September 20, 2021

* Google Play Install Referrer via BroadcastReceiver is no longer supported :
   * Removed `MetricaEventHandler` from AndroidManifest
   * Removed the `YandexMetrica#registerReferrerBroadcastReceivers` method.
   * Removed the `YandexMetricaConfig#installedAppCollecting` flag.
   * Removed the `YandexMetricaConfig.Builder#withInstalledAppCollecting` methods.

* Added the `YandexMetricaConfig.Builder#withSessionsAutoTrackingEnabled(boolean enabled)` method for automatic session tracking.
* Added the `revenueAutoTrackingEnabled` method for the automatic collection of data on In-App purchases.
* Now supports the publication of the ".module" file for the [Google Play SDK Console](https://support.google.com/googlepl..-developer/answer/10358880?hl=ru).
* Auto-tracking of deeplinks has been implemented and enabled by default.
* AppMetrica SDK [migrated to AndroidX](https://developer.android.com/jetpack/androidx/migrate).
* Added basic support for Android 12: the main functionality of the AppMetrica SDK is available on Android 12 devices in apps with targetSdkVersion = 31.
* minSdkVersion has been upgraded to 14.

{% endcut %}

## AppMetrica Gradle Plugin

### Version 1.0.1 {#c-1-0-1}

Released December 4, 2024

* Fixed the value of the `version_name` field in `info.txt` file.

### Version 1.0.0 {#c-1-0-0}

Released November 27, 2024

* Plugin connection is supported using `pluginManagement`. The plugin has been renamed to `io.appmetrica.analytics`.
* All actions in the plugin are performed in separate gradle tasks.
* The list of gradle and AGP versions that the plugin works with has been changed.
* Plugin works correctly if configuration cache is enabled.
* Fixed a bug that caused the necessary resources to be deleted under certain `R8` settings.

### Version 0.11.0 {#c-0-11-0}

Released May 2, 2024

* Fixed the error `Cannot write a file to a location pointing at a directory`.
* Stopped using the `deprecated` `VersionNumber` class.

### Version 0.10.0 {#c-0-10-0}

Released April 26, 2024

* Added a `keep` for the resources added by the plugin for AGP `8.2.+`.

### Version 0.9.0 {#c-0-9-0}

Released February 26, 2024

* Now supports AGP up to version `8.2.+` (excluding `8.0.+`) and gradle up to `8.6`.

### Version 0.8.2 {#c-0-8-2}

Released October 31, 2023

* Fixed a `StackOverflowError` that occurred when there was a circular dependency.

### Version 0.8.1 {#c-0-8-1}

Released October 4, 2023

* Fixed a possible crash when checking the use of two AppMetrica versions if there are multiple modules in a project.

### Version 0.8.0 {#c-0-8-0}

Released September 14, 2023

* Changed the plugin name to `io.appmetrica.analytics:gradle:0.8.0`.
* The `com.yandex.android:mobmetricalib-ndk-crashes:1.1.0` dependency updated to `io.appmetrica.analytics:analytics-ndk-crashes:3.0.0`.
* Now supports `io.appmetrica.analytics:analytics:6.0.0`.
* Added the `allowTwoAppMetricas` parameter to disable checking the use of different AppMetrica versions.

### Version 0.7.0 {#c-0-7-0}

Released April 19, 2023.

* Added more details to the error reporting that mapping files are missing.
* Now supports AGP up to version `7.4.+` and gradle up to `7.5`.

### Version 0.6.2 {#c-0-6-2}

Released July 28, 2022

* Improved performance of the plugin.

### Version 0.6.1 {#c-0-6-1}

Released May 20, 2022

* Improved performance of the plugin.

### Version 0.6.0 {#c-0-6-0}

Released May 17, 2022

* Added the mappingFile parameter.
* Fixed the "Cannot query the value of this property because it has no value available" error that occurred when retrieving the mapping file.

## AppMetrica Push SDK

### Version 4.1.1 {#v-4-1-1}

Released January 25, 2025

- Fixed the behavior of the `PushServiceController.shouldSendToken` method. The token is no longer sent if `shouldSendToken == false` or `token == null`.
- The dependency `androidx.legacy:legacy-support-v4` has been replaced with `androidx.core:core`.

### Version 4.0.0 {#v-4-0-0}

Released July 11, 2024

- The current `minSdkVersion` has been upgraded to `21` (Android 5.0).
- Changed the `AppMetricaPushTracker` constructor from `AppMetricaPushTracker()` to `AppMetricaPushTracker(Context)`.
- Updated the `PushServiceController` interface:
  - Renamed the `getTitle` method to `getTransportId`.
  - Added the `getExecutionRestrictions` and `shouldSendToken` methods.
- Improved the processing speed and delivery of push notifications.

### Version 3.3.0 {#v-3-3-0}

Released May 3, 2024

- Fixed push notification processing in `plugin-adapter`.

### Version 3.2.0 {#v-3-2-0}

Released April 22, 2024

- Updated the supported RuStore version to `ru.rustore.sdk:pushclient:2.1.1`.
- Added the `plugin-adapter` module to ensure proper Push SDK performance when used in plugins.
- Added support for saving variable names in the public API.

### Version 3.1.1 {#v-3-1-1}

Released April 9, 2024

- Removed debug logs.

### Version 3.1.0 {#v-3-1-0}

Released April 2, 2024

- Fixed the delivery of silent push notifications when notifications are disabled.

### Versions 3.0.0–2.0.0

{% cut "3.0.0–2.0.0" %}

#### Version 3.0.0 {#v-3-0-0}

Released November 18, 2023

- Updated the library ID, root package, and API. For more details, see the [migration instructions](push/migration-io-3-0-0.md).
- Added an API for customizing the notifications created by the SDK.
- Removed `com.yandex.android:mobmetricalib` support.

#### Version 2.3.3 {#v-2-3-3}

Released November 10, 2023

- Fixed a crash that occurred if the app had two different versions of AppMetrica SDK at the same time.

#### Version 2.3.2 {#v-2-3-2}

Released October 4, 2023

- Fixed a bug

   ```
   No field Companion of type Lio/appmetrica/analytics/ModuleEvent$Companion
   ```

#### Version 2.3.1 {#v-2-3-1}

Released July 31, 2023

- Improved performance and stability of the library.

#### Version 2.2.0 {#v-2-2-0}

Released June 2, 2022

- `minSdkVersion` (in `appmetricapush-provider-hms`) increased to 17.
- `Hms` updated to version 6.5.0.300.
- Accelerated PushSDK activation.

#### Version 2.1.1 {#v-2-1-1}

Released March 14, 2022

- Fixed a bug `BadParcelableException: Parcelable protocol requires a Parcelable.Creator object called CREATOR`.

#### Version 2.1.0 {#v-2-1-0}

Released February 24, 2022

- Improved token acquisition.
- The YandexMetricaPush.getTokens method returns new tokens when called from TokenUpdateListener.onTokenUpdated.
- Improved performance and stability of the library.

#### Version 2.0.0 {#v-2-0-0}

Released October 28, 2021

- Fixed a bug that occasionally occurred when processing a click on a push in Android 12.
- Switching from support dependencies to AndroidX.

{% endcut %}

