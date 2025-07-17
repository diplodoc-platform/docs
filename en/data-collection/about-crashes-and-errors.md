# Crashes and errors

AppMetrica lets you collect information about app crashes and errors. You can analyze them in the [Crashes/Errors](../mobile-reports/crashes-and-errors.md) reports.

Key AppMetrica crash/error analysis features:

**Automatic uploading of mapping, SO and dSYM files when building an app**

:   Information about crashes and errors on Android can be sent in an obfuscated form and on iOS in an unsymbolicated form. It's difficult to extract data from these logs for analysis. To be able to analyze logs, upload the mapping, SO, or dSYM files to AppMetrica.

    For mapping, OS, and dSYM files, AppMetrica supports automatic upload when building an app and manual upload via the web interface. For more information, see:

    - [Uploading mapping files and debugging symbols on Android](upload-mapping.md).
    - [Uploading dSYM files on iOS](upload-dsym.md).

**Grouping data**

:   Crash logs are grouped into crash groups by [stack trace](https://en.wikipedia.org/wiki/Stack_trace).

    Error grouping depends on the method that is used to send them. For more information, see [{#T}](#send-report-error).

    Groups show all the devices where crashes/errors occur. From each group, you can view the full log from a specific device.

**Opening and closing a crash or error**

:   You can close fixed crashes and errors to filter them out of the report. If, after closing, they're found in versions that didn't have them before, the crash or error is re-opened.

**Integrating a profile card**

:   To view the events that preceded the crash or error, go from the log to a [profile card](../mobile-reports/profile-list.md).

**Group comments**

:   You can add a comment for each group. For example, you can insert into a comment a link to an issue in Yandex.Tracker.

## Sending a custom error message {#send-report-error}

Examples of sending a custom error message on various platforms:

- [Android](../sdk/android/analytics/android-operations.md#send-report-error)
- [iOS](../sdk/ios/analytics/ios-operations.md#send-report-error)
- [Flutter](../sdk/flutter/analytics/flutter-operations.md#send-report-error)
- [React Native](../sdk/react-native/analytics/react-native-operations.md#send-report-error)
- [Unity](../sdk/unity/analytics/unity-operations.md#send-report-error)

## Learn more {#learn-more}

- [Crashes and errors report](../mobile-reports/crashes-and-errors.md)
- [Uploading mapping files and debugging symbols on Android](upload-mapping.md)
- [Uploading dSYM files on iOS](upload-dsym.md)
- [Android documentation](https://developer.android.com/topic/performance/vitals/crash)
- [Apple documentation](https://developer.apple.com/library/archive/technotes/tn2151/_index.html)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
