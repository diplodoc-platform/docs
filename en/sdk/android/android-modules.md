# List of modules

## Optional modules {#optional-modules}

The modules described below are optional and can be forcibly disabled from the AppMetrica SDK if necessary. To do this, add the following code to the `app/build.gradle.kts` or `app/build.gradle` file:

{% list tabs %}

- build.gradle.kts

    ```kotlin translate=no
    configurations.configureEach {
        exclude(group = "io.appmetrica.analytics", module = "analytics-{module_name}")
    }
    ```

- build.gradle

   ```groovy translate=no
   configurations.configureEach {
       exclude group: 'io.appmetrica.analytics', module: 'analytics-{module_name}'
   }
   ```

{% endlist %}

- `ad-revenue` — includes all Ad-Revenue modules of AppMetrica SDK.
- `ad-revenue-admob-v23` — adds a handler for Ad-Revenue events from `com.google.android.gms:play-services-ads`.
- `ad-revenue-applovin-v12` — adds a handler for Ad-Revenue events from `com.applovin:applovin-sdk`.
- `ad-revenue-fyber-v3` — adds a handler for Ad-Revenue events from `com.fyber:fairbid-sdk`.
- `ad-revenue-ironsource-v7` — allows AppMetrica SDK to collect Ad-Revenue events from `com.ironsource.sdk:mediationsdk`.
- `apphud` — adds integration with `com.apphud:ApphudSDK-Android`.
- `appsetid` — allows AppMetrica SDK to collect App Set IDs.
- `identifiers` — allows AppMetrica SDK to collect ADV IDs.
- `location` — allows AppMetrica SDK to collect location.
- `ndkcrashes` — allows AppMetrica SDK to handle native crashes on Android.
- `screenshot` — allows AppMetrica SDK to collect screenshot taken events.

## Modules with optional dependencies {#optional-dependencies}

The modules described below are not optional, but they do require external dependencies to function. You can find the necessary dependencies in the modules' README files.

- `billing-v6` — wrapper for `com.android.billingclient:billing`.
- `gpllibrary` — wrapper for `com.google.android.gms:play-services-location`.

## Module dependencies {#module-dependencies}

You can find list of module dependencies with supported versions in the [dependencies_versions.yaml](https://github.com/appmetrica/appmetrica-sdk-android/blob/main/dependencies_versions.yaml) file on github.

The current list of modules can also be checked on [github](https://github.com/appmetrica/appmetrica-sdk-android/blob/main/README.md).

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
