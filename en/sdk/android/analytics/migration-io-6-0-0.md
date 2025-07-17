# Migrating to version 6.0.0

When you migrate your app from `com.yandex.android:mobmetricalib` to `io.appmetrica.analytics:analytics`, the main IDs and data will be preserved. That means the transition to the new version should not result in issues or anomalies in the reports.

## Running two versions of AppMetrica SDK in parallel

We renamed the group and main artifacts. As a result, you can use two versions of AppMetrica SDK in your app in parallel: `com.yandex.android:mobmetricalib` and `io.appmetrica.analytics:analytics`. This might occur in some cases.

### 1. The app dependencies will include dependencies for both versions of AppMetrica SDK.

{% note alert %}

We strongly advise against running `com.yandex.android:mobmetricalib` and `io.appmetrica.analytics:analytics` with the same `API_KEY` in the app code. In other words, you can't use the same `API_KEY` to enable both `YandexMetrica` and `AppMetrica` at the same time. While that won't cause crashes or failures in the app, it will distort and disrupt the statistics. When migrating to `io.appmetrica.analytics:analytics`, make sure the app doesn't have any dependencies for `com.yandex.android:mobmetricalib`. Also check that the app code doesn't include class imports from the `com.yandex.metrica` package.

{% endnote %}

### 2. One of the app dependencies will transitively pull the AppMetrica SDK dependency.

If the application and libraries use different API_KEYs, this situation is acceptable but not desirable. The statistics should be collected normally, though minor deviations are possible. In that case, the app size might increase slightly since the AppMetrica app will include two SDKs instead of one.

### AppMetrica SDK and AppMetrica Push SDK compatibility

When updating AppMetrica SDK to version 6.0.0, we recommend using **AppMetrica Push SDK 2.3.3**, which supports both `com.yandex.android:mobmetricalib` and `io.appmetrica.analytics:analytics`.

## Migration guide

The guide contains examples demonstrating the differences between SDK versions `5.3.0` and `6.0.0`. This section only covers methods that do not have backward compatibility.

To migrate to the new version, follow these steps:

1. Change the dependency from `com.yandex.android:mobmetricalib:5.3.0` to `io.appmetrica.analytics:analytics:6.0.0`.
2. In the project code, replace the classes and methods that have been simply renamed or only changed their package. The changes you need to make are listed in the [section on class renaming](#rename-classes).
3. Temporarily comment out the code with the other errors to ensure that the project can be built.
4. To ensure you only run the new AppMetrica version, follow the [instructions in the section](#check).
5. If you use the plugin from `com.yandex.android:appmetrica-build-plugin`, update it to the version listed in the [section](#crash-plugin).
6. Change any exclude rules there are. The required changes are indicated in the [dependency renaming section](#dependencies).
7. Edit the code you commented out by following the other paragraphs in this guide. If you have any questions, contact [support](../../../troubleshooting/feedback-new.md).

### Renamed classes {#rename-classes}

* Replaced the `com.yandex.metrica` package with `io.appmetrica.analytics`.
* Replaced the `com.google.protobuf.nano.ym` package in the `analytics-proto` project with `io.appmetrica.analytics.protobuf.nano`.
* Renamed the `YandexMetrica` class as `AppMetrica`.
   * Removed `reportNativeCrash`.
   * Removed `requestAppMetricaDeviceID`. Use `requestStartupParams` instead.
   * Renamed `setStatisticsSending` as `setDataSendingEnabled`.
   * Removed `setLocationTracking(Context, boolean)`. Use `setLocationTracking(boolean)` instead.
* Renamed the `YandexMetricaConfig` class as `AppMetricaConfig`.
   * Renamed `Builder#withStatisticsSending` as `Builder#withDataSendingEnabled`.
* Renamed the `YandexMetricaDefaultValues` class as `AppMetricaDefaultValues`.
* Renamed the `MetricaService` class as `AppMetricaService`.
* Renamed the `IMetricaService` class as `IAppMetricaService`.
* Renamed the `YandexMetricaPlugins` class as `AppMetricaPlugins`.
* `IReporter` interface
   * Renamed `setStatisticsSending` as `setDataSendingEnabled`.
* `ReporterConfig` interface
   * Renamed `Builder#withStatisticsSending` as `Builder#withDataSendingEnabled`.

### Renamed dependencies {#dependencies}

* Renamed the `com.yandex.android:mobmetricalib-ndk-crashes` module as `io.appmetrica.analytics:analytics-ndk-crashes`. Only version 3.0.0 and later is supported.
* Renamed the `module com.yandex.android:mobmetricalib-identifiers` module as `io.appmetrica.analytics:analytics-identifiers`.

## How to make sure you're only running the new version {#check}

Because the library name was changed, there is a chance that both the old and the new AppMetricas will be used in parallel. That could lead to abnormal behavior. To avoid such situations, make sure the old AppMetrica is not used in the app.

To check that the `com.yandex.android:mobmetricalib` dependency is not used, run this command:

```
./gradlew :app:dependencies
```

The command will display the dependencies for all your app build variants. After that, look up where `com.yandex.android:mobmetricalib` is used and replace it with the new dependency.

If you did everything correctly, the following command call will return an empty response:

```
./gradlew app:dependencies | grep com.yandex.android:mobmetricalib
```

## Compatibility with the AppMetrica Gradle Plugin versions {#crash-plugin}

{% note warning %}

The artifact name changed in the plugin.

{% endnote %}

To ensure proper desymbolization of crashes, use a AppMetrica Gradle Plugin version `io.appmetrica.analytics:gradle:0.8.2` or later.

## Dependency exclusion {#exclude}

### Integrating a library for getting advertising IDs

AppMetrica SDK uses `io.appmetrica.analytics:analytics-identifiers`, a separate library, to obtain ad IDs. This library contains a dependency on `com.google.android.gms:play-services-ads-identifier:18.0.1`, which is used to get the GAID. The `io.appmetrica.analytics:analytics-identifiers` library version should correspond to the `io.appmetrica.analytics:analytics` library version.

This dependency is added by default.

If you don't want to obtain advertising IDs (for example, for children's apps), exclude the library in the project's `build.gradle` file:

{% list tabs %}

- build.gradle.kts

   ```kotlin translate=no
   configurations.configureEach {
       exclude(group = "io.appmetrica.analytics", module = "analytics-identifiers")
   }
   ```

- build.gradle

   ```groovy translate=no
   configurations.configureEach {
       exclude group: 'io.appmetrica.analytics', module: 'analytics-identifiers'
   }
   ```

{% endlist %}

### Integrating the location library

AppMetrica SDK uses `io.appmetrica.analytics:analytics-location`, a separate library, to obtain locations. It contains a dependency on `com.google.android.gms:play-services-location:19.0.1` used to get locations. The `io.appmetrica.analytics:analytics-location` library version should correspond to the `io.appmetrica.analytics:analytics` library version.

This dependency is added by default.

If you don't want to get locations, exclude the library in the project's `build.gradle` file:

{% list tabs %}

- build.gradle.kts

   ```kotlin translate=no
   configurations.configureEach {
       exclude(group = "io.appmetrica.analytics", module = "analytics-location")
   }
   ```

- build.gradle

   ```groovy translate=no
   configurations.configureEach {
       exclude group: 'io.appmetrica.analytics', module: 'analytics-location'
   }
   ```

{% endlist %}

## Migrating the requestAppMetricaDeviceID method

Removed the `YandexMetrica.requestAppMetricaDeviceID` method. Use the `AppMetrica.requestStartupParams` method instead.

{% note warning %}

Make sure to request the `StartupParamsCallback.APPMETRICA_DEVICE_ID_HASH` key rather than `StartupParamsCallback.APPMETRICA_DEVICE_ID` since the `StartupParamsCallback.APPMETRICA_DEVICE_ID` key will return a different ID.

{% endnote %}

{% list tabs group=instructions %}

- Kotlin

   ```kotlin translate=no
   val startupParamsCallback = object : StartupParamsCallback {
       override fun onReceive(
           result: StartupParamsCallback.Result?,
       ) {
           val deviceIdHash = result?.deviceIdHash
           // ...
       }

       override fun onRequestError(
           reason: StartupParamsCallback.Reason,
           result: StartupParamsCallback.Result?,
       ) {
           // ...
       }
   }
   AppMetrica.requestStartupParams(
       this,
       startupParamsCallback,
       listOf(StartupParamsCallback.APPMETRICA_DEVICE_ID_HASH)
   )
   ```

- Java

   ```java translate=no
   StartupParamsCallback startupParamsCallback = new StartupParamsCallback() {
       @Override
       public void onReceive(@Nullable Result result) {
           if (result != null) {
               String deviceId = result.deviceId;
               String deviceIdHash = result.deviceIdHash;
               String uuid = result.uuid;
           }
       }

       @Override
       public void onRequestError(@NonNull Reason reason, @Nullable Result result) {
           // ...
       }
   };
   AppMetrica.requestStartupParams(
           this,
           startupParamsCallback,
           Arrays.asList(StartupParamsCallback.APPMETRICA_DEVICE_ID_HASH)
   );
   ```

{% endlist %}

## Removal of the deprecated Revenue#newBuilder(double, Currency) method

- Removed the previously `@deprecated` `Revenue#newBuilder(double, Currency)` method. Use `Revenue#newBuilder(int, Currency)` instead, where `int` implies the use of `revenueMicros`.
- Renamed the `Revenue#newBuilderWithMicros(int, Currency)` method as `Revenue#newBuilder(int, Currency)`.

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
