# Compliance with Google Play policies (use and transfer of geodata)

{% note info %}

The official interpretation of notifications and recommendations on complying with policies can only be provided by Google Play. The general recommendations are described below.

{% endnote %}

According to the [updated Google Play policy](https://support.google.com/googleplay/android-developer/answer/11995078), the use and transfer of geodata must be stipulated by the functionality or necessity for the app to function. Therefore, we recommend that you:

- Explicitly explain to the user why the app needs to use and transfer geodata.
- Obtain the user's consent to process and transfer data.

This means that sending a user's geolocation to various services, including AppMetrica, is allowed only after informing them about it and obtaining proper consent. This is why sending geolocation data in the Android AppMetrica SDK 5.0 is [disabled](../sdk/android/changelog-android.md) by default.

## About the notification in Google Play Console {#google-play-console}

{% note info %}

Notifications might be related both to the published app version and its test builds uploaded to Google Play.

{% endnote %}

This notification could probably be received by apps that declare geo permissions (`access_fine_location / access_coarse_location`) and use the SDK below version 5.0. At the same time, the content of the notification in Google Play Console doesn't mean a "violation", but rather indicates a potential risk of non-compliance with policies (for example, if there are geo permissions, geodata sending is enabled in the SDK and there is no "prominent disclosure" for the user about it).

If you don't declare geo permissions, disabled (or didn't enable) sending geodata in the SDK, or previously received the user's consent and properly informed them, no "violation" will occur.

## What to do if you received the notification {#how-to}

1. Make sure that your app generally complies with the updated policies. If the use of geodata isn't stipulated by its functionality, we recommend you abandon it and stop declaring geo permissions, because geodata can't be obtained without them. This will reduce the risk of a "violation". For more information, see the [Google documentation](https://support.google.com/googleplay/android-developer/answer/10144311).
1. Upgrade to the [Android AppMetrica SDK 5.0](../sdk/android/changelog-android.md) in order to eliminate the risks of data transmission before the user's consent is obtained.
1. If geodata is needed for your app to work, you need to display it in "prominent disclosure" for the user and obtain their consent. For more information, see the [Google documentation](https://support.google.com/googleplay/android-developer/answer/11995078). After that, enable sending geodata using one of the following methods: `withLocationTracking(boolean enabled)` or `setLocationTracking(boolean enabled)`.

If updating isn't yet possible, we recommend disabling the transfer of geodata when initializing the library. See [Examples](../data-collection/geo.md#track-location).

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
