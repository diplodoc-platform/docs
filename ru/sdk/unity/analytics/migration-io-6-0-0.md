# Руководство по миграции на версию 6.0.0

## Одновременное использование двух версий AppMetrica SDK {#two-versions}

В одном приложении могут использоваться сразу две версии AppMetrica SDK. Такая ситуация нежелательна. Статистика должна собираться нормально, хотя допустимы небольшие отклонения. В этом случае возможно некоторое увеличение размера приложения, так как в составе приложения будут присутствовать два SDK, вместо одного.

{% note alert %}

Категорически не рекомендуется одновременная работа в коде приложения двух версий SDK с одним `API_KEY`. То есть нельзя одновременно активировать `AppMetrica` и использовать префаб с одним `API_KEY`. Это не приведет к сбоям и крэшам в приложении, но вызовет искажение и нарушение статистики. При миграции на новую версию плагина проверьте, что у вас нет папки `Assets/AppMetrica`, новая версия плагина поставляется через UPM и будет располагаться в `Library/PackageCache/io.appmetrica.analytics@hash`.

{% endnote %}

## Руководство по миграции {#about-migration}

Руководство содержит примеры, демонстрирующие различия между версиями плагина `5.2.0` и `6.0.0`. В разделе рассматриваются только те методы, в которых нарушена обратная совместимость.

Для миграции на новую версию выполните следующие шаги:

1. Удалите старую версию плагина.
2. Добавьте новую версию плагина используя UPM. Подробнее смотрите в [разделе про подключение плагина](#integration).
3. Замените префаб на активацию через [RuntimeInitializeOnLoadMethodAttribute](https://docs.unity3d.com/ScriptReference/RuntimeInitializeOnLoadMethodAttribute.html). Подробнее смотрите в [разделе про замену префаба](#init-change).
4. В коде проекта замените те классы и методы, которые были переименованы или поменяли только пакет. Подробнее смотрите в [разделе про переименования](#rename).

### Подключение AppMetrica Unity Plugin 6.0.0 {#integration}

Для подключения плагина используется [Unity Package Manager](https://docs.unity3d.com/Manual/Packages.html).

{% list tabs %}

- OpenUPM

  Добавьте зависимости в [Packages/manifest.json](https://docs.unity3d.com/Manual/upm-manifestPrj.html):

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

  1. Подключите External Dependency Manager согласно [документации](https://github.com/googlesamples/unity-jar-resolver/tree/master?tab=readme-ov-file#getting-started).

  2. Добавьте AppMetrica Unity Plugin в зависимости в [Packages/manifest.json](https://docs.unity3d.com/Manual/upm-manifestPrj.html):

    ```json translate=no
    {
      "dependencies": {
        "io.appmetrica.analytics": "https://github.com/appmetrica/appmetrica-unity-plugin.git#v{{ appmetrica-unity-plugin }}"
      }
    }
     ```

{% endlist %}

### Замена префаба {#init-change}

1. Создайте static метод с атрибутом `[RuntimeInitializeOnLoadMethod(RuntimeInitializeLoadType.BeforeSceneLoad)]` и произведите активацию AppMetrica с помощью метода `AppMetrica.Activate()`.

  **Пример:**
  
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

2. Удалите `AppMetrica` префаб с ваших сцен.

## Переименование {#rename}

{% note info %}

Для работы с AppMetrica используйте static методы из класса `AppMetrica`. Для этого замените `AppMetrica.Instance` на `AppMetrica` и добавьте импорт `Io.AppMetrica`.

{% endnote %}

* Интерфейс `IYandexAppMetrica` удален, методы перенесены в класс `AppMetrica`.
  * Свойство `LibraryVersion` удалено, используйте метод `GetLibraryVersion()`.
  * Свойство `LibraryApiLevel` удалено.
  * Метод `ActivateWithConfiguration` переименован в `Activate`.
  * Метод `ReportEvent(string, IDictionary<string, object>)` удален, используйте метод `ReportEvent(string, string)`.
  * Метод `ReportError(string, string)` удален.
  * Метод `ReportError(string, string, string)` удален.
  * Метод `ReportError(string, string, YandexAppMetricaErrorDetails)` удален, используйте метод `ReportError(string, string, Exception)`.
  * Метод `ReportError(string, string, YandexAppMetricaErrorDetails)` удалён, используйте метод `ReportError(string, string, Exception)`.
  * Метод `ReportError(Exception, string)` удален, используйте метод `ReportError(string, Exception)`.
  * Метод `ReportError(YandexAppMetricaErrorDetails, string)` удалён, используйте метод `ReportError(string, Exception)`.
  * Метод `ReportUnhandledException(YandexAppMetricaErrorDetails)` удален, используйте метод `ReportUnhandledException(Exception)`.
  * Метод `ReportErrorFromLogCallback` удален.
  * Метод `SetStatisticsSending` переименован в `SetDataSendingEnabled`.
  * Метод `RequestAppMetricaDeviceID` удален, используйте метод `RequestStartupParams`.
  * Метод `ReportReferralUrl` удален.
  * Метод `RequestTrackingAuthorization` удален.
* Класс `YandexAppMetricaConfig` переименован в `AppMetricaConfig` и перенесен в пространство имен `Io.AppMetrica`.
  * Свойство `StatisticsSending` переименовано в `DataSendingEnabled`.
  * Свойство `HandleFirstActivationAsUpdate` переименовано в `FirstActivationAsUpdate`.
  * Свойство `AppForKids` удалено.
* Класс `YandexAppMetricaConfig.Coordinates` переименован в `Location` и перенесен в пространство имен `Io.AppMetrica`.
* Класс `YandexAppMetricaPreloadInfo` переименован в `PreloadInfo` и перенесен в пространство имен `Io.AppMetrica`.
* Перечисление `YandexAppMetricaRequestDeviceIDError` удалено.
* Перечисление `YandexAppMetricaRequestTrackingStatus` удалено.

**AdRevenue**

* Класс `YandexAppMetricaAdRevenue` переименован в `AdRevenue` и перенесен в пространство имен `Io.AppMetrica`.
  * Свойство `AdRevenue` переименовано в `AdRevenueValue`.

**Revenue**

* Класс `YandexAppMetricaRevenue` переименован в `Revenue` и перенесен в пространство имен `Io.AppMetrica`.
  * Конструктор `(double, string)` удален, используйте `(long, string)`.
  * Свойство `Price` удалено, используйте `PriceMicros`.
  * Свойство `Receipt` переименовано в `ReceiptValue`.
* Класс `YandexAppMetricaReceipt` переименован в `Revenue.Receipt` и перенесен в пространство имен `Io.AppMetrica`.

**Атрибуты пользователя**

* Класс `YandexAppMetricaAttribute` переименован в `Attribute` и перенесен в пространство имен `Io.AppMetrica.Profile`.
* Класс `YandexAppMetricaBirthDateAttribute` переименован в `BirthDateAttribute` и перенесен в пространство имен `Io.AppMetrica.Profile`.
* Класс `YandexAppMetricaBooleanAttribute` переименован в `BooleanAttribute` и перенесен в пространство имен `Io.AppMetrica.Profile`.
* Класс `YandexAppMetricaCounterAttribute` переименован в `CounterAttribute` и перенесен в пространство имен `Io.AppMetrica.Profile`.
* Класс `YandexAppMetricaGenderAttribute` переименован в `GenderAttribute` и перенесен в пространство имен `Io.AppMetrica.Profile`.
* Класс `YandexAppMetricaGenderAttribute.Gender` переименован в `GenderAttribute.Gender` и перенесен в пространство имен `Io.AppMetrica.Profile`.
  * Значение `FEMALE` переименовано в `Female`.
  * Значение `MALE` переименовано в `Male`.
  * Значение `OTHER` переименовано в `Other`.
* Класс `YandexAppMetricaNameAttribute` переименован в `NameAttribute` и перенесен в пространство имен `Io.AppMetrica.Profile`.
* Класс `YandexAppMetricaNotificationsEnabledAttribute` переименован в `NotificationsEnabledAttribute` и перенесен в пространство имен `Io.AppMetrica.Profile`.
* Класс `YandexAppMetricaNumberAttribute` переименован в `NumberAttribute` и перенесен в пространство имен `Io.AppMetrica.Profile`.
* Класс `YandexAppMetricaStringAttribute` переименован в `StringAttribute` и перенесен в пространство имен `Io.AppMetrica.Profile`.
* Класс `YandexAppMetricaUserProfile` переименован в `UserProfile` и перенесен в пространство имен `Io.AppMetrica.Profile`.
  * Метод `ApplyFromArray(List<YandexAppMetricaUserProfileUpdate>)` удален.
* Класс `YandexAppMetricaUserProfileUpdate` переименован в `UserProfileUpdate` и перенесен в пространство имен `Io.AppMetrica.Profile`.
