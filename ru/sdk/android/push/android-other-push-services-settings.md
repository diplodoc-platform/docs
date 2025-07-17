# Использование с другими push-сервисами

AppMetrica Push SDK можно использовать одновременно с другими push-сервисами. Для этого необходимо создать свой push-сервис для FCM или HMS, который будет перенаправлять сообщения между интегрированными SDK.

## Использование с другими Firebase push-сервисами {#fcm}

### Шаг 1. Внесите изменения в AndroidManifest.xml {#fcm-settings}

Внесите изменения в элемент `application` файла `AndroidManifest.xml`:

```xml translate=no
<service android:name=".FirebaseMessagingMainService"
         android:enabled="true"
         android:exported="false">
    <intent-filter android:priority="100">
        <action android:name="com.google.firebase.MESSAGING_EVENT"/>
    </intent-filter>
</service>
<service android:name="io.appmetrica.analytics.push.provider.firebase.AppMetricaMessagingService" tools:node="remove"/>
```

### Шаг 2. Добавьте в проект зависимость {#dependencies}

{% list tabs %}

- app/build.gradle.kts

  ```kotlin translate=no
  dependencies {
      implementation("io.appmetrica.analytics:push-provider-firebase:$appmetrica_push_version")
  }
  ```
- app/build.gradle

  ```groovy translate=no
  dependencies {
      implementation "io.appmetrica.analytics:push-provider-firebase:$appmetrica_push_version"
  }
  ```

{% endlist %}

### Шаг 3. Добавьте обработку push-уведомлений {#handling}

Объявите производный класс `FirebaseMessagingMainService` от базового `FirebaseMessagingService` для обработки push-уведомлений:

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  class FirebaseMessagingMainService : FirebaseMessagingService() {
      override fun onMessageReceived(message: RemoteMessage) {
          super.onMessageReceived(message)
          if (AppMetricaMessagingService.isNotificationRelatedToSDK(message)) {
              AppMetricaMessagingService().processPush(this, message)
              return
          }

          // Implement the logic for sending messages to other SDKs or handle own pushes.
      }
  }
  ```
- Java

  ```java translate=no
  public class FirebaseMessagingMainService extends FirebaseMessagingService {
      @Override
      public void onMessageReceived(RemoteMessage message) {
          super.onMessageReceived(message);
          if (AppMetricaMessagingService.isNotificationRelatedToSDK(message)) {
              new AppMetricaMessagingService().processPush(this, message);
              return;
          }

          // Implement the logic for sending messages to other SDKs or handle own pushes.
      }
  }
  ```

{% endlist %}

### Шаг 4. Добавьте обработку push-токенов {#tokens}

Дополните код класса `FirebaseMessagingMainService` для обработки push-токенов:

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  class FirebaseMessagingMainService : FirebaseMessagingService() {
      override fun onNewToken(token: String) {
          super.onNewToken(token);
          AppMetricaMessagingService().processToken(this, token)

          // Implement the logic for sending tokens to other SDKs.
      }
  }
  ```

- Java

  ```java translate=no
  public class FirebaseMessagingMainService extends FirebaseMessagingService {
      @Override
      public void onNewToken(@NonNull String token) {
          super.onNewToken(token);
          new AppMetricaMessagingService().processToken(this, token);

          // Implement the logic for sending tokens to other SDKs.
      }
  }
  ```

{% endlist %}

## Использование с другими HMS push-сервисами {#hms}

### Шаг 1. Внесите изменения в AndroidManifest.xml {#hms-settings}

Внесите изменения в элемент `application` файла `AndroidManifest.xml`:

```xml translate=no
<service
    android:name=".HmsMessagingMainService"
    android:exported="true"
    android:permission="${applicationId}.permission.PROCESS_PUSH_MSG">
    <intent-filter android:priority="100">
        <action android:name="com.huawei.push.action.MESSAGING_EVENT" />
    </intent-filter>
</service>
<service android:name="io.appmetrica.analytics.push.provider.hms.AppMetricaHmsMessagingService" tools:node="remove"/>
```

### Шаг 2. Добавьте обработку push-уведомлений {#hms-handling}

Объявите производный класс `HmsMessagingMainService` от базового `HmsMessageService` для обработки push-уведомлений:

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  class HmsMessagingMainService : HmsMessageService() {
      override fun onMessageReceived(message: RemoteMessage) {
          super.onMessageReceived(message)
          if (AppMetricaHmsMessagingService.isNotificationRelatedToSDK(message) {
              AppMetricaHmsMessagingService().processPush(this, message)
              return
          }

          // Implement the logic for sending messages to other SDKs or handle own pushes.
      }
  }
  ```

- Java

  ```java translate=no
  public class HmsMessagingMainService extends HmsMessageService {
      @Override
      public void onMessageReceived(RemoteMessage message) {
          super.onMessageReceived(message);
          if (AppMetricaHmsMessagingService.isNotificationRelatedToSDK(message) {
              new AppMetricaHmsMessagingService().processPush(this, message);
              return;
          }

          // Implement the logic for sending messages to other SDKs or handle own pushes.
      }
  }
  ```

{% endlist %}

### Шаг 3. Добавьте обработку push-токенов {#hms-tokens}

Дополните код класса `HmsMessagingMainService` для обработки push-токенов:

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  class HmsMessagingMainService : HmsMessageService() {
      override fun onNewToken(token: String?) {
          super.onNewToken(token);
          AppMetricaHmsMessagingService().processToken(this, token)

          // Implement the logic for sending tokens to other SDKs.
      }
  }
  ```

- Java

  ```java translate=no
  public class HmsMessagingMainService extends HmsMessageService {
      @Override
      public void onNewToken(@Nullable String token) {
          super.onNewToken(token);
          new AppMetricaHmsMessagingService().processToken(this, token);

          // Implement the logic for sending tokens to other SDKs.
      }
  }
  ```

{% endlist %}

#### См. также

- [Подключение и инициализация AppMetrica Push SDK](quick-start.md)
- [Запуск push-кампании](../../../push/marketing.md)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
