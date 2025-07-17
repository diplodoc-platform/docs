# Миграция на версию 6.0.0

При миграции приложения с `com.yandex.android:mobmetricalib` на `io.appmetrica.analytics:analytics` будут сохранены основные идентификаторы и данные, то есть процесс перехода на новую версию не должен вызвать проблем и аномалий в отчетах.

## Одновременное использование двух версий AppMetrica SDK

Переименованы группа и названия основных артефактов, поэтому в одном приложении могут использоваться сразу две версии AppMetrica SDK: `com.yandex.android:mobmetricalib` и `io.appmetrica.analytics:analytics`. Это может произойти в некоторых случаях.

### 1. Среди зависимостей приложения будут прописаны зависимости сразу от двух разных версий AppMetrica SDK

{% note alert %}

Категорически не рекомендуется одновременная работа в коде приложения с `com.yandex.android:mobmetricalib` и `io.appmetrica.analytics:analytics` с одним `API_KEY`. То есть нельзя одновремено активировать `YandexMetrica` и `AppMetrica` с одним `API_KEY`. Это не приведет к сбоям и крешам в приложении, но вызовет искажение и нарушение статистики. При миграции на `io.appmetrica.analytics:analytics` проверьте, что среди зависимостей приложения нет зависимости от `com.yandex.android:mobmetricalib`, а в коде приложения отсутствуют импорты классов из пакета `com.yandex.metrica`.

{% endnote %}

### 2. Одна из зависимостей приложения будет транзитивно затягивать зависимость от AppMetrica SDK

Если приложение и библиотеки используют разные API_KEY, данная ситуация является возможной, но нежелательной. Статистика должна собираться нормально, хотя допустимы небольшие отклонения. В этом случае возможно некоторое увеличение размера приложения, так как в составе приложения AppMetrica будут присутствовать два SDK, вместо одного.

### Совместимость AppMetrica SDK и AppMetrica Push SDK

При поднятии версии AppMetrica SDK до 6.0.0 рекомендуется использовать **AppMetrica Push SDK 2.3.3**, которая имеет поддержку и `com.yandex.android:mobmetricalib`, и `io.appmetrica.analytics:analytics`.

## Руководство по миграции

Руководство содержит примеры, демонстрирующие различия между версиями SDK версий `5.3.0` и `6.0.0`. В разделе рассматриваются только те методы, в которых нарушена обратная совместимость.

Для миграции на новую версию выполните следующие шаги:

1. Поменяйте зависимость `com.yandex.android:mobmetricalib:5.3.0` на `io.appmetrica.analytics:analytics:6.0.0`.
2. В коде проекта замените те классы и методы, которые были просто переименованы или поменяли только пакет. Необходимые изменения указаны в [разделе про переименование классов](#rename-classes).
3. Код с остальными ошибками временно закомментируйте, чтобы проект можно было собрать.
4. Убедитесь, что используется только новая версия AppMetrica с помощью [инструкции в соответствующем разделе](#check).
5. Если используется плагин из `com.yandex.android:appmetrica-build-plugin`, обновите его версию до указанной в соответствующем [разделе](#crash-plugin).
6. Поменяйте exclude правила, если они имелись. Необходимые изменения указаны в [разделе про переименование зависимостей](#dependencies).
7. Исправьте закомментированный код, используя остальные пункты данной инструкции. При возникновении вопросов напишите в [поддержку](../../../troubleshooting/feedback-new.md).

### Переименованные классы {#rename-classes}

* Пакет `com.yandex.metrica` заменен на `io.appmetrica.analytics`.
* Пакет `com.google.protobuf.nano.ym` заменен на `io.appmetrica.analytics.protobuf.nano` в проекте `analytics-proto`.
* Класс `YandexMetrica` переименован в `AppMetrica`.
   * `reportNativeCrash` удален.
   * `requestAppMetricaDeviceID` удален. Используйте `requestStartupParams`.
   * `setStatisticsSending` переименован в `setDataSendingEnabled`.
   * `setLocationTracking(Context, boolean)` удален. Используйте `setLocationTracking(boolean)`.
* Класс `YandexMetricaConfig` переименован в `AppMetricaConfig`.
   * `Builder#withStatisticsSending` переменован в `Builder#withDataSendingEnabled`.
* Класс `YandexMetricaDefaultValues` переименован в `AppMetricaDefaultValues`.
* Класс `MetricaService` переименован в `AppMetricaService`.
* Класс `IMetricaService` переименован в `IAppMetricaService`.
* Класс `YandexMetricaPlugins` переименован в `AppMetricaPlugins`.
* Интерфейс `IReporter`
   * `setStatisticsSending` переименован в `setDataSendingEnabled`.
* Интерфейс `ReporterConfig`
   * `Builder#withStatisticsSending` переменован в `Builder#withDataSendingEnabled`.

### Переименованные зависимости {#dependencies}

* Модуль `com.yandex.android:mobmetricalib-ndk-crashes` переименован в `io.appmetrica.analytics:analytics-ndk-crashes`. Поддерживается только версия 3.0.0 и выше.
* Модуль `com.yandex.android:mobmetricalib-identifiers` переименован в `io.appmetrica.analytics:analytics-identifiers`.

## Как убедиться, что используется только новая версия {#check}

Так как название библиотеки было изменено, возможен вариант, когда будет одновременно использоваться и старая, и новая AppMetrica. Это может привести к странному поведению. Для исключения таких случаев убедитесь, что старая AppMetrica не используется в приложении.

Проверить, что в проекте не используется зависимость от `com.yandex.android:mobmetricalib` можно, используя команду:

```
./gradlew :app:dependencies
```

Эта команда выведет зависимости всех вариантов сборки приложения. После этого необходимо посмотреть где используется `com.yandex.android:mobmetricalib` и заменить на новую зависимость.

Если все сделано правильно, то будет пустой ответ после вызова команды:

```
./gradlew app:dependencies | grep com.yandex.android:mobmetricalib
```

## Совместимость с версиями AppMetrica Gradle Plugin {#crash-plugin}

{% note warning %}

Плагин поменял название артефакта.

{% endnote %}

Для корректной работы десимволикации крэшей необходимо использовать AppMetrica Gradle Plugin версии не ниже `io.appmetrica.analytics:gradle:0.8.2`.

## Исключение зависимостей {#exclude}

### Интеграция библиотеки для получения рекламных идентификаторов

Для получения рекламных идентификаторов AppMetrica SDK использует отдельную библиотеку `io.appmetrica.analytics:analytics-identifiers`. Эта библиотека содержит зависимость от `com.google.android.gms:play-services-ads-identifier:18.0.1`, которая используется для получения GAID. Версия библиотеки `io.appmetrica.analytics:analytics-identifiers` должна соответствовать версии библиотеки `io.appmetrica.analytics:analytics`.

Эта зависимость добавляется по умолчанию.

Если получение рекламных идентификаторов нежелательно (например, для детских приложений), исключите библиотеку в файле `build.gradle` проекта:

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

### Интеграция библиотеки для получения локации

Для получения локации AppMetrica SDK использует отдельную библиотеку `io.appmetrica.analytics:analytics-location`. Эта библиотека содержит зависимость от `com.google.android.gms:play-services-location:19.0.1`, которая используется для получения локации. Версия библиотеки `io.appmetrica.analytics:analytics-location` должна соответствовать версии библиотеки `io.appmetrica.analytics:analytics`.

Эта зависимость добавляется по умолчанию.

Если получение локации нежелательно, исключите библиотеку в файле `build.gradle` проекта:

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

## Миграция метода requestAppMetricaDeviceID

Метод `YandexMetrica.requestAppMetricaDeviceID` был удален. Вместо него используйте метод `AppMetrica.requestStartupParams`.

{% note warning %}

Запрашивать нужно именно ключ `StartupParamsCallback.APPMETRICA_DEVICE_ID_HASH`, а не `StartupParamsCallback.APPMETRICA_DEVICE_ID`, так как по ключу `StartupParamsCallback.APPMETRICA_DEVICE_ID` вернется иной идентификатор.

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

## Удаление deprecated метода Revenue#newBuilder(double, Currency)

- Метод `Revenue#newBuilder(double, Currency)` был `@deprecated` и теперь удален. Вместо него стоит использовать `Revenue#newBuilder(int, Currency)`, где `int` - предполагает использование `revenueMicros`.
- Метод `Revenue#newBuilderWithMicros(int, Currency)` был переименован в `Revenue#newBuilder(int, Currency)`.

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
