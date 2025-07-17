# Uploading mapping files and debugging symbols on Android

AppMetrica lets you collect information about native and Java crashes. You can analyze them in the [Crashes and errors](../mobile-reports/crashes-and-errors.md) report. See also [Configuring data collection](about-crashes-and-errors.md).

To reduce the size of an app, [optimize](https://developer.android.com/studio/build/shrink-code) the code during a release build.

If the code was compressed and obfuscated during the build of an Android application, information about crashes is transmitted in obfuscated form. To extract data for analysis from such crash logs, AppMetrica performs server-side deobfuscation.

To do this, upload the mapping files or debug symbols of SO files to AppMetrica, either automatically when building the app or manually via the web interface.

To send files, enable the [AppMetrica Gradle Plugin](../sdk/android/analytics/android-gradle-plugin.md).

{% note info "" %}

Upload mapping files if you use [ProGuard](https://www.guardsquare.com/en/products/proguard/manual) or [R8](https://r8.googlesource.com/r8/). If you don't compress or obfuscate the code, don't enable the plugin.

{% endnote %}

## Learn more {#learn-more}

- [Crashes and errors report](../mobile-reports/crashes-and-errors.md)
- [Android documentation](https://developer.android.com/topic/performance/vitals/crash)

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
