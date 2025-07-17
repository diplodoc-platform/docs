# Determining the location

AppMetrica can determine the location of a device. Location accuracy depends on the configuration that the library uses for initialization:

**With the locationTracking option enabled**

:   {% note info "" %}

    For iOS, the option is enabled by default.

    {% endnote %}

    Location is determined down to the city level. You can retrieve the information in [reports](../mobile-reports/index.md) and via the [Logs API](../mobile-api/logs/about.md).

    The app requests GPS access. Battery consumption may increase.

**With the locationTracking option disabled**

:   {% note info "" %}

    Starting with the Android AppMetrica SDK 5.0.0, the `locationTracking` option is disabled by default.

    If the version is lower than 5.0.0, the `locationTracking` option is enabled by default.

    {% endnote %}

    The location is determined by the IP address with accuracy to the country. You can retrieve the information in [reports](../mobile-reports/index.md) but not the [Logs API](../mobile-api/logs/about.md).

    The app requests GPS access. Battery consumption does not increase.

    {% note info "" %}

    If you have IP address masking enabled, AppMetrica determines the location with country-level accuracy using the unmasked part of the IP address.

    {% endnote %}

## Determining the location {#track-location}

Examples of location tracking on different platforms:

- [Android](../sdk/android/analytics/android-operations.md#track-location)
- [iOS](../sdk/ios/analytics/ios-operations.md#track-location)
- [Flutter](../sdk/flutter/analytics/flutter-operations.md#track-location)
- [React Native](../sdk/react-native/analytics/react-native-operations.md#track-location)
- [Unity](../sdk/unity/analytics/unity-operations.md#track-location)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
