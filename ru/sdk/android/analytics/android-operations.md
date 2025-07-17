# Примеры использования методов

## Инициализация библиотеки с расширенной конфигурацией {#initialize}

С помощью расширенной конфигурации можно включить/отключить [логирование](android-logs.md), установить тайм-аут сессии, передать параметры для [отслеживания предустановленных приложений](../../../mobile-tracking/preinstalled-app-attr.md) и т. д.

Настройки расширенной конфигурации применяются с момента инициализации библиотеки.

Чтобы инициализировать библиотеку с расширенной стартовой конфигурацией, создайте объект класса `AppMetricaConfig` с необходимыми настройками и активируйте библиотеку с помощью метода `AppMetrica.activate(Context context, AppMetricaConfig config)`. 

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  class YourApplication : Application() {
      override fun onCreate() {
          super.onCreate()
          // Creating an extended library configuration.
          val config = AppMetricaConfig.newConfigBuilder(API_KEY)
              // Setting up the configuration. For example, to enable logging.
              .withLogs()
              // ...
              .build()
          // Initializing the AppMetrica SDK.
          AppMetrica.activate(applicationContext, config)
          // Automatic tracking of user activity.
          AppMetrica.enableActivityAutoTracking(this)
      }
  }
  ```

- Java

  ```java translate=no
  public class YourApplication extends Application {
      @Override
      public void onCreate() {
          super.onCreate();
          // Creating an extended library configuration.
          AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_KEY)
                  // Setting up the configuration. For example, to enable logging.
                  .withLogs()
                  // ...
                  .build();
          // Initializing the AppMetrica SDK.
          AppMetrica.activate(getApplicationContext(), config);
          // Automatic tracking of user activity.
          AppMetrica.enableActivityAutoTracking(this);
      }
  }
  ```

{% endlist %}

Чтобы настроить библиотеку в процессе работы приложения, используйте методы класса `AppMetrica`.

## Отправка статистики на дополнительный API key {#reporter-different-apikey}

Отправка данных на дополнительный API key позволяет собирать для каждого API key свою статистику. Это можно использовать для управления доступом к информации. Например, чтобы предоставить доступ к статистике для аналитиков, можно продублировать отправку маркетинговых данных на дополнительный API key и предоставить им доступ к этой статистике. Так у них будет доступ только к той информации, которая им необходима.

Для отправки данных на дополнительный API key необходимо использовать репортеры. С помощью них можно отправлять события, сообщения об ошибках, профили и информацию о покупках в приложении. Репортеры могут работать без инициализации AppMetrica SDK.

### Шаг 1. (Опционально) Инициализируйте репортер с расширенной конфигурацией {#reporter-different-apikey-initialize}

Чтобы инициализировать репортер с расширенной конфигурацией, создайте объект класса `ReporterConfig` с необходимыми настройками и активируйте репортер с помощью метода `AppMetrica.activateReporter(Context context, ReporterConfig config)`. Конфигурация применяется для репортера с указанным API key. Для каждого дополнительного API key можно настроить свою конфигурацию.

{% note alert %}

 Инициализацию репортера с расширенной конфигурацией необходимо проводить до первого обращения к репортеру. Иначе репортер будет инициализирован без конфигурации.

{% endnote %}

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  // Creating extended configuration of the reporter.
  // To create it, pass a ANOTHER_API_KEY that is different from the app's API_KEY.
  val reporterConfig = ReporterConfig.newConfigBuilder(ANOTHER_API_KEY)
      // Setting up the configuration. For example, to enable logging.
      .withLogs()
      // ...
      .build()
  // Initializing a reporter.
  AppMetrica.activateReporter(applicationContext, reporterConfig)
  ```

- Java

  ```java translate=no
  // Creating extended configuration of the reporter.
  // To create it, pass a ANOTHER_API_KEY that is different from the app's API_KEY.
  ReporterConfig reporterConfig = ReporterConfig.newConfigBuilder(ANOTHER_API_KEY)
          // Setting up the configuration. For example, to enable logging.
          .withLogs()
          // ...
          .build();
  // Initializing a reporter.
  AppMetrica.activateReporter(getApplicationContext(), reporterConfig);
  ```

{% endlist %}

### Шаг 2. Настройте отправку данных с помощью репортера {#reporter-different-apikey-send}

Для отправки данных с помощью репортера, необходимо получить объект, который реализует интерфейс `IReporter` с помощью метода `AppMetrica.getReporter(Context context, String apiKey)` и использовать методы интерфейса для отправки отчетов. Если репортер не был инициализирован с расширенной конфигурацией, то вызов данного метода произведет инициализацию репортера для указанного API key.

Пример отправки события:

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  AppMetrica.getReporter(applicationContext, ANOTHER_API_KEY).reportEvent("Updates installed")
  ```

- Java

  ```java translate=no
  AppMetrica.getReporter(getApplicationContext(), ANOTHER_API_KEY).reportEvent("Updates installed");
  ```

{% endlist %}

Для корректного отслеживания сессий взаимодействия пользователя с приложением настройте отправку событий о начале и приостановке сессии для каждого репортера. Для этого используйте методы `resumeSession()` и `pauseSession()` интерфейса `IReporter` в реализации `onResume()` и `onPause()` ваших Activity:

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  public class YourActivity : Activity() {
      override fun onResume() {
          super.onResume()
          AppMetrica.getReporter(applicationContext, ANOTHER_API_KEY).resumeSession()
      }

      override fun onPause() {
          AppMetrica.getReporter(applicationContext, ANOTHER_API_KEY).pauseSession()
          super.onPause()
      }
  }
  ```

- Java

  ```java translate=no
  public class YourActivity extends Activity {
      @Override
      protected void onResume() {
          super.onResume();
          AppMetrica.getReporter(getApplicationContext(), ANOTHER_API_KEY).resumeSession();
      }

      @Override
      protected void onPause() {
          AppMetrica.getReporter(getApplicationContext(), ANOTHER_API_KEY).pauseSession();
          super.onPause();
      }
  }
  ```

{% endlist %}

## Отслеживание аварийных остановок приложения {#set-report-crash}

Отчеты об аварийных остановках приложения отправляются по умолчанию.

Чтобы отключить автоматическое отслеживание, инициализируйте библиотеку с конфигурацией, в которой отправка информации об аварийных остановках приложения отключена. Для этого передайте значение `false` в метод `withCrashReporting(boolean enabled)` при создании расширенной конфигурации библиотеки.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  // Creating an extended library configuration.
  val config = AppMetrica.newConfigBuilder(API_KEY)
      // Disabling the data sending about the app crashes.
      .withCrashReporting(false)
      .build()
  // Initializing the AppMetrica SDK.
  AppMetrica.activate(applicationContext, config)
  ```

- Java

  ```java translate=no
  // Creating an extended library configuration.
  AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_KEY)
          // Disabling the data sending about the app crashes.
          .withCrashReporting(false)
          .build();
  // Initializing the AppMetrica SDK.
  AppMetrica.activate(getApplicationContext(), config);
  ```

{% endlist %}

Если автоматическое отслеживание отключено, вы можете [отправлять информацию об аварийных остановках вручную](#report-unhandled).

## Отслеживание аварийных остановок приложения вручную {#report-unhandled}

Отчеты об аварийных остановках приложения отправляются по умолчанию. Чтобы избежать дублирования событий при ручной отправке, необходимо отключить [автоматическое отслеживание аварийных остановок](#set-peropt-crash).

Чтобы отправлять информацию об аварийных остановках приложения вручную, используйте метод `AppMetrica.reportUnhandledException(Throwable exception)`:

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  val previousUncaughtExceptionHandler = Thread.getDefaultUncaughtExceptionHandler()
  // Creating a new handler.
  val uncaughtExceptionHandler = Thread.UncaughtExceptionHandler { thread, exception ->
      try {
          // Sending a message about an app crash to the AppMetrica server.
          AppMetrica.reportUnhandledException(exception)
      } finally {
          // Sending a message about an app crash to the system handler.
          previousUncaughtExceptionHandler?.uncaughtException(thread, exception)
      }
  }
  // Setting the default handler.
  Thread.setDefaultUncaughtExceptionHandler(uncaughtExceptionHandler)
  ```

- Java

  ```java translate=no
  final Thread.UncaughtExceptionHandler previousUncaughtExceptionHandler = Thread.getDefaultUncaughtExceptionHandler();
  // Creating a new handler.
  Thread.UncaughtExceptionHandler uncaughtExceptionHandler = new Thread.UncaughtExceptionHandler() {
      @Override
      public void uncaughtException(Thread thread, Throwable exception) {
          try {
              // Sending a message about an app crash to the AppMetrica server.
              AppMetrica.reportUnhandledException(exception);
          } finally {
              // Sending a message about an app crash to the system handler.
              if (previousUncaughtExceptionHandler != null) {
                  previousUncaughtExceptionHandler.uncaughtException(thread, exception);
              }
          }
      }
  };
  // Setting the default handler.
  Thread.setDefaultUncaughtExceptionHandler(uncaughtExceptionHandler);
  ```

{% endlist %}

## Отслеживание нативных аварийных остановок приложения {#native-crashes}

Отчеты о нативных аварийных остановках приложения отправляются автоматически, если SO-файлы библиотеки добавлены в проект.
По умолчанию SO-файлы отсутствуют.
Чтобы добавить их, настройте [AppMetrica Gradle Plugin](android-gradle-plugin.md) следующим образом:

{% list tabs %}

- build.gradle.kts

  ```kotlin translate=no
  appmetrica {
      ...
      ndk {
          enable = { applicationVariant -> true }
      }
  }
  ```

- build.gradle

  ```groovy translate=no
  appmetrica {
      ...
      ndk {
          enable = { applicationVariant -> true }
      }
  }
  ```

{% endlist %}

Плагин автоматически подключит необходимые зависимости.
Подключаемая плагином бибилотека содержит so-файлы для всех платформ (arm, armv7, mips, x86).
Используйте [abi splits](https://developer.android.com/studio/build/configure-apk-splits#configure-abi-split) для исключения неиспользуемых so-файлов.

{% cut "Если вы не используете Gradle" %}

[Загрузите](https://repo1.maven.org/maven2/io/appmetrica/analytics/analytics-ndk-crashes/{{ io-appmetrica-analytics-analytics-ndk-crashes }}/analytics-ndk-crashes-{{ io-appmetrica-analytics-analytics-ndk-crashes }}.aar) и добавьте библиотеку в проект.

{% endcut %}

Чтобы отключить автоматическое отслеживание, инициализируйте библиотеку с конфигурацией, в которой отправка информации о нативных аварийных остановках приложения отключена.
Для этого передайте значение `false` в метод `withNativeCrashReporting(boolean enabled)` при создании расширенной конфигурации библиотеки.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  // Creating an extended library configuration.
  val config = AppMetricaConfig.newConfigBuilder(API_KEY)
      // Disabling the data sending about the native app crashes.
      .withNativeCrashReporting(false)
      .build()
  // Initializing the AppMetrica SDK.
  AppMetrica.activate(applicationContext, config)
  ```

- Java

  ```java translate=no
  // Creating an extended library configuration.
  AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_KEY)
          // Disabling the data sending about the native app crashes.
          .withNativeCrashReporting(false)
          .build();
  // Initializing the AppMetrica SDK.
  AppMetrica.activate(getApplicationContext(), config);
  ```

{% endlist %}

[Подробнее о нативном коде](https://developer.android.com/tools/sdk/ndk/index.html#Using).

## Отправка рекламных идентификаторов библиотекой {#track-adv-identifiers}

{% note info %}

Отправка рекламных идентификаторов с событиями по умолчанию включена.

{% endnote %}

Если вам необходимо отключить сбор рекламных идентификаторов по какой-либо причине, например, вы ожидаете согласие пользователя, отключите отправку на этапе инициализации библиотеки. Для этого передайте значение `false` в метод `withAdvIdentifiersTracking (boolean enabled)` при создании конфигурации.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  // Creating an extended library configuration.
  val config = AppMetricaConfig.newConfigBuilder(API_KEY)
      // Disabling advertising identifiers tracking
      .withAdvIdentifiersTracking(false)
      .build()
  // Initializing the AppMetrica SDK.
  AppMetrica.activate(applicationContext, config)
  ```

- Java

  ```java translate=no
  // Creating an extended library configuration.
  AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_KEY)
          // Disabling advertising identifiers tracking
          .withAdvIdentifiersTracking(false)
          .build();
  // Initializing the AppMetrica SDK.
  AppMetrica.activate(getApplicationContext(), config);
  ```

{% endlist %}

После получения согласия пользователя рекомендуется включить сбор рекламных идентификаторов в процессе работы. Для этого передайте значение `true` в метод `AppMetrica.setAdvIdentifiersTracking(boolean enabled)`.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  // Enabling advertising identifiers tracking
  AppMetrica.setAdvIdentifiersTracking(true)
  ```

- Java

  ```java translate=no
  // Enabling advertising identifiers tracking
  AppMetrica.setAdvIdentifiersTracking(true);
  ```

{% endlist %}

## Отправка местоположения устройства библиотекой {#track-location}

{% note info "" %}

Отправка местоположения устройства по умолчанию отключена.

Начиная с версии 5.0.0 AppMetrica SDK по умолчанию инициализируется с отключенной опцией `locationTracking`.

{% endnote %}

Чтобы включить отправку, инициализируйте библиотеку с конфигурацией, в которой отправка информации о местоположении устройства включена. Для этого передайте значение `true` в метод `withLocationTracking(boolean enabled)` при создании расширенной конфигурации библиотеки.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  // Creating an extended library configuration.
  val config = AppMetricaConfig.newConfigBuilder(API_KEY)
      // Enabling the data sending about the device location.
      .withLocationTracking(true)
      .build()
  // Initializing the AppMetrica SDK.
  AppMetrica.activate(applicationContext, config)
  ```

- Java

  ```java translate=no
  // Creating an extended library configuration.
  AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_KEY)
          // Enabling the data sending about the device location.
          .withLocationTracking(true)
          .build();
  // Initializing the AppMetrica SDK.
  AppMetrica.activate(getApplicationContext(), config);
  ```

{% endlist %}

Чтобы включить отправку в процессе работы приложения, используйте метод `AppMetrica.setLocationTracking(boolean enabled)`:

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  AppMetrica.setLocationTracking(true)
  ```

- Java

  ```java translate=no
  AppMetrica.setLocationTracking(true);
  ```

{% endlist %}

Для более точного определения местоположения добавьте в файл AndroidManifest.xml одно из следующих разрешений:

- [android.permission.ACCESS_COARSE_LOCATION](https://developer.android.com/reference/android/Manifest.permission.html#ACCESS_COARSE_LOCATION) — для приблизительного определения.
- [android.permission.ACCESS_FINE_LOCATION](https://developer.android.com/reference/android/Manifest.permission.html#ACCESS_FINE_LOCATION) — для точного определения.

Например:

```xml translate=no
<manifest>
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
    <application>...</application>
</manifest>
```

## Установка местоположения вручную {#location-manual}

Перед отправкой собственной информации о местоположении устройства убедитесь, что отправка отчетов была включена.

Библиотека определяет местоположение устройства самостоятельно. Чтобы отправить собственную информацию о местоположении устройства, передайте объект класса [android.location.Location](https://developer.android.com/reference/android/location/Location) в метод `AppMetrica.setLocation(Location location)`.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  // Determining the location.
  val currentLocation = ...
  // Setting your own location information of the device.
  AppMetrica.setLocation(currentLocation)
  ```

- Java

  ```java translate=no
  // Determining the location.
  Location currentLocation = ...;
  // Setting your own location information of the device.
  AppMetrica.setLocation(currentLocation);
  ```

{% endlist %}

Чтобы отправить собственную информацию о местоположении устройства с помощью стартовой конфигурации, передайте объект `android.location.Location` в метод `withLocation(Location location)` при создании расширенной конфигурации библиотеки.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  // Determining the location.
  val currentLocation = ...

  // Creating an extended library configuration.
  AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_KEY)
      // Set your own location information of the device.
      .withLocation(currentLocation)
      .build()
  // Initializing the AppMetrica SDK.
  AppMetrica.activate(applicationContext, config)
  ```

- Java

  ```java translate=no
  // Determining the location.
  Location currentLocation = ...;

  // Creating an extended library configuration.
  AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_KEY)
          // Set your own location information of the device.
          .withLocation(currentLocation)
          .build();
  // Initializing the AppMetrica SDK.
  AppMetrica.activate(getApplicationContext(), config);
  ```

{% endlist %}

Чтобы возобновить определение местоположения библиотекой, передайте в метод `AppMetrica.setLocation(Location location)` значение `null` и настройте [отправку местоположения устройства](#track-location).

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  AppMetrica.setLocation(null)
  ```

- Java

  ```java translate=no
  AppMetrica.setLocation(null);
  ```

{% endlist %}

## Отправка собственного события {#report-event}

Чтобы отправить собственное событие без вложенных параметров, передайте короткое название или описание события в метод `AppMetrica.reportEvent(String eventName)`:

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  AppMetrica.reportEvent("Updates installed")
  ```

- Java

  ```java translate=no
  AppMetrica.reportEvent("Updates installed");
  ```

{% endlist %}

## Отправка собственного события с вложенными параметрами {#report-event-params}

AppMetrica SDK позволяет отправлять собственные события с вложенными параметрами, которые могут быть заданы в формате JSON или в виде набора атрибутов (Map).

**JSON**

Чтобы передать вложенные параметры события в формате JSON, используйте метод `AppMetrica.reportEvent(String eventName, String jsonValue)`:

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  val eventParameters = """{"name":"Alice", "age":"18"}"""

  AppMetrica.reportEvent("New person", eventParameters)
  ```

- Java

  ```java translate=no
  String eventParameters = "{\"name\":\"Alice\", \"age\":\"18\"}";

  AppMetrica.reportEvent("New person", eventParameters);
  ```

{% endlist %}

**Map**

Чтобы передать вложенные параметры события в виде набора атрибутов (Map), используйте метод `AppMetrica.reportEvent(String eventName, Map<String, Object> attributes)`:

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  val eventParameters = mapOf("name" to "Alice", "age" to 18)

  AppMetrica.reportEvent("New person", eventParameters)
  ```

- Java

  ```java translate=no
  Map<String, Object> eventParameters = new HashMap<String, Object>();
  eventParameters.put("name", "Alice");
  eventParameters.put("age", 18);

  AppMetrica.reportEvent("New person", eventParameters);
  ```

{% endlist %}


Веб-интерфейс AppMetrica отображает до пяти уровней вложенности события. Если событие содержит шесть уровней и более, в отчете отобразятся пять верхних. С помощью [API отчетов](../../../mobile-api/api_v1/intro.md) можно выгрузить до десяти уровней.

Подробнее о событиях в разделе [События](../../../data-collection/about-events.md).

## Отправка события из JavaScript-кода WebView {#js-event}

AppMetrica SDK позволяет отправлять клиентские события из JavaScript-кода. Инициализируйте отправку вызовом метода `initWebViewReporting`:

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  val webView = findViewById<WebView>(R.id.myWebView)
  // do your initialization here
  webView.settings.javaScriptEnabled = true
  AppMetrica.initWebViewReporting(webView)
  webView.loadUrl(myURL)
  ```

- Java

  ```java translate=no
  WebView webView = (WebView) findViewById(R.id.myWebView);
  // do your initialization here
  webView.getSettings().setJavaScriptEnabled(true);
  AppMetrica.initWebViewReporting(webView);
  webView.loadUrl(myURL);
  ```

{% endlist %}

Вызывайте метод `initWebViewReporting` после вызова метода `setJavaScriptEnabled` и до вызова loadUrl.

Для отправки события из JavaScript-кода используйте метод `reportEvent(name, value)` интерфейса AppMetrica:

**Javascript**

  ```javascript translate=no
  function buttonClicked() {
    AppMetrica.reportEvent('Button clicked!', '{}');
  }
  ```

Аргументы метода `reportEvent`:

- `name` — строка. Не может быть null или пустым.
- `value` — JSON-строка. Может быть null.

## Отправка собственного сообщения об ошибке {#send-report-error}

Чтобы отправить собственное сообщение об ошибке, используйте методы:

- `AppMetrica.reportError(String message, Throwable error)`
- `AppMetrica.reportError(String groupIdentifier, String message)`
- `AppMetrica.reportError(String groupIdentifier, String message, Throwable error)`

{% cut "Пример c groupIdentifier" %}

Если ошибки отправляются с помощью методов c groupIdentifier, они группируются по идентификатору.

   {% list tabs group=instructions %}

   - Kotlin

     ```kotlin translate=no
     try {
         "00xffWr0ng".toInt()
     } catch (error: Throwable) {
         AppMetrica.reportError("Your ID", "Error while parsing some integer number", error)
     }
     ```

   - Java

     ```java translate=no
     try {
         Integer.valueOf("00xffWr0ng");
     } catch (Throwable error) {
         AppMetrica.reportError("Your ID", "Error while parsing some integer number", error);
     }
     ```

   {% endlist %}

Не используйте переменные значения в качестве идентификатора для группировки. Иначе количество групп будет увеличиваться и их будет сложно анализировать.

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/id-group-android.png){style="border: solid 1px #cccccc; max-width: 800px;"}

{% endcut %}

{% cut "Пример c message" %}

Если ошибки отправляются с помощью метода `AppMetrica.reportError(String message, Throwable error)`, они группируются по [stack trace](https://en.wikipedia.org/wiki/Stack_trace).

   {% list tabs group=instructions %}

   - Kotlin

     ```kotlin translate=no
     try {
         "00xffWr0ng".toInt()
     } catch (error: Throwable) {
         AppMetrica.reportError("Error while parsing some integer number", error)
     }
     ```

   - Java

     ```java translate=no
     try {
         Integer.valueOf("00xffWr0ng");
     } catch (Throwable error) {
         AppMetrica.reportError("Error while parsing some integer number", error);
     }
     ```

   {% endlist %}

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/msg-group-android.png){style="border: solid 1px #cccccc; max-width: 800px;"}

{% endcut %}

## Отправка событий из буфера {#send-events-buffer}

AppMetrica SDK не отправляет событие сразу после того, как оно произошло. Библиотека хранит данные о событиях в буфере. Метод `sendEventsBuffer` инициирует отправку данных из буфера и очищает его. Используйте этот метод для принудительной отправки сохраненных событий после прохождения важных сценариев пользователя.


{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  AppMetrica.sendEventsBuffer()
  ```

- Java

  ```java translate=no
  AppMetrica.sendEventsBuffer();
  ```

{% endlist %}

{% note alert "" %}

Частое использование метода может привести к повышению энергопотребления и расходу интернет-трафика.

{% endnote %}

## Отправка ProfileId {#send-profile-id}

Если идентификатор пользовательского профиля известен до инициализации AppMetrica SDK, передавайте его до инициализации (`setUserProfileID`) или во время инициализации с расширенной конфигурацией (`withUserProfileID`).

В противном случае будет создан пользовательский профиль с идентификатором `appmetrica_device_id`.

{% note warning "" %}

Если отправка `ProfileId` не настроена, [предопределенные атрибуты](../../../data-collection/profile-attributes.md#pre-defined) не отображаются в веб-интерфейсе.

{% endnote %}

В любой момент можно обновить `ProfileId` с помощью вызова `setUserProfileID`:

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  AppMetrica.setUserProfileID("id")
  ```

- Java

  ```java translate=no
  AppMetrica.setUserProfileID("id");
  ```

   {% endlist %}

## Отправка атрибутов профиля {#send-attribute-profile}

Чтобы отправить атрибуты профиля, передайте в объект `UserProfile` необходимые атрибуты и отправьте этот объект с помощью метода `AppMetrica.reportUserProfile(UserProfile profile)`. Атрибуты профиля создаются с помощью методов класса `Attribute`.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  // Creating the UserProfile instance.
  val userProfile = UserProfile.newBuilder()
      // Updating predefined attributes.
      .apply(Attribute.name().withValue("John"))
      .apply(Attribute.gender().withValue(GenderAttribute.Gender.MALE))
      .apply(Attribute.birthDate().withAge(24))
      .apply(Attribute.notificationsEnabled().withValue(false))
      // Updating custom attributes.
      .apply(Attribute.customString("string_attribute").withValue("string"))
      .apply(Attribute.customNumber("number_attribute").withValue(55.0))
      .apply(Attribute.customCounter("counter_attribute").withDelta(1.0))
      .build()
  // Setting the ProfileID using the method of the AppMetrica class.
  AppMetrica.setUserProfileID("id")

  // Sending the UserProfile instance.
  AppMetrica.reportUserProfile(userProfile)
  ```

- Java

  ```java translate=no
  // Creating the UserProfile instance.
  UserProfile userProfile = UserProfile.newBuilder()
          // Updating predefined attributes.
          .apply(Attribute.name().withValue("John"))
          .apply(Attribute.gender().withValue(GenderAttribute.Gender.MALE))
          .apply(Attribute.birthDate().withAge(24))
          .apply(Attribute.notificationsEnabled().withValue(false))
          // Updating custom attributes.
          .apply(Attribute.customString("string_attribute").withValue("string"))
          .apply(Attribute.customNumber("number_attribute").withValue(55))
          .apply(Attribute.customCounter("counter_attribute").withDelta(1))
          .build();
  // Setting the ProfileID using the method of the AppMetrica class.
  AppMetrica.setUserProfileID("id");

  // Sending the UserProfile instance.
  AppMetrica.reportUserProfile(userProfile);
  ```

{% endlist %}

## Отправка ECommerce-событий {#send-ecommerce}

В AppMetrica нет возможности сегментировать ECommerce-события на «тестовые» и «не тестовые». Если для отладки покупок вы используете основной API key, то тестовые события будут попадать в общую статистику. Поэтому, чтобы отладить отправку ECommerce-событий, используйте отправку статистики на дополнительный API key с помощью репортера.

### Шаг 1. Настройте отправку ECommerce-событий на тестовый API key {#send-ecommerce-test-key}

Для различных действий пользователя есть соответствующие типы ECommerce-событий. Чтобы создать конкретный тип события, используйте нужный метод класса `ECommerceEvent`.

Ниже приведены примеры отправки конкретных типов событий:

{% cut "Открытие страницы" %}

   {% list tabs group=instructions %}

   - Kotlin

     ```kotlin translate=no
     val payload = mapOf(
         "configuration" to "landscape",
         "full_screen" to "true",
     )
     // Creating a screen object.
     val screen = ECommerceScreen()
         .setCategoriesPath(listOf("Акции", "Красная цена")) // Optional.
         .setName("ProductCardActivity") // Optional.
         .setSearchQuery("даниссимо кленовый сироп") // Optional.
         .setPayload(payload) // Optional.
     val showScreenEvent = ECommerceEvent.showScreenEvent(screen)
     // Sending an e-commerce event.
     AppMetrica.getReporter(applicationContext, "Testing API key").reportECommerce(showScreenEvent)
     ```

   - Java

     ```java translate=no
     Map<String, String> payload = new HashMap<>();
     payload.put("configuration", "landscape");
     payload.put("full_screen", "true");
     // Creating a screen object.
     CommerceScreen screen = new ECommerceScreen()
             .setCategoriesPath(Arrays.asList("Акции", "Красная цена")) // Optional.
             .setName("ProductCardActivity") // Optional.
             .setSearchQuery("даниссимо кленовый сироп") // Optional.
             .setPayload(payload); // Optional.
     ECommerceEvent showScreenEvent = ECommerceEvent.showScreenEvent(screen);
     // Sending an e-commerce event.
     AppMetrica.getReporter(getApplicationContext(), "Testing API key").reportECommerce(showScreenEvent);
     ```

   {% endlist %}

{% endcut %}

{% cut "Просмотр карточки товара" %}

   {% list tabs group=instructions %}

   - Kotlin

     ```kotlin translate=no
     val payload = mapOf(
         "configuration" to "landscape",
         "full_screen" to "true",
     )
     // Creating a screen object.
     val screen = ECommerceScreen()
         .setCategoriesPath(listOf("Акции", "Красная цена")) // Optional.
         .setName("ProductCardActivity") // Optional.
         .setSearchQuery("даниссимо кленовый сироп") // Optional.
         .setPayload(payload) // Optional.
     // Creating an actualPrice object.
     val actualPrice = ECommercePrice(ECommerceAmount(4.53, "USD"))
         .setInternalComponents(listOf( // Optional.
             ECommerceAmount(30570000, "wood"),
             ECommerceAmount(26.89, "iron"),
             ECommerceAmount(BigDecimal("5.1"), "gold")
         ))
     // Creating an originalPrice object.
     val originalPrice = ECommercePrice(ECommerceAmount(5.78, "USD"))
         .setInternalComponents(listOf( // Optional.
             ECommerceAmount(30590000, "wood"),
             ECommerceAmount(26.92, "iron"),
             ECommerceAmount(BigDecimal("5.5"), "gold")
         ))
     // Creating a product object.
     val product = ECommerceProduct("779213")
         .setActualPrice(actualPrice) // Optional.
         .setPromocodes(listOf("BT79IYX", "UT5412EP")) // Optional.
         .setPayload(payload) // Optional.
         .setOriginalPrice(originalPrice) // Optional.
         .setName("Продукт творожный «Даниссимо» 5.9%, 130 г.") // Optional.
         .setCategoriesPath(listOf("Продукты", "Молочные продукты", "Йогурты")) // Optional.
     val showProductCardEvent = ECommerceEvent.showProductCardEvent(product, screen)
     // Sending an e-commerce event.
     AppMetrica.getReporter(applicationContext, "Testing API key").reportECommerce(showProductCardEvent)
     ```

   - Java

     ```java translate=no
     Map<String, String> payload = new HashMap<>();
     payload.put("configuration", "landscape");
     payload.put("full_screen", "true");
     // Creating a screen object.
     ECommerceScreen screen = new ECommerceScreen()
             .setCategoriesPath(Arrays.asList("Акции", "Красная цена")) // Optional.
             .setName("ProductCardActivity") // Optional.
             .setSearchQuery("даниссимо кленовый сироп") // Optional.
             .setPayload(payload); // Optional.
     // Creating an actualPrice object.
     ECommercePrice actualPrice = new ECommercePrice(new ECommerceAmount(4.53, "USD"))
             .setInternalComponents(Arrays.asList( // Optional.
                     new ECommerceAmount(30_570_000, "wood"),
                     new ECommerceAmount(26.89, "iron"),
                     new ECommerceAmount(new BigDecimal("5.1"), "gold")
             ));
     // Creating an originalPrice object.
     ECommercePrice originalPrice = new ECommercePrice(new ECommerceAmount(5.78, "USD"))
             .setInternalComponents(Arrays.asList( // Optional.
                     new ECommerceAmount(30_590_000, "wood"),
                     new ECommerceAmount(26.92, "iron"),
                     new ECommerceAmount(new BigDecimal("5.5"), "gold")
             ));
     // Creating a product object.
     ECommerceProduct product = new ECommerceProduct("779213")
             .setActualPrice(actualPrice) // Optional.
             .setPromocodes(Arrays.asList("BT79IYX", "UT5412EP")) // Optional.
             .setPayload(payload) // Optional.
             .setOriginalPrice(originalPrice) // Optional.
             .setName("Продукт творожный «Даниссимо» 5.9%, 130 г.") // Optional.
             .setCategoriesPath(Arrays.asList("Продукты", "Молочные продукты", "Йогурты")); // Optional.
     ECommerceEvent showProductCardEvent = ECommerceEvent.showProductCardEvent(product, screen);
     // Sending an e-commerce event.
     AppMetrica.getReporter(getApplicationContext(), "Testing API key").reportECommerce(showProductCardEvent);
     ```

   {% endlist %}

{% endcut %}

{% cut "Просмотр страницы товара" %}

   {% list tabs group=instructions %}

   - Kotlin

     ```kotlin translate=no
     val payload = mapOf(
         "configuration" to "landscape",
         "full_screen" to "true",
     )
     // Creating a screen object.
     val screen = ECommerceScreen()
         .setCategoriesPath(listOf("Акции", "Красная цена")) // Optional.
         .setName("ProductCardActivity") // Optional.
         .setSearchQuery("даниссимо кленовый сироп") // Optional.
         .setPayload(payload) // Optional.
     // Creating an actualPrice object.
     val actualPrice = ECommercePrice(ECommerceAmount(4.53, "USD"))
         .setInternalComponents(listOf( // Optional.
             ECommerceAmount(30570000, "wood"),
             ECommerceAmount(26.89, "iron"),
             ECommerceAmount(BigDecimal("5.1"), "gold")
         ))
     // Creating an originalPrice object.
     val originalPrice = ECommercePrice(ECommerceAmount(5.78, "USD"))
         .setInternalComponents(listOf( // Optional.
             ECommerceAmount(30590000, "wood"),
             ECommerceAmount(26.92, "iron"),
             ECommerceAmount(BigDecimal("5.5"), "gold")
         ))
     // Creating a product object.
     val product = ECommerceProduct("779213")
         .setActualPrice(actualPrice) // Optional.
         .setPromocodes(listOf("BT79IYX", "UT5412EP")) // Optional.
         .setPayload(payload) // Optional.
         .setOriginalPrice(originalPrice) // Optional.
         .setName("Продукт творожный «Даниссимо» 5.9%, 130 г.") // Optional.
         .setCategoriesPath(listOf("Продукты", "Молочные продукты", "Йогурты")) // Optional.
     // Creating a referrer object.
     val referrer = ECommerceReferrer()
         .setType("button") // Optional.
         .setIdentifier("76890") // Optional.
         .setScreen(screen) // Optional.
     val showProductDetailsEvent = ECommerceEvent.showProductDetailsEvent(product, referrer) // Referrer is optional — can be null.
     // Sending an e-commerce event.
     AppMetrica.getReporter(applicationContext, "Testing API key").reportECommerce(showProductDetailsEvent)
     ```

   - Java

     ```java translate=no
     Map<String, String> payload = new HashMap<>();
     payload.put("configuration", "landscape");
     payload.put("full_screen", "true");
     // Creating a screen object.
     ECommerceScreen screen = new ECommerceScreen()
             .setCategoriesPath(Arrays.asList("Акции", "Красная цена")) // Optional.
             .setName("ProductCardActivity") // Optional.
             .setSearchQuery("даниссимо кленовый сироп") // Optional.
             .setPayload(payload); // Optional.
     // Creating an actualPrice object.
     ECommercePrice actualPrice = new ECommercePrice(new ECommerceAmount(4.53, "USD"))
             .setInternalComponents(Arrays.asList( // Optional.
                     new ECommerceAmount(30_570_000, "wood"),
                     new ECommerceAmount(26.89, "iron"),
                     new ECommerceAmount(new BigDecimal("5.1"), "gold")
             ));
     // Creating an originalPrice object.
     ECommercePrice originalPrice = new ECommercePrice(new ECommerceAmount(5.78, "USD"))
             .setInternalComponents(Arrays.asList( // Optional.
                     new ECommerceAmount(30_590_000, "wood"),
                     new ECommerceAmount(26.92, "iron"),
                     new ECommerceAmount(new BigDecimal("5.5"), "gold")
             ));
     // Creating a product object.
     ECommerceProduct product = new ECommerceProduct("779213")
             .setActualPrice(actualPrice) // Optional.
             .setPromocodes(Arrays.asList("BT79IYX", "UT5412EP")) // Optional.
             .setPayload(payload) // Optional.
             .setOriginalPrice(originalPrice) // Optional.
             .setName("Продукт творожный «Даниссимо» 5.9%, 130 г.") // Optional.
             .setCategoriesPath(Arrays.asList("Продукты", "Молочные продукты", "Йогурты")); // Optional.
     // Creating a referrer object.
     ECommerceReferrer referrer = new ECommerceReferrer()
             .setType("button") // Optional.
             .setIdentifier("76890") // Optional.
             .setScreen(screen); // Optional.
     ECommerceEvent showProductDetailsEvent = ECommerceEvent.showProductDetailsEvent(product, referrer); // Referrer is optional — can be null.
     // Sending an e-commerce event.
     AppMetrica.getReporter(getApplicationContext(), "Testing API key").reportECommerce(showProductDetailsEvent);
     ```

   {% endlist %}

{% endcut %}

{% cut "Добавление или удаление товара из корзины" %}

   {% list tabs group=instructions %}

   - Kotlin

     ```kotlin translate=no
     val payload = mapOf(
         "configuration" to "landscape",
         "full_screen" to "true",
     )
     // Creating a screen object.
     val screen = ECommerceScreen()
         .setCategoriesPath(listOf("Акции", "Красная цена")) // Optional.
         .setName("ProductCardActivity") // Optional.
         .setSearchQuery("даниссимо кленовый сироп") // Optional.
         .setPayload(payload) // Optional.
     // Creating an actualPrice object.
     val actualPrice = ECommercePrice(ECommerceAmount(4.53, "USD"))
         .setInternalComponents(listOf( // Optional.
             ECommerceAmount(30570000, "wood"),
             ECommerceAmount(26.89, "iron"),
             ECommerceAmount(BigDecimal("5.1"), "gold")
         ))
     // Creating an originalPrice object.
     val originalPrice = ECommercePrice(ECommerceAmount(5.78, "USD"))
         .setInternalComponents(listOf( // Optional.
             ECommerceAmount(30590000, "wood"),
             ECommerceAmount(26.92, "iron"),
             ECommerceAmount(BigDecimal("5.5"), "gold")
         ))
     // Creating a product object.
     val product = ECommerceProduct("779213")
         .setActualPrice(actualPrice) // Optional.
         .setPromocodes(listOf("BT79IYX", "UT5412EP")) // Optional.
         .setPayload(payload) // Optional.
         .setOriginalPrice(originalPrice) // Optional.
         .setName("Продукт творожный «Даниссимо» 5.9%, 130 г.") // Optional.
         .setCategoriesPath(listOf("Продукты", "Молочные продукты", "Йогурты")) // Optional.
     // Creating a referrer object.
     val referrer = ECommerceReferrer()
         .setType("button") // Optional.
         .setIdentifier("76890") // Optional.
         .setScreen(screen) // Optional.
     // Creating a cartItem object.
     val addedItems1 = ECommerceCartItem(product, actualPrice, 1.0)
         .setReferrer(referrer) // Optional.
     val addCartItemEvent = ECommerceEvent.addCartItemEvent(addedItems1)
     // Sending an e-commerce event.
     AppMetrica.getReporter(applicationContext, "Testing API key").reportECommerce(addCartItemEvent)
     val removeCartItemEvent = ECommerceEvent.removeCartItemEvent(addedItems1)
     // Sending an e-commerce event.
     AppMetrica.getReporter(applicationContext, "Testing API key").reportECommerce(removeCartItemEvent)
     ```

   - Java

     ```java translate=no
     Map<String, String> payload = new HashMap<>();
     payload.put("configuration", "landscape");
     payload.put("full_screen", "true");
     // Creating a screen object.
     ECommerceScreen screen = new ECommerceScreen()
             .setCategoriesPath(Arrays.asList("Акции", "Красная цена")) // Optional.
             .setName("ProductCardActivity") // Optional.
             .setSearchQuery("даниссимо кленовый сироп") // Optional.
             .setPayload(payload); // Optional.
     // Creating an actualPrice object.
     ECommercePrice actualPrice = new ECommercePrice(new ECommerceAmount(4.53, "USD"))
             .setInternalComponents(Arrays.asList( // Optional.
                     new ECommerceAmount(30_570_000, "wood"),
                     new ECommerceAmount(26.89, "iron"),
                     new ECommerceAmount(new BigDecimal("5.1"), "gold")
             ));
     // Creating an originalPrice object.
     ECommercePrice originalPrice = new ECommercePrice(new ECommerceAmount(5.78, "USD"))
             .setInternalComponents(Arrays.asList( // Optional.
                     new ECommerceAmount(30_590_000, "wood"),
                     new ECommerceAmount(26.92, "iron"),
                     new ECommerceAmount(new BigDecimal("5.5"), "gold")
             ));
     // Creating a product object.
     ECommerceProduct product = new ECommerceProduct("779213")
             .setActualPrice(actualPrice) // Optional.
             .setPromocodes(Arrays.asList("BT79IYX", "UT5412EP")) // Optional.
             .setPayload(payload) // Optional.
             .setOriginalPrice(originalPrice) // Optional.
             .setName("Продукт творожный «Даниссимо» 5.9%, 130 г.") // Optional.
             .setCategoriesPath(Arrays.asList("Продукты", "Молочные продукты", "Йогурты")); // Optional.
     // Creating a referrer object.
     ECommerceReferrer referrer = new ECommerceReferrer()
             .setType("button") // Optional.
             .setIdentifier("76890") // Optional.
             .setScreen(screen); // Optional.
     // Creating a cartItem object.
     ECommerceCartItem addedItems1 = new ECommerceCartItem(product, actualPrice, 1.0)
             .setReferrer(referrer); // Optional.
     ECommerceEvent addCartItemEvent = ECommerceEvent.addCartItemEvent(addedItems1);
     // Sending an e-commerce event.
     AppMetrica.getReporter(getApplicationContext(), "Testing API key").reportECommerce(addCartItemEvent);
     ECommerceEvent removeCartItemEvent = ECommerceEvent.removeCartItemEvent(addedItems1);
     // Sending an e-commerce event.
     AppMetrica.getReporter(getApplicationContext(), "Testing API key").reportECommerce(removeCartItemEvent);
     ```

   {% endlist %}

{% endcut %}

{% cut "Начало оформления и завершение покупки" %}

   {% list tabs group=instructions %}

   - Kotlin

     ```kotlin translate=no
     val payload = mapOf(
         "configuration" to "landscape",
         "full_screen" to "true",
     )
     // Creating a screen object.
     val screen = ECommerceScreen()
         .setCategoriesPath(listOf("Акции", "Красная цена")) // Optional.
         .setName("ProductCardActivity") // Optional.
         .setSearchQuery("даниссимо кленовый сироп") // Optional.
         .setPayload(payload) // Optional.
     // Creating an actualPrice object.
     val actualPrice = ECommercePrice(ECommerceAmount(4.53, "USD"))
         .setInternalComponents(listOf( // Optional.
             ECommerceAmount(30570000, "wood"),
             ECommerceAmount(26.89, "iron"),
             ECommerceAmount(BigDecimal("5.1"), "gold")
         ))
     // Creating an originalPrice object.
     val originalPrice = ECommercePrice(ECommerceAmount(5.78, "USD"))
         .setInternalComponents(listOf( // Optional.
             ECommerceAmount(30590000, "wood"),
             ECommerceAmount(26.92, "iron"),
             ECommerceAmount(BigDecimal("5.5"), "gold")
         ))
     // Creating a product object.
     val product = ECommerceProduct("779213")
         .setActualPrice(actualPrice) // Optional.
         .setPromocodes(listOf("BT79IYX", "UT5412EP")) // Optional.
         .setPayload(payload) // Optional.
         .setOriginalPrice(originalPrice) // Optional.
         .setName("Продукт творожный «Даниссимо» 5.9%, 130 г.") // Optional.
         .setCategoriesPath(listOf("Продукты", "Молочные продукты", "Йогурты")) // Optional.
     // Creating a referrer object.
     val referrer = ECommerceReferrer()
         .setType("button") // Optional.
         .setIdentifier("76890") // Optional.
         .setScreen(screen) // Optional.
     // Creating a cartItem object.
     val addedItems1 = ECommerceCartItem(product, actualPrice, 1.0)
         .setReferrer(referrer) // Optional.
     // Creating an order object.
     val order = ECommerceOrder("88528768", listOf(addedItems1))
         .setPayload(payload) // Optional.
     val beginCheckoutEvent = ECommerceEvent.beginCheckoutEvent(order)
     // Sending an e-commerce event.
     AppMetrica.getReporter(applicationContext, "Testing API key").reportECommerce(beginCheckoutEvent)
     val purchaseEvent = ECommerceEvent.purchaseEvent(order)
     // Sending an e-commerce event.
     AppMetrica.getReporter(applicationContext, "Testing API key").reportECommerce(purchaseEvent)
     ```

   - Java

     ```java translate=no
     Map<String, String> payload = new HashMap<>();
     payload.put("configuration", "landscape");
     payload.put("full_screen", "true");
     // Creating a screen object.
     ECommerceScreen screen = new ECommerceScreen()
             .setCategoriesPath(Arrays.asList("Акции", "Красная цена")) // Optional.
             .setName("ProductCardActivity") // Optional.
             .setSearchQuery("даниссимо кленовый сироп") // Optional.
             .setPayload(payload); // Optional.
     // Creating an actualPrice object.
     ECommercePrice actualPrice = new ECommercePrice(new ECommerceAmount(4.53, "USD"))
             .setInternalComponents(Arrays.asList( // Optional.
                     new ECommerceAmount(30_570_000, "wood"),
                     new ECommerceAmount(26.89, "iron"),
                     new ECommerceAmount(new BigDecimal("5.1"), "gold")
             ));
     // Creating an originalPrice object.
     ECommercePrice originalPrice = new ECommercePrice(new ECommerceAmount(5.78, "USD"))
             .setInternalComponents(Arrays.asList( // Optional.
                     new ECommerceAmount(30_590_000, "wood"),
                     new ECommerceAmount(26.92, "iron"),
                     new ECommerceAmount(new BigDecimal("5.5"), "gold")
             ));
     // Creating a product object.
     ECommerceProduct product = new ECommerceProduct("779213")
             .setActualPrice(actualPrice) // Optional.
             .setPromocodes(Arrays.asList("BT79IYX", "UT5412EP")) // Optional.
             .setPayload(payload) // Optional.
             .setOriginalPrice(originalPrice) // Optional.
             .setName("Продукт творожный «Даниссимо» 5.9%, 130 г.") // Optional.
             .setCategoriesPath(Arrays.asList("Продукты", "Молочные продукты", "Йогурты")); // Optional.
     // Creating a referrer object.
     ECommerceReferrer referrer = new ECommerceReferrer()
             .setType("button") // Optional.
             .setIdentifier("76890") // Optional.
             .setScreen(screen); // Optional.
     // Creating a cartItem object.
     ECommerceCartItem addedItems1 = new ECommerceCartItem(product, actualPrice, 1.0)
             .setReferrer(referrer); // Optional.
     // Creating an order object.
     ECommerceOrder order = new ECommerceOrder("88528768", Arrays.asList(addedItems1))
             .setPayload(payload); // Optional.
     ECommerceEvent beginCheckoutEvent = ECommerceEvent.beginCheckoutEvent(order);
     // Sending an e-commerce event.
     AppMetrica.getReporter(getApplicationContext(), "Testing API key").reportECommerce(beginCheckoutEvent);
     ECommerceEvent purchaseEvent = ECommerceEvent.purchaseEvent(order);
     // Sending an e-commerce event.
     AppMetrica.getReporter(getApplicationContext(), "Testing API key").reportECommerce(purchaseEvent);
     ```

   {% endlist %}

{% endcut %}

### Шаг 2. Проверьте отчет тестового приложения {#send-ecommerce-test-app}

Совершите тестовые покупки в приложении. Через некоторое время в интерфейсе AppMetrica проверьте отчет «Ecommerce». Убедитесь, что ECommerce-события отображаются в отчете.

Подробнее об отчете в разделе [Ecommerce](../../../mobile-reports/ecommerce-report.md).

### Шаг 3. Настройте отправку на основной API key {#send-ecommerce-key}

После успешного тестирования настройте отправку ECommerce-событий на основной API key.

Чтобы отправить объект `ECommerceEvent` на основной API key, используйте метод `AppMetrica.reportECommerce(@NonNull ECommerceEvent event)`.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  // ...
  // Sending an e-commerce event.
  AppMetrica.reportECommerce(ecommerceEvent)
  ```

- Java

  ```java translate=no
  // ...
  // Sending an e-commerce event.
  AppMetrica.reportECommerce(ecommerceEvent);
  ```

{% endlist %}

## Отправка Revenue {#send-revenue}

AppMetrica поддерживает валидацию покупок, которые реализованы с помощью библиотеки [Google Play Billing](https://developer.android.com/google/play/billing/billing_overview). Валидация позволяет фильтровать покупки, которые совершаются из взломанных приложений. Если валидация включена и покупка не проходит валидацию, она не отображается в отчетах.

{% note info %}

 Для валидации покупок на Android используется локальная валидация с помощью публичного ключа. Чтобы включить валидацию, создайте публичный ключ и укажите его в настройках.

 {% endnote %}

### Шаг 1. Настройте отправку Revenue на тестовый API key {#send-revenue-test-key}

В AppMetrica нет возможности сегментировать Revenue на «тестовые» и «не тестовые». Если для отладки покупок вы используете основной API key, то тестовые покупки будут попадать в общую статистику. Поэтому, чтобы отладить отправку Revenue, используйте отправку статистики на дополнительный API key с помощью репортера.

Ниже описаны этапы отправки Revenue на дополнительный API key:

{% cut "С валидацией" %}

  Чтобы покупки на Android валидировались, настройте отправку объекта `Revenue.Receipt` вместе с `Revenue`:

  1. Создайте объект `Revenue.Receipt` с информацией о покупке и подписью. Его необходимо использовать при создании объекта `Revenue` в методе `Revenue.Builder.withReceipt(Revenue.Receipt receipt)`.
  2. Создайте объект `Revenue` с помощью конструктора `Revenue.Builder`.
  3. Отправьте объект `Revenue` на тестовый API key с помощью репортера `IReporter`. Подробнее о работе репортеров в разделе [Отправка статистики на дополнительный API key](#reporter-different-apikey).

  {% list tabs group=instructions %}

  - Kotlin

    ```kotlin translate=no
    fun handlePurchase(purchase: Purchase) {
        // Creating the Revenue.Receipt instance.
        // It is used for checking purchases in Google Play.
        val revenueReceipt = Receipt.newBuilder()
            .withData(purchase.originalJson)
            .withSignature(purchase.signature)
            .build()
        // Creating the Revenue instance.
        val revenue = Revenue.newBuilder(99000000, Currency.getInstance("RUB"))
            .withProductID("io.appmetrica.service.299")
            .withQuantity(2)
            .withReceipt(revenueReceipt)
            .withPayload("""{"source":"Google Play"}""")
            .build()
        // Sending the Revenue instance using reporter.
        AppMetrica.getReporter(applicationContext, "Testing API key").reportRevenue(revenue)
    }
    ```

  - Java

    ```java translate=no
    void handlePurchase(Purchase purchase) {
        // Creating the Revenue.Receipt instance.
        // It is used for checking purchases in Google Play.
        Revenue.Receipt revenueReceipt = Revenue.Receipt.newBuilder()
                .withData(purchase.getOriginalJson())
                .withSignature(purchase.getSignature())
                .build();
        // Creating the Revenue instance.
        Revenue revenue = Revenue.newBuilder(99000000, Currency.getInstance("RUB"))
                .withProductID("io.appmetrica.service.299")
                .withQuantity(2)
                .withReceipt(revenueReceipt)
                .withPayload("{\"source\":\"Google Play\"}")
                .build();
        // Sending the Revenue instance using reporter.
        AppMetrica.getReporter(getApplicationContext(), "Testing API key").reportRevenue(revenue);
    }
    ```

  {% endlist %}

{% endcut %}

{% cut "Без валидации" %}

  Чтобы отправить информацию о покупке без валидации:

  1. Создайте объект `Revenue` с помощью конструктора `Revenue.Builder`.
  2. (Опционально) Чтобы группировать покупки по `OrderID`, укажите его в методе `Revenue.Builder.withPayload(String payload)`.

     {% note info %}

     Если идентификатор `OrderID` не указан, AppMetrica генерирует идентификатор автоматически.

     {% endnote %}

  3. Отправьте объект `Revenue` на тестовый API key с помощью репортера `IReporter`. Подробнее о работе репортеров в разделе [Отправка статистики на дополнительный API key](#reporter-different-apikey).

  {% list tabs group=instructions %}

  - Kotlin

    ```kotlin translate=no
    // Creating the Revenue instance.
    val revenue = Revenue.newBuilder(99000000, Currency.getInstance("RUB"))
        .withProductID("io.appmetrica.service.299")
        .withQuantity(2) // Passing the OrderID parameter in the .withPayload(String payload) method to group purchases.
        .withPayload("""{"OrderID":"Identifier", "source":"Google Play"}""")
        .build()
    // Sending the Revenue instance using reporter.
    AppMetrica.getReporter(applicationContext, "Testing API key").reportRevenue(revenue)
    ```

  - Java

    ```java translate=no
    // Creating the Revenue instance.
    Revenue revenue = Revenue.newBuilder(99000000, Currency.getInstance("RUB"))
            .withProductID("io.appmetrica.service.299")
            .withQuantity(2)
            // Passing the OrderID parameter in the .withPayload(String payload) method to group purchases.
            .withPayload("{\"OrderID\":\"Identifier\", \"source\":\"Google Play\"}")
            .build();
    // Sending the Revenue instance using reporter.
    AppMetrica.getReporter(getApplicationContext(), "Testing API key").reportRevenue(revenue);
    ```

  {% endlist %}

{% endcut %}

### Шаг 2. Проверьте отчет тестового приложения {#send-revenue-test-app}

В интерфейсе AppMetrica проверьте отчет «Revenue». Убедитесь, что количество покупок увеличилось.

Подробнее об отчете в разделе [In-app и Ad Revenue](../../../mobile-reports/revenue-report.md).

### Шаг 3. Настройте отправку Revenue на основной API key {#send-revenue-key}

После успешного тестирования настройте отправку `Revenue` на основной API key.

Чтобы отправить объект `Revenue` на основной API key, используйте метод `AppMetrica.reportRevenue(Revenue revenue)`.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  // ...
  // Sending the Revenue instance.
  AppMetrica.reportRevenue(revenue)
  ```

- Java

  ```java translate=no
  // ...
  // Sending the Revenue instance.
  AppMetrica.reportRevenue(revenue);
  ```

{% endlist %}

## Отправка Ad Revenue {#send-adrevenue}

В AppMetrica реализовано несколько вариантов для отправки Ad Revenue из сервисов рекламной монетизации и медиации:

- [Автоматическая интеграция](#send-adrevenue-automatic-integration). Поддерживается для ironSource.
- [Упрощенная интеграция](#send-adrevenue-simple-integration). Поддерживается для:
     - [Applovin MAX](#send-adrevenue-simple-integration-applovin-max)
     - [Digital Turbine](#send-adrevenue-simple-integration-digital-turbine)
     - [Google AdMob](#send-adrevenue-simple-integration-google-admob)
- [Ручная интеграция/самостоятельная настройка](#send-adrevenue-manual-integration).

### Автоматическая интеграция {#send-adrevenue-automatic-integration}

Данные передаются автоматически. При необходимости автосбор можно отключить.

#### ironSource {#send-adrevenue-automatic-integration-ironsource}

##### Шаг 1. Настройте отправку Ad Revenue {#send-adrevenue-automatic-integration-ironsource-send}

Для ironSource поддержан автоматический сбор Ad Revenue. За это отвечает модуль `io.appmetrica.analytics:analytics-ad-revenue-ironsource-v7`.

{% include notitle [activate](../../_includes/check-reports-ad-revenue-android.md#activate) %}

##### Шаг 2. Убедитесь, что Ad Revenue отображается в отчетах {#send-adrevenue-automatic-integration-ironsource-check-reports}

{% include notitle [check-reports](../../_includes/check-reports-ad-revenue-android.md#check-reports) %}

##### Отключение автосбора Ad Revenue {#send-adrevenue-automatic-integration-ironsource-off}

Если вам необходимо отключить автосбор Ad Revenue, то исключите модуль из списка зависимостей:

{% list tabs %}

- build.gradle.kts

  ```kotlin translate=no
  configurations.configureEach {
      exclude(group = "io.appmetrica.analytics", module = "io.appmetrica.analytics:analytics-ad-revenue-ironsource-v7")
  }
  ```

- build.gradle

  ```groovy translate=no
  configurations.configureEach {
      exclude group: 'io.appmetrica.analytics', module: 'io.appmetrica.analytics:analytics-ad-revenue-ironsource-v7'
  }
  ```

{% endlist %}

### Упрощенная интеграция {#send-adrevenue-simple-integration}

Используйте упрощенный API для отправки данных. Он поддерживает популярные сервисы рекламной монетизации и медиации.

#### Applovin MAX {#send-adrevenue-simple-integration-applovin-max}

##### Шаг 1. Убедитесь, что SDK активирован {#send-adrevenue-simple-integration-applovin-max-active}

{% include notitle [activate](../../_includes/check-reports-ad-revenue-android.md#activate) %}

##### Шаг 2. Настройте отправку Ad Revenue {#send-adrevenue-simple-integration-applovin-max-send}

1. После создания соответствующего рекламного объекта установите `MaxAdRevenueListener`, используя метод `setRevenueListener`.
2. Из метода `onAdRevenuePaid(MaxAd)` отправьте данные в AppMetrica SDK: вызвовите метод `AppMetrica#reportExternalAdRevenue` и передайте в качестве аргументов параметр, переданный в слушатель `MaxAd` и экземпляр `AppLovinSdk`.

   {% list tabs %}

   - App open ad

     {% list tabs group=instructions %}

     - Kotlin

       ```kotlin translate=no
       val maxAppOpenAdView = MaxAppOpenAd( "ad-unit-ID", applicationContext)
       maxAppOpenAdView.setRevenueListener {
           AppMetrica.reportExternalAdRevenue(it, AppLovinSdk.getInstance(applicationContext))
       }
       ```

     - Java

       ```java translate=no
       MaxAppOpenAd maxAppOpenAd = new MaxAppOpenAd( "ad-unit-ID", getApplicationContext());
       maxAppOpenAd.setRevenueListener(maxAdRevenue ->
           AppMetrica.reportExternalAdRevenue(maxAdRevenue, AppLovinSdk.getInstance(getApplicationContext())));
       ```

     {% endlist %}

   - Banner

     {% list tabs group=instructions %}

     - Kotlin

       ```kotlin translate=no
       val maxAdView = MaxAdView("ad-unit-ID", applicationContext)
       maxAdView.setRevenueListener {
           AppMetrica.reportExternalAdRevenue(it, AppLovinSdk.getInstance(applicationContext))
       }
       ```

     - Java

       ```java translate=no
       MaxAdView maxAdView = new MaxAdView("ad-unit-ID", getApplicationContext());
       maxAdView.setRevenueListener(maxAdRevenue ->
           AppMetrica.reportExternalAdRevenue(maxAdRevenue, AppLovinSdk.getInstance(getApplicationContext())));
       ```

     {% endlist %}

   - Interstitial

     {% list tabs group=instructions %}

     - Kotlin

       ```kotlin translate=no
       val maxInterstitialAd = MaxInterstitialAd("ad-unit-ID", applicationContext)
       maxInterstitialAd.setRevenueListener {
           AppMetrica.reportExternalAdRevenue(it, AppLovinSdk.getInstance(applicationContext))
       }
       ```

     - Java

       ```java translate=no
       MaxInterstitialAd maxInterstitialAd = new MaxInterstitialAd("ad-unit-ID", getApplicationContext());
       maxInterstitialAd.setRevenueListener(maxAdRevenue ->
           AppMetrica.reportExternalAdRevenue(maxAdRevenue, AppLovinSdk.getInstance(getApplicationContext())));
       ```

     {% endlist %}

   - Native

     {% list tabs group=instructions %}

     - Kotlin

       ```kotlin translate=no
       val nativeAdLoader = MaxNativeAdLoader("ad-unit-ID", applicationContext)
       nativeAdLoader.setRevenueListener {
           AppMetrica.reportExternalAdRevenue(it, AppLovinSdk.getInstance(applicationContext))
       }
       ```

     - Java

       ```java translate=no
       MaxNativeAdLoader maxNativeAdLoader = new MaxNativeAdLoader("ad-unit-ID", getApplicationContext());
       maxNativeAdLoader.setRevenueListener(maxAdRevenue ->
           AppMetrica.reportExternalAdRevenue(maxAdRevenue, AppLovinSdk.getInstance(getApplicationContext())));
       ```

     {% endlist %}

   - Rewarded

     {% list tabs group=instructions %}

     - Kotlin

       ```kotlin translate=no
       val maxRewardedAd = MaxRewardedAd.getInstance("ad-unit-ID", applicationContext);
       maxRewardedAd.setRevenueListener {
           AppMetrica.reportExternalAdRevenue(it, AppLovinSdk.getInstance(applicationContext))
       }
       ```

     - Java

       ```java translate=no
       MaxRewardedAd maxRewardedAd = MaxRewardedAd.getInstance("ad-unit-ID", getApplicationContext());
       maxRewardedAd.setRevenueListener(maxAdRevenue ->
           AppMetrica.reportExternalAdRevenue(maxAdRevenue, AppLovinSdk.getInstance(getApplicationContext())));
       ```

     {% endlist %}

   {% endlist %}

##### Шаг 3. Убедитесь, что Ad Revenue отображается в отчетах {#send-adrevenue-simple-integration-applovin-max-check-reports}

{% include notitle [check-reports](../../_includes/check-reports-ad-revenue-android.md#check-reports) %}

#### Digital Turbine {#send-adrevenue-simple-integration-digital-turbine}

##### Шаг 1. Убедитесь, что SDK активирован {#send-adrevenue-simple-integration-digital-turbine-active}

{% include notitle [activate](../../_includes/check-reports-ad-revenue-android.md#activate) %}

##### Шаг 2. Настройте отправку Ad Revenue {#send-adrevenue-simple-integration-digital-turbine-send}

1. Для необходимых типов рекламы (`Banner`, `Interstitial`, `Rewarded`) устанавите соответствующий слушатель (`BannerListener`, `InterstitalListener`, `RewardedListener`).
2. Из метода `onShow` слушателя настройте отправку `impressionData` в AppMetrica SDK c помощью метода `AppMetrica#reportExternalAdRevenue()`.

   {% list tabs %}

   - Banner

     {% list tabs group=instructions %}

     - Kotlin

       ```kotlin translate=no
       Banner.setBannerListener(object:BannerListener {
           //....
           override fun onShow(placementId: String, impressionData: ImpressionData) {
               AppMetrica.reportAdRevenue(impressionData)
                   //.....
           }
           //....
       })
       ```

     - Java

       ```java translate=no
       Banner.setBannerListener(new BannerListener() {
           //......
           @Override
           public void onShow(@NonNull String s, @NonNull ImpressionData impressionData) {
               AppMetrica.reportExternalAttribution(impressionData);
               //......
           }
           //......
       });
       ```

     {% endlist %}

   - Interstitial

     {% list tabs group=instructions %}

     - Kotlin

       ```kotlin translate=no
       Interstitial.setInterstitialListener(object:InterstitialListener {
           //....
           override fun onShow(placementId: String, impressionData: ImpressionData) {
               AppMetrica.reportExternalAdRevenue(impressionData)
               //....
           }
       //....
       })
       ```

     - Java

       ```java translate=no
       Interstitial.setInterstitialListener(new InterstitialListener() {
           //......
           @Override
           public void onShow(@NonNull String s, @NonNull ImpressionData impressionData) {
               AppMetrica.reportExternalAdRevenue(impressionData);
               //......
           }
       //.......
       });
       ```

     {% endlist %}

   - Rewarded

     {% list tabs group=instructions %}

     - Kotlin

       ```kotlin translate=no
       Rewarded.setRewardedListener(object:RewardedListener {
           override fun onShow(placementId: String, impressionData: ImpressionData) {
               AppMetrica.reportExternalAdRevenue(impressionData);
               //.......
           }
       })
       ```

     - Java

       ```java translate=no
       Rewarded.setRewardedListener(new RewardedListener() {
           //.....
           @Override
           public void onShow(@NonNull String s, @NonNull ImpressionData impressionData) {
               AppMetrica.reportExternalAdRevenue(impressionData);
               //......
           }
           //.....
       });
       ```

     {% endlist %}

   {% endlist %}

##### Шаг 3. Убедитесь, что Ad Revenue отображается в отчетах {#send-adrevenue-simple-integration-digital-turbine-check-reports}

{% include notitle [check-reports](../../_includes/check-reports-ad-revenue-android.md#check-reports) %}

#### Google AdMob {#send-adrevenue-simple-integration-google-admob}

##### Шаг 1. Убедитесь, что SDK активирован {#send-adrevenue-simple-integration-google-admob-active}

{% include notitle [activate](../../_includes/check-reports-ad-revenue-android.md#activate) %}

##### Шаг 2. Настройте отправку Ad Revenue {#send-adrevenue-simple-integration-google-admob-send}

{% list tabs %}

- App open ad

  1. В методе `AppOpenAdLoadCallback#onAdLoaded` слушателя загрузки рекламы установите слушатель `OnPaidEventListener`.
  2. В методе `OnPaidEventListener#onPaidEvent` настройте отправку данных в AppMetrica с помощью метода `AppMetrica#reportExternalAdRevenue()`, передав в качестве аргументов полученный объект `AdValue` и `AppOpenAd`.

     {% list tabs group=instructions %}

      - Kotlin

        ```kotlin translate=no
        AppOpenAd.load(
            this,
            "ad-unit-ID",
            adRequest,
            AppOpenAd.APP_OPEN_AD_ORIENTATION_PORTRAIT,
            object : AppOpenAdLoadCallback() {
                override fun onAdLoaded(adMobAppOpenAd: AppOpenAd) {
                    super.onAdLoaded(adMobAppOpenAd)
                    adMobAppOpenAd.onPaidEventListener =
                        OnPaidEventListener { adValue ->
                            AppMetrica.reportExternalAdRevenue(
                                adValue,
                                adMobAppOpenAd
                            )
                            //......
                        }
                    //......
                }
        })
        ```

      - Java

        ```java translate=no
        AppOpenAd.load(
            this,
            "ad-unit-ID",
            adRequest,
            AppOpenAd.APP_OPEN_AD_ORIENTATION_PORTRAIT,
            new RewardedInterstitialAdLoadCallback() {
            @Override
            public void onAdLoaded(@NonNull AppOpenAd adMobAppOpenAd) {
                super.onAdLoaded(adMobAppOpenAd);
                adMobAppOpenAd.setOnPaidEventListener(adValue -> {
                    AppMetrica.reportExternalAdRevenue(adValue, adMobAppOpenAd);
                    //......
                });
                //......
            }
        });
        ```

     {% endlist %}

- Banner

  1. После создания `adView` и до загрузки рекламы с помощью вызова `setOnPaidEventListener` зарегистрируйте слушатель `OnPaidEventListener`.
  2. В методе `OnPaidEventListener#onPaidEvent` настройте отправку данных в AppMetrica с помощью метода `AppMetrica#reportExternalAdRevenue()`, передав в качестве аргументов полученный объект `AdValue` и `adView`.

     {% list tabs group=instructions %}

     - Kotlin

       ```kotlin translate=no
       val adMobAdView = AdView(this)
       //........
       adMobAdView.setOnPaidEventListener {
           AppMetrica.reportExternalAdRevenue(it, adMobAdView)
           //.......
       }
       //........
       adMobAdView.loadAd(adRequest)
       ```

     - Java

       ```java translate=no
       AdView adMobAdView = new AdView(this);
       //......
       adMobAdView.setOnPaidEventListener(adValue -> {
           AppMetrica.reportExternalAdRevenue(adValue, adMobAdView);
           //.......
       });
       //.......
       adMobAdView.loadAd(adRequest);
       ```

     {% endlist %}

- Interstitial

  1. В методе `InterstitialAdLoadCallback#onAdLoaded` слушателя загрузки рекламы установите слушатель `OnPaidEventListener`.
  2. В методе `OnPaidEventListener#onPaidEvent` настройте отправку данных в AppMetrica с помощью метода `AppMetrica#reportExternalAdRevenue()`, передав в качестве аргументов полученный объект `AdValue` и `interstitialAd`.

     {% list tabs group=instructions %}

     - Kotlin

       ```kotlin translate=no
       InterstitialAd.load(this, "add-unit-ID", adRequest, object : InterstitialAdLoadCallback() {
           //......
           override fun onAdLoaded(adMobInterstitalAd: InterstitialAd) {
               super.onAdLoaded(adMobInterstitalAd)
               //.......
               adMobInterstitalAd.setOnPaidEventListener { adValue ->
                   AppMetrica.reportExternalAdRevenue(adValue, adMobInterstitalAd)
               }
               //.......
           }
       })
       ```

     - Java

       ```java translate=no
       InterstitialAd.load(this, "ad-unit-ID", adRequest, new InterstitialAdLoadCallback() {
       //........
           @Override
           public void onAdLoaded(@NonNull InterstitialAd adMobInterstitialAd) {
               super.onAdLoaded(adMobInterstitialAd);
               adMobInterstitialAd.setOnPaidEventListener(adValue -> {
                   AppMetrica.reportExternalAdRevenue(adValue, adMobInterstitialAd);
                   //......
               });
               //......
           }
       });
       ```

     {% endlist %}

- Native

  1. В методе `OnNativeAdLoadedListener#onNativeAdLoaded` слушателя загрузки рекламы установите слушатель `OnPaidEventListener`.
  2. В методе `OnPaidEventListener#onPaidEvent` настройте отправку данных в AppMetrica с помощью метода `AppMetrica#reportExternalAdRevenue()`, передав в качестве аргументов полученный объект `AdValue` и `nativeAd`.

     {% list tabs group=instructions %}

     - Kotlin

       ```kotlin translate=no
       val adMobAdLoader = AdLoader.Builder(this, "add-unit-ID")
           .forNativeAd { adMobNativeAd ->
              adMobNativeAd.setOnPaidEventListener { adValue ->
                   AppMetrica.reportExternalAdRevenue(adValue, adMobNativeAd)
               }
           }
           //.......
           .build()
       //.....
       ```

     - Java

       ```java translate=no
       //.....
       AdLoader admobLoader = new AdLoader.Builder(this, "ad-unit-ID")
           .forNativeAd(adMobNativeAd -> {
               adMobNativeAd.setOnPaidEventListener(adValue -> {
                   AppMetrica.reportExternalAdRevenue(adValue, adMobNativeAd);
                   //......
               });
           //......
           })
           .build();
       //......
       ```

     {% endlist %}

- Rewarded

  1. В методе `RewardedAdLoadCallback#onAdLoaded` слушателя загрузки рекламы установите слушатель `OnPaidEventListener`.
  2. В методе `OnPaidEventListener#onPaidEvent` настройте отправку данных в AppMetrica с помощью метода `AppMetrica#reportExternalAdRevenue()`, передав в качестве аргументов полученный объект `AdValue` и `rewardedAd`.

     {% list tabs group=instructions %}

     - Kotlin

       ```kotlin translate=no
       //.....
       RewardedAd.load(this, "ad-unit-ID", adRequest, object : RewardedAdLoadCallback() {
           override fun onAdLoaded(rewardedAd: RewardedAd) {
               super.onAdLoaded(rewardedAd)
               //.....
               rewardedAd.onPaidEventListener = OnPaidEventListener { adValue ->
                   AppMetrica.reportExternalAdRevenue(
                       adValue,
                       rewardedAd
                   )
               }
           }
       })
       //.....
       ```

     - Java

       ```java translate=no
       //.....
       RewardedAd.load(this, "ad-unit-ID", adRequest, new RewardedAdLoadCallback() {
           @Override
           public void onAdLoaded(@NonNull RewardedAd rewardedAd) {
               super.onAdLoaded(rewardedAd);
               //.....
               rewardedAd.setOnPaidEventListener(adValue -> {
                   AppMetrica.reportExternalAdRevenue(adValue, rewardedAd);
                   //........
               });
           }
       });
       //.....
       ```

     {% endlist %}

- Rewarded interstitial

  1. В методе `RewardedInterstitialAdLoadCallback#onAdLoaded` слушателя загрузки рекламы установите слушатель `OnPaidEventListener`.
  2. В методе `OnPaidEventListener#onPaidEvent` настройте отправку данных в AppMetrica с помощью метода `AppMetrica#reportExternalAdRevenue()`, передав в качестве аргументов полученный объект `AdValue` и `rewardedInterstitialAd`.

     {% list tabs group=instructions %}

     - Kotlin

       ```kotlin translate=no
       RewardedInterstitialAd.load(
           this,
           "ad-unit-ID",
           adRequest,
           object : RewardedInterstitialAdLoadCallback() {
               override fun onAdLoaded(rewardedInterstitialAd: RewardedInterstitialAd) {
                   super.onAdLoaded(rewardedInterstitialAd)
                   rewardedInterstitialAd.onPaidEventListener =
                       OnPaidEventListener { adValue ->
                           AppMetrica.reportExternalAdRevenue(
                               adValue,
                               rewardedInterstitialAd
                           )
                           //......
                       }
                   //......
               }
       })
       ```

     - Java

       ```java translate=no
       RewardedInterstitialAd.load(this, "ad-unit-ID", adRequest, new RewardedInterstitialAdLoadCallback() {
           @Override
           public void onAdLoaded(@NonNull RewardedInterstitialAd rewardedInterstitialAd) {
               super.onAdLoaded(rewardedInterstitialAd);
               rewardedInterstitialAd.setOnPaidEventListener(adValue -> {
                   AppMetrica.reportExternalAdRevenue(adValue, rewardedInterstitialAd);
                   //......
               });
               //......
           }
       });
       ```

     {% endlist %}

{% endlist %}

##### Шаг 3. Убедитесь, что Ad Revenue отображается в отчетах {#send-adrevenue-simple-integration-google-admob-check-reports}

{% include notitle [check-reports](../../_includes/check-reports-ad-revenue-android.md#check-reports) %}

### Ручная интеграция/самостоятельная настройка {#send-adrevenue-manual-integration}

Используйте этот вариант, чтобы самостоятельно настроить передачу данных любого другого сервиса рекламной монетизации, который предоставляет Impression level Revenue Data.

#### Шаг 1. Убедитесь, что SDK активирован {#send-adrevenue-manual-integration-active}

{% include notitle [activate](../../_includes/check-reports-ad-revenue-android.md#activate) %}

#### Шаг 2. Настройте отправку Ad Revenue {#send-adrevenue-manual-integration-send}

1. Создайте объект `AdRevenue` с помощью конструктора `AdRevenue.Builder`.

    ```java translate=no
    Map<String, String> adRevenuePayload = new HashMap<>();
    adRevenuePayload.put("payload_key_1", "payload_value_1");
    adRevenuePayload.put("payload_key_2", "payload_value_2");
    AdRevenue adRevenue = AdRevenue.newBuilder(new BigDecimal("100.100"), Currency.getInstance("USD"))
    .withAdNetwork("ad_network")
    .withAdPlacementId("ad_placement_id")
    .withAdPlacementName("ad_placement_name")
    .withAdType(AdType.NATIVE)
    .withAdUnitId("ad_unit_id")
    .withAdUnitName("ad_unit_name")
    .withPrecision("some precision")
    .withPayload(adRevenuePayload)
    .build();
    ```

2. Отправьте объект `Ad Revenue` с помощью метода `AppMetrica.reportAdRevenue(AdRevenue adRevenue)`.

    ```java translate=no
    AppMetrica.reportAdRevenue(adRevenue);
    ```

#### Шаг 3. Убедитесь, что Ad Revenue отображается в отчетах {#send-adrevenue-manual-integration-check-reports}

{% include notitle [check-reports](../../_includes/check-reports-ad-revenue-android.md#check-reports) %}

## Установка длительности тайм-аута сессии {#session-timeout}

По умолчанию длительность таймаута сессии равна 10 секундам. Это минимально допустимое значение параметра `sessionTimeout`.

Чтобы изменить длительность таймаута, передайте значение в секундах в метод `withSessionTimeout(int sessionTimeout)` при создании расширенной конфигурации библиотеки.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  // Creating an extended library configuration.
  val config = AppMetricaConfig.newConfigBuilder(API_KEY)
      // Setting the length of the session timeout.
      .withSessionTimeout(15)
      .build()
  // Initializing the AppMetrica SDK.
  AppMetrica.activate(applicationContext, config)
  ```

- Java

  ```java translate=no
  // Creating an extended library configuration.
  AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_KEY)
          // Setting the length of the session timeout.
          .withSessionTimeout(15)
          .build();
  // Initializing the AppMetrica SDK.
  AppMetrica.activate(getApplicationContext(), config);
  ```

{% endlist %}

## Установка версии приложения {#version-app}

По умолчанию версия приложения задается в файле [build.gradle](https://developer.android.com/studio/publish/versioning).

Чтобы указать версию приложения из кода, передайте версию приложения в метод `withAppVersion(String appVersion)` при создании расширенной конфигурации библиотеки.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  // Creating an extended library configuration.
  val config = AppMetricaConfig.newConfigBuilder(API_KEY)
      // Setting the app version.
      .withAppVersion("1.13.2")
      .build()
  // Initializing the AppMetrica SDK.
  AppMetrica.activate(applicationContext, config)
  ```

- Java

  ```java translate=no
  // Creating an extended library configuration.
  AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_KEY)
          // Setting the app version.
          .withAppVersion("1.13.2")
          .build();
  // Initializing the AppMetrica SDK.
  AppMetrica.activate(getApplicationContext(), config);
  ```

{% endlist %}

где `1.13.2` — версия приложения.

## Определение уровня API библиотеки (Android) {#level-api-android}

Чтобы определить уровень API библиотеки из кода приложения, используйте метод `AppMetrica.getLibraryApiLevel()`.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  val libraryApiLevel = AppMetrica.getLibraryApiLevel()
  ```

- Java

  ```java translate=no
  int libraryApiLevel = AppMetrica.getLibraryApiLevel();
  ```

{% endlist %}

## Определение версии библиотеки {#version-sdk}

Чтобы определить версию библиотеки из кода приложения, используйте метод `AppMetrica.getLibraryVersion()`.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  val libraryVersion = AppMetrica.getLibraryVersion()
  ```

- Java

  ```java translate=no
  String libraryVersion = AppMetrica.getLibraryVersion();
  ```

{% endlist %}

## Отслеживание источников установки {#source}

Отслеживание источников установок в AppMetrica SDK работает по умолчанию.

## Отслеживание открытий приложения с помощью deeplink {#deeplink}

Чтобы отслеживать открытия приложения с помощью deeplink, необходимо добавить изменения в Activity, которая обрабатывает deeplink. Отслеживание открытий необходимо для корректного трекинга ремаркетинг-кампаний.

{% note tip %}

 Для работы с deeplink [поддержите их](https://developer.android.com/training/app-links/deep-linking#adding-filters) в вашем приложении.

{% endnote %}

Отслеживание открытий осуществляется с помощью метода `reportAppOpen()`:

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  class DeeplinkActivity : Activity() {
      override fun onCreate(savedInstanceState: Bundle?) {
          super.onCreate(savedInstanceState)
          if (savedInstanceState == null) {
              AppMetrica.reportAppOpen(this)
          }
      }

      override fun onNewIntent(intent: Intent) {
          super.onNewIntent(intent)
          AppMetrica.reportAppOpen(intent)
      }
  }
  ```

- Java

  ```java translate=no
  public class DeeplinkActivity extends Activity {
      @Override
      protected void onCreate(@Nullable final Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          if (savedInstanceState == null) {
              AppMetrica.reportAppOpen(this);
          }
      }

      @Override
      protected void onNewIntent(final Intent intent) {
          super.onNewIntent(intent);
          AppMetrica.reportAppOpen(intent);
      }
  }
  ```

{% endlist %}

{% note info %}

На Android можно поддержать открытие [отложенного deeplink](android-deferred-deeplinks.md).

{% endnote %}

См. также [Как создать ремаркетинг-кампанию в AppMetrica](../../../troubleshooting/troubleshooting.md#remarketing-campaign).

## Запрос отложенного deeplink {#deferreddeeplink-request}

Чтобы запросить отложенный deeplink, передайте в метод `AppMetrica.requestDeferredDeeplink(DeferredDeeplinkListener listener)` объект класса, реализующий интерфейс `DeferredDeeplinkListener`. Метод возвращает отложенный deeplink только при первом запуске приложения после получения Google Play Install Referrer.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  AppMetrica.requestDeferredDeeplink(object : DeferredDeeplinkListener {
      override fun onDeeplinkLoaded(deeplink: String) {
          Log.i("Deeplink", "deeplink = $deeplink")
      }

      override fun onError(error: DeferredDeeplinkListener.Error, referrer: String?) {
          Log.i("Deeplink", "Error: ${error.description}, unparsed referrer: $referrer")
      }
  })
  ```

- Java

  ```java translate=no
  AppMetrica.requestDeferredDeeplink(new DeferredDeeplinkListener() {
      @Override
      public void onDeeplinkLoaded(@NotNull String deeplink) {
          Log.i("Deeplink", "deeplink = " + deeplink);
      }

      @Override
      public void onError(@NotNull Error error, @Nullable String referrer) {
          Log.i("Deeplink", "Error: " + error.getDescription() + ", unparsed referrer: " + referrer);
      }
  });
  ```

{% endlist %}

Подробнее об отложенных deeplinks в разделе [Поддержка отложенных deeplinks](android-deferred-deeplinks.md).

## Запрос параметров отложенного deeplink {#deferreddeeplink-parameters-request}

Чтобы запросить параметры отложенного deeplink, передайте в метод `AppMetrica.requestDeferredDeeplinkParameters(DeferredDeeplinkParametersListener listener)` объект класса, реализующий интерфейс `DeferredDeeplinkParametersListener`. Метод возвращает параметры отложенного deeplink только при первом запуске приложения после получения Google Play Install Referrer.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  AppMetrica.requestDeferredDeeplinkParameters(object : DeferredDeeplinkParametersListener {
      override fun onParametersLoaded(parameters: Map<String, String>) {
          // Processing deeplink parameters.
          for (key in parameters.keys) {
              Log.i("Deeplink params", "key: $key value: ${parameters[key]}")
          }
      }

      override fun onError(error: DeferredDeeplinkParametersListener.Error, referrer: String) {
          // Handling the error.
          Log.e("Error!", error.description)
      }
  })
  ```

- Java

  ```java translate=no
  AppMetrica.requestDeferredDeeplinkParameters(new DeferredDeeplinkParametersListener() {
      @Override
      public void onParametersLoaded(@NotNull Map<String, String> parameters) {
          // Processing deeplink parameters.
          for (String key : parameters.keySet()) {
              Log.i("Deeplink params", "key: " + key + " value: " + parameters.get(key));
          }
      }

      @Override
      public void onError(@NotNull Error error, @NotNull String referrer) {
          // Handling the error.
          Log.e("Error!", error.getDescription());
      }
  });
  ```

{% endlist %}

Подробнее об отложенных deeplinks в разделе [Поддержка отложенных deeplinks](android-deferred-deeplinks.md).

## Учет новых пользователей {#new-user}

По умолчанию в момент первого запуска приложения все пользователи определяются как новые. Если AppMetrica SDK подключается к приложению, у которого уже есть активные пользователи, то для корректного отслеживания статистики можно настроить учет новых и старых пользователей. Для этого необходимо инициализировать AppMetrica SDK, используя расширенную стартовую конфигурацию `AppMetricaConfig`:

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  var isFirstLaunch: Boolean = false
  // Implement logic to detect whether the app is opening for the first time.
  // For example, you can check for files (settings, databases, and so on),
  // which the app creates on its first launch.
  if (conditions) {
      isFirstLaunch = true
  }
  // Creating an extended library configuration.
  val config = AppMetricaConfig.newConfigBuilder(API_KEY)
      .handleFirstActivationAsUpdate(!isFirstLaunch)
      .build()
  // Initializing the AppMetrica SDK.
  AppMetrica.activate(applicationContext, config)
  ```

- Java

  ```java translate=no
  boolean isFirstLaunch = false;
  // Implement logic to detect whether the app is opening for the first time.
  // For example, you can check for files (settings, databases, and so on),
  // which the app creates on its first launch.
  if (conditions) {
      isFirstLaunch = true;
  }
  // Creating an extended library configuration.
  AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_KEY)
          .handleFirstActivationAsUpdate(!isFirstLaunch)
          .build();
  // Initializing the AppMetrica SDK.
  AppMetrica.activate(getApplicationContext(), config);
  ```

{% endlist %}

## Отключение и включение отправки статистики {#stat}

Если для отправки статистических данных требуется согласие пользователя, необходимо инициализировать библиотеку с отключенной опцией отправки статистики. Для этого передайте значение `false` в метод `withDataSendingEnabled(boolean value)` при создании расширенной конфигурации библиотеки.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  // Creating an extended library configuration.
  val config = AppMetricaConfig.newConfigBuilder(API_KEY)
  // Disabling sending data.
      .withDataSendingEnabled(false)
      .build()
  // Initializing the AppMetrica SDK.
  AppMetrica.activate(applicationContext, config)
  ```

- Java

  ```java translate=no
  // Creating an extended library configuration.
  AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_KEY)
          // Disabling sending data.
          .withDataSendingEnabled(false)
          .build();
  // Initializing the AppMetrica SDK.
  AppMetrica.activate(getApplicationContext(), config);
  ```

{% endlist %}

После того как пользователь дал согласие на отправку статистики (например, в настройках приложения или в соглашении при первом открытии), включите отправку статистики с помощью метода `AppMetrica.setDataSendingEnabled(true)`:

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  // Checking the status of the boolean variable. It shows the user confirmation.
  if (flag) {
      // Enabling sending data.
      AppMetrica.setDataSendingEnabled(true)
  }
  ```

- Java

  ```java translate=no
  // Checking the status of the boolean variable. It shows the user confirmation.
  if (flag) {
      // Enabling sending data.
      AppMetrica.setDataSendingEnabled(true);
  }
  ```

{% endlist %}

### Пример оповещения {#stat-alert-example}

Для информирования пользователей вы можете использовать любой текст. Например:

Это приложение использует сервис аналитики AppMetrica, предоставляемый компанией ООО «ЯНДЕКС», 119021, Россия,Москва, ул. Л. Толстого, 16 (далее — Яндекс) на [Условиях использования сервиса](https://yandex.ru/legal/metrica_termsofuse/).

AppMetrica анализирует данные об использовании приложения, в том числе об устройстве, на котором оно функционирует, источнике установки, составляет конверсию и статистику вашей активности в целях продуктовой аналитики, анализа и оптимизации рекламных кампаний, а также для устранения ошибок. Собранная таким образом информация не может идентифицировать вас.

Информация об использовании вами данного приложения, собранная при помощи инструментов AppMetrica, в обезличенном виде будет передаваться Яндексу и храниться на сервере Яндекса в ЕС и Российской Федерации. Яндекс будет обрабатывать эту информацию для предоставления статистики использования вами приложения, составления для нас отчетов о работе приложения, и предоставления других услуг.

## Получение различных идентификаторов AppMetrica SDK {#get-ids}

Чтобы получить различные идентификаторы AppMetrica SDK (`DeviceId`, `DeviceIdHash`, `UUID`) используйте метод `requestStartupParams()`. Для получения `appmetrica_device_id` нужно запрашивать `DeviceIdHash`.

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
      listOf(
          StartupParamsCallback.APPMETRICA_UUID,
          StartupParamsCallback.APPMETRICA_DEVICE_ID,
          StartupParamsCallback.APPMETRICA_DEVICE_ID_HASH
      )
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
          Arrays.asList(
                  StartupParamsCallback.APPMETRICA_DEVICE_ID,
                  StartupParamsCallback.APPMETRICA_DEVICE_ID_HASH,
                  StartupParamsCallback.APPMETRICA_UUID
          )
  );
  ```

{% endlist %}

## Передача типа устройства {#device-type}

Если вы хотите задать тип устройства, укажите его при создании конфигурации:

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  class YourApplication : Application() {
      override fun onCreate() {
          super.onCreate()
          // Creating an extended library configuration.
          val config = AppMetricaConfig.newConfigBuilder(API_KEY)
              // Defining the device type
              .withDeviceType(PredefinedDeviceTypes.TABLET)
              // ...
              .build()
          // Initializing the AppMetrica SDK.
          AppMetrica.activate(applicationContext, config)
          // Automatic tracking of user activity.
          AppMetrica.enableActivityAutoTracking(this)
      }
  }
  ```

- Java

  ```java translate=no
  public class YourApplication extends Application {
     @Override
     public void onCreate() {
        super.onCreate();
        // Creating an extended library configuration.
        AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_KEY)
                // Defining the device type
                .withDeviceType(PredefinedDeviceTypes.TABLET)
                // ...
                .build();
        // Initializing the AppMetrica SDK.
        AppMetrica.activate(getApplicationContext(), config);
        // Automatic tracking of user activity.
        AppMetrica.enableActivityAutoTracking(this);
     }
  }
  ```

{% endlist %}

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
