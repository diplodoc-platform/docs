# Migrating to version 6.0.0

## Running two versions of AppMetrica SDK in parallel {#two-versions}

You can use two versions of AppMetrica SDK in your app in parallel. This is undesirable. The statistics should be collected normally, though minor deviations are possible. In that case, the app size might increase slightly since it will include two SDKs instead of one.

{% note alert %}

We strongly advise against running two SDK versions with the same `API_KEY` in the app code. In other words, you can't activate `AppMetrica` and use the prefab with the same `API_KEY` at the same time. While that won't cause crashes or failures in the app, it will distort and disrupt the statistics. When migrating to the new plugin version, make sure you don't have the `Assets/AppMetrica` directory. The new plugin version is provided via UPM and saved to `Library/PackageCache/io.appmetrica.analytics@hash`.

{% endnote %}

## Migration guide {#about-migration}

This guide contains examples that show the differences between plugin versions `5.2.0` and `6.0.0`. This section only covers methods that do not have backward compatibility.

To migrate to the new version, follow these steps:

1. Remove the previous plugin version.
2. Add the new plugin version using UPM. For more information, see the [section on enabling the plugin](#integration).
3. Replace the prefab with activation via [RuntimeInitializeOnLoadMethodAttribute](https://docs.unity3d.com/ScriptReference/RuntimeInitializeOnLoadMethodAttribute.html). For more information, see the [section on replacing the prefab](#init-change).
4. In the project code, replace the classes and methods that have been renamed or only changed their package. For more information, see the [section on renamings](#rename).

### Enabling AppMetrica Unity Plugin 6.0.0 {#integration}

The plugin is enabled via the [Unity Package Manager](https://docs.unity3d.com/Manual/Packages.html).

{% list tabs %}

- OpenUPM

  Add the following dependencies to [Packages/manifest.json](https://docs.unity3d.com/Manual/upm-manifestPrj.html):

     ```json translate=no
     {
       "scopedRegistries": [
         {
           "name": "package.openupm.com",
           "url": "https://package.openupm.com",
           "scopes": [
             "com.google.external-dependency-manager",
             "io.appmetrica.analytics"
           ]
         }
       ],
       "dependencies": {
         "com.google.external-dependency-manager": "{{ google-external-dependency-manager }}",
         "io.appmetrica.analytics": "{{ appmetrica-unity-plugin }}"
       }
     }
     ```

- UPM (GitHub)

  1. Follow the [documentation](https://github.com/googlesamples/unity-jar-resolver/tree/master?tab=readme-ov-file#getting-started) to enable External Dependency Manager.

  2. Add AppMetrica Unity Plugin to the dependencies in [Packages/manifest.json](https://docs.unity3d.com/Manual/upm-manifestPrj.html):

     ```json translate=no
     {
       "dependencies": {
         "io.appmetrica.analytics": "https://github.com/appmetrica/appmetrica-unity-plugin.git#v{{ appmetrica-unity-plugin }}"
       }
     }
     ```

{% endlist %}

### Replacing the prefab {#init-change}

1. Create a static method with the `[RuntimeInitializeOnLoadMethod(RuntimeInitializeLoadType.BeforeSceneLoad)]` attribute and activate AppMetrica using the `AppMetrica.Activate()` method.

  **Example:**

  ```csharp translate=no
  using Io.AppMetrica;
  using UnityEngine;

  public static class AppMetricaActivator {
      [RuntimeInitializeOnLoadMethod(RuntimeInitializeLoadType.BeforeSceneLoad)]
      private static void Activate() {
          AppMetrica.Activate(new AppMetricaConfig("APIKey") {
              // copy settings from prefab
              CrashReporting = true, // prefab field 'Exceptions Reporting'
              SessionTimeout = 10, // prefab field 'Session Timeout Sec'
              LocationTracking = false, // prefab field 'Location Tracking'
              Logs = false, // prefab field 'Logs'
              FirstActivationAsUpdate = !IsFirstLaunch(), // prefab field 'Handle First Activation As Update'
              DataSendingEnabled = true, // prefab field 'Statistics Sending'
          });
      }

      private static bool IsFirstLaunch() {
          // Implement logic to detect whether the app is opening for the first time.
          // For example, you can check for files (settings, databases, and so on),
          // which the app creates on its first launch.
          return true;
      }
  }
  ```

2. Remove the `AppMetrica` prefab from your stages.

## Renamings {#rename}

{% note info %}

Use static methods from the `AppMetrica` class for working with AppMetrica. To do this, replace `AppMetrica.Instance` with `AppMetrica` and add `Io.AppMetrica` import.

{% endnote %}

* Removed the `IYandexAppMetrica` interface and transferred the methods to the `AppMetrica` class.
  * Removed the `LibraryVersion` property, use the `GetLibraryVersion()` method.
  * Removed the `LibraryApiLevel` property.
  * Renamed the `ActivateWithConfiguration` method as `Activate`.
  * Removed the `ReportEvent(string, IDictionary<string, object>)` method, use the `ReportEvent(string, string)` method instead.
  * Removed the `ReportError(string, string)` method.
  * Removed the `ReportError(string, string, string)` method.
  * Removed the `ReportError(string, string, YandexAppMetricaErrorDetails)` method, use the `ReportError(string, string, Exception)` method instead.
  * Removed the `ReportError(string, string, YandexAppMetricaErrorDetails)` method, use the `ReportError(string, string, Exception)` method instead.
  * Removed the `ReportError(Exception, string)` method, use the `ReportError(string, Exception)` method instead.
  * Removed the `ReportError(YandexAppMetricaErrorDetails, string)` method, use the `ReportError(string, Exception)` method instead.
  * Removed the `ReportUnhandledException(YandexAppMetricaErrorDetails)` method, use the `ReportUnhandledException(Exception)` method instead.
  * Removed the `ReportErrorFromLogCallback` method.
  * Renamed the `SetStatisticsSending` method as `SetDataSendingEnabled`.
  * Removed the `RequestAppMetricaDeviceID` method, use the `RequestStartupParams` method instead.
  * Removed the `ReportReferralUrl` method.
  * Removed the `RequestTrackingAuthorization` method.
* Renamed the `YandexAppMetricaConfig` class as `AppMetricaConfig` and transferred it to the `Io.AppMetrica` namespace.
  * Renamed the `StatisticsSending` property as `DataSendingEnabled`.
  * Renamed the `HandleFirstActivationAsUpdate` property as `FirstActivationAsUpdate`.
  * Removed the `AppForKids` property.
* Renamed the `YandexAppMetricaConfig.Coordinates` class as `Location` and transferred it to the `Io.AppMetrica` namespace.
* Renamed the `YandexAppMetricaPreloadInfo` class as `PreloadInfo` and transferred it to the `Io.AppMetrica` namespace.
* Removed the `YandexAppMetricaRequestDeviceIDError` enumeration.
* Removed the `YandexAppMetricaRequestTrackingStatus` enumeration.

**AdRevenue**

* Renamed the `YandexAppMetricaAdRevenue` class as `AdRevenue` and transferred it to the `Io.AppMetrica` namespace.
  * Renamed the `AdRevenue` property as `AdRevenueValue`.

**Revenue**

* Renamed the `YandexAppMetricaRevenue` class as `Revenue` and transferred it to the `Io.AppMetrica` namespace.
  * Removed the `(double, string)` constructor, use `(long, string)`.
  * Removed the `Price` property, use `PriceMicros`.
  * Renamed the `Receipt` property as `ReceiptValue`.
* Renamed the `YandexAppMetricaReceipt` class as `Revenue.Receipt` and transferred it to the `Io.AppMetrica` namespace.

**User attributes**

* Renamed the `YandexAppMetricaAttribute` class as `Attribute` and transferred it to the `Io.AppMetrica.Profile` namespace.
* Renamed the `YandexAppMetricaBirthDateAttribute` class as `BirthDateAttribute` and transferred it to the `Io.AppMetrica.Profile` namespace.
* Renamed the `YandexAppMetricaBooleanAttribute` class as `BooleanAttribute` and transferred it to the `Io.AppMetrica.Profile` namespace.
* Renamed the `YandexAppMetricaCounterAttribute` class as `CounterAttribute` and transferred it to the `Io.AppMetrica.Profile` namespace.
* Renamed the `YandexAppMetricaGenderAttribute` class as `GenderAttribute` and transferred it to the `Io.AppMetrica.Profile` namespace.
* Renamed the `YandexAppMetricaGenderAttribute.Gender` class as `GenderAttribute.Gender` and transferred it to the `Io.AppMetrica.Profile` namespace.
  * Changed the name of the `FEMALE` value to `Female`.
  * Changed the name of the `MALE` value to `Male`.
  * Changed the name of the `OTHER` value to `Other`.
* Renamed the `YandexAppMetricaNameAttribute` class as `NameAttribute` and transferred it to the `Io.AppMetrica.Profile` namespace.
* Renamed the `YandexAppMetricaNotificationsEnabledAttribute` class as `NotificationsEnabledAttribute` and transferred it to the `Io.AppMetrica.Profile` namespace.
* Renamed the `YandexAppMetricaNumberAttribute` class as `NumberAttribute` and transferred it to the `Io.AppMetrica.Profile` namespace.
* Renamed the `YandexAppMetricaStringAttribute` class as `StringAttribute` and transferred it to the `Io.AppMetrica.Profile` namespace.
* Renamed the `YandexAppMetricaUserProfile` class as `UserProfile` and transferred it to the `Io.AppMetrica.Profile` namespace.
  * Removed the `ApplyFromArray(List<YandexAppMetricaUserProfileUpdate>)` method.
* Renamed the `YandexAppMetricaUserProfileUpdate` class as `UserProfileUpdate` and transferred it to the `Io.AppMetrica.Profile` namespace.
