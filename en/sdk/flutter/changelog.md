# Changelog

## AppMetrica SDK {#sdk}

### Version 3.2.0 {#v-3-2-0}

Released May 14, 2025

- Updated the Android AppMetrica SDK native version to 7.8.0, iOS to 5.10.

- Improve statistics when using with Yandex.Ads SDK. Add meta-data with plugin description to AndroidManifest.

- Support Swift Package Manager feature.

- Add `appOpen` ad type for `adRevenue` events.

- Add `AppMetrica.setAdvIdentifiersTracking` method to enable/disable including advertising identifiers withing its reports.

### Version 3.1.0 {#v-3-1-0}

Released September 20, 2024

- Updated the Android AppMetrica SDK native version to 7.2.0, iOS to 5.8.

### Version 3.0.0 {#v-3-0-0}

Released August 29, 2024

- Added the prefix `AppMetrica` to all plugin classes to avoid conflicts with foreign code (For more details, see the [migration guide](analytics/migration-io-3-0-0.md)).
- Added the `AppMetricaConfig.flutterCrashReporting` parameter to disable the collection of flutter crashes.
- Updated the `decimal` dependency version to `3.0.0` and accordingly increased the minimum flutter version.

### Version 2.1.1 {#v-2-1-1}

Released May 22, 2024

- Fixed incorrect `null` processing in the `AppMetrica.reportEventWithMap` method.

### Version 2.1.0 {#v-2-1-0}

Released May 7, 2024

- Added methods for sending the external attribution.
- Added keys to be used in the `requestStartupParams` method.

### Version 2.0.0 {#v-2-0-0}

Released March 26, 2024

- The AppMetrica SDK has been updated for Android to version 6.3.0 and for iOS to version 5.0.

### Version 1.3.0 {#v-1-3-0}

Released June 14, 2023

- The native android part of the plugin was rewritten on java due to the problems with kotlin versions.

### Version 1.2.0 {#v-1-2-0}

Released June 5, 2023

- Added auto support for deeplinks.
- Updated dev_dependencies.
- Fixes and improvements.

### Version 1.1.0 {#v-1-1-0}

Released October 10, 2022

- Added support for the AdRevenue API.
- Updated the Android AppMetrica SDK native version to 5.2.0, iOS to 4.4.

### Version 1.0.1 {#v-1-0-1}

Released July 20, 2022

- Fixed the NPE raised when creating `UserProfileAttribute` with `null` arguments.

### Version 1.0.0 {#v-1-0-0}

Released July 14, 2022

- Updated the Android AppMetrica SDK native version to 5.0.0.

### Version 0.1.0 {#v-0-1-0}

Released February 22, 2022

- Initial release. Supports most of the features available in AppMetrica. Native SDK versions:
   - Android: 4.2.0.
   - iOS: 4.2.

## Push SDK {#push}

### Version 2.0.0 {#v-push-2-0-0}

- Updated the AppMetrica Flutter SDK version to [3.0.0](#v-3-0-0).

### Version 1.0.0 {#v-push-1-0-0}

Released May 6, 2024

- Updated versions of the AppMetrica Push SDK ([iOS 2.0.0](../ios/changelog-ios.md#v-push-2-0-0), [Android 3.2.0](../android/changelog-android.md#v-3-2-0)).

### Version 0.3.0 {#v-push-0-3-0}

Released June 16, 2023

- The native android part of the plugin was rewritten on java due to the problems with kotlin versions.
- Updated dev_dependencies.

### Version 0.2.0 {#v-push-0-2-0}

Released August 29, 2022

- Updated versions of the AppMetrica Push SDK ([iOS 1.3.0](../ios/changelog-ios.md), [Android 2.2.0](../android/changelog-android.md)).
- Updated the appmetrica_plugin version to [1.0.1](../flutter/changelog.md).

### Version 0.1.0 {#v-push-0-1-0}

Released March 15, 2022

Initial release. Supports most of the features available in the AppMetrica Push SDK. Native SDK versions:
- Android: 2.1.1.
- iOS: 1.1.


