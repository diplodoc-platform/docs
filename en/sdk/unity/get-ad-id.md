# Getting advertising IDs

An advertising ID (GAID) is a unique Google Play service identifier for displaying ads to users who agree to see personalized ads. The user can disable the personalization of ads or reset the ID in settings. In this case, advertising networks won't be able to use it to select relevant ads. The accuracy of traffic attribution will also decrease significantly.

## Integrating a library for getting advertising IDs {#enable}

Plugin AppMetrica Unity SDK uses `io.appmetrica.analytics:analytics-identifiers`, a separate library, to obtain ad IDs. This library contains a dependency on `com.google.android.gms:play-services-ads-identifier:18.0.1`, which is used to get the GAID. The `io.appmetrica.analytics:analytics-identifiers` library version should correspond to the `io.appmetrica.analytics:analytics` library version.

{% note info "" %}

A dependency on the `io.appmetrica.analytics:analytics-identifiers` library is added by default.

{% endnote %}

### Excluding the library of advertising IDs from the list of dependencies {#disable}

If you don't want to obtain advertising IDs (for example, for children's apps), exclude the library in the project's Custom Launcher Gradle Template (file `Assets/Plugins/Android/launcherTemplate.gradle`). If there is no such file, check the Custom Gradle Template (file `Assets/Plugins/Android/mainTemplate.gradle`)`.

```csharp translate=no
configurations.configureEach {
  exclude(group = "io.appmetrica.analytics", module = "analytics-identifiers")
}
```

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
