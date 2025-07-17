# Deeplink tracking

Deeplinks are links that show the user the desired content in an already installed app. Deeplinks can work when the app is launched and in an already open app.

{% note info "" %}

To work with deeplinks, support them in your application on [Android](https://developer.android.com/training/app-links/deep-linking#adding-filters) or [iOS](https://developer.apple.com/documentation/xcode/allowing-apps-and-websites-to-link-to-your-content).

{% endnote %}

Starting with version 4.0 of the iOS/Android SDK, deeplink tracking works automatically when the app is opened. To enable or disable automatic tracking, use the `withAppOpenTrackingEnabled` SDK method for Android and the `appOpenTrackingEnabled` property for iOS.

Even if both automatic and manual deeplink tracking are used when a user opens an app, the information in reports isn't duplicated.

## Deeplink inside the app {#inside}

Deeplinks can be used not only to launch the app, but also to navigate when the app is already open.

The AppMetrica SDK doesn't automatically track deeplinks that are processed in a running application. To track such deeplinks, you'll need additional configuration. [View examples](#tracking).

## Tracking app opens using deeplinks {#tracking}

Examples of tracking app launches from deeplinks on different platforms:

- [Android](../sdk/android/analytics/android-operations.md#deeplink)
- [iOS](../sdk/ios/analytics/ios-operations.md#deeplink)
- [Flutter](../sdk/flutter/analytics/flutter-operations.md#deeplink)
- [React Native](../sdk/react-native/analytics/react-native-operations.md#deeplink)
- [Unity](../sdk/unity/analytics/unity-operations.md#deeplink)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
