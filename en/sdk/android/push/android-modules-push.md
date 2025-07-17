# List of optional modules for Push SDK

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

## Included by default {#default}

- `provider-firebase` — allows AppMetrica Push SDK to work with `com.google.firebase:firebase-messaging`.

## Not included by default {#not-default}

- `plugin-adapter` — module for plugin developers.
- `provider-gcm` — allows AppMetrica Push SDK to work with `com.google.android.gms:play-services-gcm`.
- `provider-hms` — allows AppMetrica Push SDK to work with `com.huawei.hms:push`.
- `provider-rustore` — allows AppMetrica Push SDK to work with `ru.rustore.sdk:pushclient`.

The current list of modules can be checked on [github](https://github.com/appmetrica/push-sdk-android/blob/main/README.md).

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
