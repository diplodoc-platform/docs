# Подключение и инициализация

Push SDK под Android предоставляется в виде библиотеки в формате AAR.
Библиотека доступна в [Maven-репозитории](https://search.maven.org/search?q=g:io.appmetrica.analytics%20AND%20a:push).

Ниже описаны этапы подключения и инициализации AppMetrica Push SDK:

## Шаг 1. Подготовьте приложение {#preparation}

Перед подключением библиотеки AppMetrica Push SDK, подготовьте ваше приложение:

1. [Подключите основную библиотеку AppMetrica SDK](../analytics/quick-start.md) не ниже версии 6.0.0.
2. [Настройте приложение](android-settings.md) для отправки push-уведомлений.

## Шаг 2. Подключите библиотеку {#installation}

Push SDK использует библиотеку [OKHttp](https://github.com/square/okhttp) для кэширования изображений, которые показываются в push-уведомлениях.
Правила кэширования берутся из HTTP-заголовка `cache-control`.
Если вы не хотите, чтобы изображения кэшировались, подключите библиотеку без кэширования.

1. Если вы используете Gradle для сборки приложения, добавьте следующую зависимость в Gradle файл приложения:

   {% cut "С кэшированием" %}

     {% list tabs %}

     - build.gradle.kts

       ```kotlin translate=no
       dependencies {
           // AppMetrica Push SDK.
           implementation("io.appmetrica.analytics:push:{{ push-sdk-android-version }}")
           implementation("androidx.legacy:legacy-support-v4:1.0.0")
       }
       ```

     - build.gradle

       ```groovy translate=no
       dependencies {
           // AppMetrica Push SDK.
           implementation "io.appmetrica.analytics:push:{{ push-sdk-android-version }}"
           implementation "androidx.legacy:legacy-support-v4:1.0.0"
       }
       ```

     {% endlist %}

   {% endcut %}

   {% cut "Без кэширования" %}

     {% list tabs %}

     - build.gradle.kts

       ```kotlin translate=no
       dependencies {
           // AppMetrica Push SDK.
           implementation("io.appmetrica.analytics:push:{{ push-sdk-android-version }}") {
             exclude(group = "com.squareup.okhttp3", module = "okhttp")
           }
           implementation("androidx.legacy:legacy-support-v4:1.0.0")
       }
       ```

     - build.gradle

       ```groovy translate=no
       dependencies {
           // AppMetrica Push SDK.
           implementation "io.appmetrica.analytics:push:{{ push-sdk-android-version }}" {
            exclude group: "com.squareup.okhttp3", module: "okhttp"
           }
           implementation "androidx.legacy:legacy-support-v4:1.0.0"
       }
       ```

     {% endlist %}

   {% endcut %}

1. Подключите транспорт.

   {% list tabs %}

   - Firebase

     1. Если вы используете Gradle для сборки приложения, добавьте следующую зависимость в Gradle файл приложения:

        - **app/build.gradle.kts**

          ```kotlin translate=no
          dependencies {
                  // minimum support version 20.3.0
                  implementation("com.google.firebase:firebase-messaging:{{ push-sdk-android-version-firebase-messaging }}")
                  implementation("com.google.android.gms:play-services-base:{{ com-google-android-gms-play-services-base }}")
              }
          ```

        - **app/build.gradle**

          ```groovy translate=no
          dependencies {
                  // minimum support version 20.3.0
                  implementation "com.google.firebase:firebase-messaging:{{ push-sdk-android-version-firebase-messaging }}"
                  implementation "com.google.android.gms:play-services-base:{{ com-google-android-gms-play-services-base }}"
              }
          ```

        Используемая при разработке версия указана в [репозитории](https://github.com/appmetrica/push-sdk-android/blob/main/build-logic/src/main/kotlin/io/appmetrica/analytics/gradle/PushConstants.kt#L30).

     1. Инициализируйте Firebase, используя один из способов:

        {% cut "Использование Google Services Plugin" %}

        1. [Загрузите](https://support.google.com/firebase/answer/7015592) конфигурационный файл `google-services.json` и разместите его в каталоге модуля проекта (например, `app`).
        1. Для корректной работы с файлом подключите плагин Google Services в проект, добавив следующие строки в Gradle файл:

            **проекта**

           - **build.gradle.kts**

             ```kotlin translate=no
             buildscript {
                 dependencies {
                     classpath("com.google.gms:google-services:{{ com-google-gms-google-services  }}")
                 }
             }
             ```
           - **build.gradle**

             ```groovy translate=no
             buildscript {
                 dependencies {
                     classpath "com.google.gms:google-services:{{ com-google-gms-google-services  }}"
                 }
             }
             ```

            **приложения (модуля)**

            - **app/build.gradle.kts**

              ```kotlin translate=no
              apply(plugin = "com.google.gms.google-services")
              ```
            - **app/build.gradle**

              ```groovy translate=no
              apply plugin: "com.google.gms.google-services"
              ```

        {% endcut %}

        {% cut "Без использования плагина" %}

        Внесите изменения в элемент `application` файла `AndroidManifest.xml`:

        ```xml translate=no
        <meta-data android:name="ymp_firebase_default_app_id" android:value="APP_ID"/>
        <meta-data android:name="ymp_gcm_default_sender_id" android:value="number:SENDER_ID"/>
        <meta-data android:name="ymp_firebase_default_api_key" android:value="API_KEY"/>
        <meta-data android:name="ymp_firebase_default_project_id" android:value="PROJECT_ID"/>
        ```

        {{ app-id }}

        {{ sender-id }}

        {{ api-key-push }}

        {{ project-id }}

        {% endcut %}

        {% cut "Использование с другими Firebase-проектами" %}

        Внесите изменения в элемент `application` файла `AndroidManifest.xml`:

        ```xml translate=no
        <meta-data android:name="ymp_firebase_app_id" android:value="APP_ID"/>
        <meta-data android:name="ymp_gcm_sender_id" android:value="number:SENDER_ID"/>
        <meta-data android:name="ymp_firebase_api_key" android:value="API_KEY"/>
        <meta-data android:name="ymp_firebase_project_id" android:value="PROJECT_ID"/>
        ```

        {{ app-id }}

        {{ sender-id }}

        {{ api-key-push }}

        {{ project-id }}

        {% note alert %}

        Вам необходимо самостоятельно инициализировать Firebase-проект по умолчанию.

        {% endnote %}

        {% endcut %}

   - HMS

     1. Добавьте [HMS Push Kit](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/android-app-quickstart-0000001071490422) в проект. Используемая при разработке версия указана в [репозитории](https://github.com/appmetrica/push-sdk-android/blob/main/build-logic/src/main/kotlin/io/appmetrica/analytics/gradle/PushConstants.kt#L33).
     1. Если вы используете Gradle для сборки приложения, добавьте следующую зависимость в Gradle файл приложения:

        - **app/build.gradle.kts**
          ```kotlin translate=no
          dependencies {
              implementation("io.appmetrica.analytics:push-provider-hms:{{ push-sdk-android-version }}")
          }
          ```

        - **app/build.gradle**
          ```groovy translate=no
          dependencies {
              implementation "io.appmetrica.analytics:push-provider-hms:{{ push-sdk-android-version }}"
          }
          ```

        {% note alert %}

        Если вы собираетесь использовать только HMS, исключите Firebase зависимость из основной библиотеки:

         - **app/build.gradle.kts**
           ```kotlin translate=no
           dependencies {
               implementation("io.appmetrica.analytics:push:{{ push-sdk-android-version }}") {
                   exclude(group =  "io.appmetrica.analytics", module = "push-provider-firebase")
               }
           }
           ```

         - **app/build.gradle**
           ```groovy translate=no
           dependencies {
               implementation("io.appmetrica.analytics:push:{{ push-sdk-android-version }}") {
                   exclude group: "io.appmetrica.analytics", module: "push-provider-firebase"
               }
           }
           ```

        {% endnote %}

     1. Внесите изменения в элемент `application` файла `AndroidManifest.xml`:

        ```xml translate=no
        <meta-data android:name="ymp_hms_default_app_id" android:value="number:APP_ID"/>
        ```

        `APP_ID` — идентификатор приложения в HMS. Его можно найти в поле `app_id` файла `agconnect-services.json`. Файл можно скачать из [консоли Huawei](https://developer.huawei.com/consumer/{{ locale }}/service/josp/agc/index.html).

   {% endlist %}

AppMetrica Push SDK умеет работать одновременно с Firebase и с HMS.

## Шаг 3. Инициализируйте библиотеку {#initialization}

Инициализируйте библиотеку в приложении — объявите производный класс от базового класса `Application` и переопределите метод `onCreate()` следующим образом:

{% cut "Только Firebase" %}

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  class MyApp : Application() {
      override fun onCreate() {
          super.onCreate()
          AppMetricaPush.activate(applicationContext)
      }
  }
  ```

- Java

  ```java translate=no
  public class MyApp extends Application {
      @Override
      public void onCreate() {
          super.onCreate();
          AppMetricaPush.activate(getApplicationContext());
      }
  }
  ```

{% endlist %}

{% endcut %}

{% cut "Только HMS" %}

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  class MyApp : Application() {
      override fun onCreate() {
          super.onCreate()
          AppMetricaPush.activate(applicationContext, HmsPushServiceControllerProvider(this))
      }
  }
  ```

- Java

  ```java translate=no
  public class MyApp extends Application {
      @Override
      public void onCreate() {
          super.onCreate();
          AppMetricaPush.activate(getApplicationContext(), new HmsPushServiceControllerProvider(this));
      }
  }
  ```

{% endlist %}

{% endcut %}

{% cut "Firebase и HMS" %}

{% list tabs group=instructions %}

- Kotlin

  Добавьте зависимость, чтобы иметь возможность вызвать `FirebasePushServiceControllerProvider(this)`:

  ```kotlin translate=no
  dependencies {
      implementation("io.appmetrica.analytics:push-provider-firebase:$appmetrica_push_version")
  }
  ```

  Переопределите класс:

  ```kotlin translate=no
  class MyApp : Application() {
      override fun onCreate() {
          super.onCreate()
          AppMetricaPush.activate(
              applicationContext,
              FirebasePushServiceControllerProvider(this),
              HmsPushServiceControllerProvider(this)
          )
      }
  }
  ```

- Java

  Добавьте зависимость, чтобы иметь возможность вызвать `FirebasePushServiceControllerProvider(this)`:

  ```java translate=no
  dependencies {
      implementation "io.appmetrica.analytics:push-provider-firebase:$appmetrica_push_version"
  }
  ```

  Переопределите класс:

  ```java translate=no
  public class MyApp extends Application {
      @Override
      public void onCreate() {
          super.onCreate();
          AppMetricaPush.activate(
              getApplicationContext(),
              new FirebasePushServiceControllerProvider(this),
              new HmsPushServiceControllerProvider(this)
          );
      }
  }
  ```

{% endlist %}

{% endcut %}

{% note alert %}

Библиотеку AppMetrica Push SDK необходимо инициализировать в главном процессе.

{% endnote %}

## Шаг 4. (_Опционально_) Настройте Silent Push Notifications {#settings-of-silent-push}

Настройте обработку push-уведомлений, которые не предполагают вывод сообщений (Silent Push Notifications).

1. Создайте специальный `BroadcastReceiver`:

   {% list tabs group=instructions %}

    - Kotlin

      ```kotlin translate=no
      class SilentPushReceiver : BroadcastReceiver() {
          override fun onReceive(context: Context, intent: Intent) {
              // Extract push message payload from your push message.
              val payload = intent.getStringExtra(AppMetricaPush.EXTRA_PAYLOAD)
          }
      }
      ```

   - Java

     ```java translate=no
     public class SilentPushReceiver extends BroadcastReceiver {
         @Override
         public void onReceive(Context context, Intent intent) {
             // Extract push message payload from your push message.
             String payload = intent.getStringExtra(AppMetricaPush.EXTRA_PAYLOAD);
         }
     }
     ```

   {% endlist %}

2. Внесите изменения в элемент `application` файла `AndroidManifest.xml`:

    ```xml translate=no
    <manifest xmlns:android="http://schemas.android.com/apk/res/android">
      <application>
        <receiver android:name=".SilentPushReceiver">
          <intent-filter>
            <!-- Receive silent push notifications -->
            <action android:name="${applicationId}.action.ymp.SILENT_PUSH_RECEIVE"/>
          </intent-filter>
        </receiver>
      </application>
    </manifest>
    ```

    `applicationId` — уникальный идентификатор приложения в Gradle (имя пакета).
    Например, `com.example.name`.

## Шаг 5. (_Опционально_) Включите актуализацию push‑токенов {#actualization}

{% note alert "" %}

Если у вас есть свой сервис для обработки пушей (класс, унаследованный от `FirebaseMessagingService` или `HmsMessageService`), проверьте, что не обрабатываете пуши от AppMetrica.

Чтобы проверить, что пуш не от AppMetrica, воспользуйтесь методом `AppMetricaMessagingService.isNotificationRelatedToSDK` или `AppMetricaHmsMessagingService.isNotificationRelatedToSDK`.

{% endnote %}

Сервис FCM может отозвать push-токен устройства, например, если пользователь долго не запускал приложение. AppMetrica хранит push-токены на сервере и не может отправить push-уведомление на устройство с устаревшим токеном.

Чтобы автоматически собирать актуальные push-токены, перейдите в настройки приложения в веб-интерфейсе AppMetrica и выберите опцию **Актуализировать токены с помощью Silent Push-уведомлений** во вкладке **Push-уведомления**.

## Шаг 6. (_Опционально_) Настройте использование с другими push SDK {#other-push-services}

Если в приложение интегрировано несколько SDK для обработки push-уведомлений, выполните инструкцию [{#T}](android-other-push-services-settings.md).

{% note info "" %}

Необходимо выполнить дополнительные настройки, иначе возможны проблемы с обработкой push-уведомлений.

{% endnote %}

## Отправка дополнительной информации {#send-additional-info}

При необходимости вы можете передавать вместе с push-уведомлением дополнительную информацию. Эти данные указываются в веб-интерфейсе AppMetrica при [настройке push-кампании](../../../push/marketing.md).

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  class TargetActivity : Activity() {
      override fun onCreate(savedInstanceState: Bundle?) {
          super.onCreate(savedInstanceState)
          handlePayload(intent)
      }

      override fun onNewIntent(intent: Intent) {
          super.onNewIntent(intent)
          handlePayload(intent)
      }

      private fun handlePayload(intent: Intent) {
          // Handle your payload.
          val payload = intent.getStringExtra(AppMetricaPush.EXTRA_PAYLOAD)
      }
  }
  ```

- Java

  ```java translate=no
  public class TargetActivity extends Activity {
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          handlePayload(getIntent());
      }

      @Override
      protected void onNewIntent(Intent intent) {
          super.onNewIntent(intent);
          handlePayload(intent);
      }

      private void handlePayload(Intent intent) {
          // Handle your payload.
          String payload = intent.getStringExtra(AppMetricaPush.EXTRA_PAYLOAD);
      }
  }
  ```

{% endlist %}

## Отслеживание запуска приложения через push-уведомление {#track-start-via-push}

Чтобы отличить запуски приложения по открытию push-уведомления AppMetrica Push SDK от общего числа запусков, необходимо проверить [Intent action](https://developer.android.com/reference/android/content/Intent.html#getAction()) приложения:

- Если в качестве действия вы указали deeplink, он будет являться Intent action.

- Если в качестве действия выбрано открытие приложения, Intent action будет передавать значение `AppMetricaPush#OPEN_DEFAULT_ACTIVITY_ACTION`.

## Настройка иконки по умолчанию {#icon}

Чтобы указать иконку push-уведомления по умолчанию, внесите изменения в элемент `application` файла `AndroidManifest.xml`:

```
<meta-data android:name="io.appmetrica.analytics.push.default_notification_icon"
           android:resource="ICON_RESOURCE"/>
```

`ICON_RESOURCE` — ресурс иконки.
Например, `@drawable/large_icon`.

## Изменение настроек канала уведомлений {#notification-channel}

Вы можете изменить настройки канала уведомлений, используемого по умолчанию. Например, добавить в него описание или изменить важность. 

{% note info "" %}

Изменить настройки канала можно только до его создания, то есть до отправки первого пуша через AppMetrica.

{% endnote %}

Для получения дефолтного канала вызовите метод `getDefaultNotificationChannel()`:

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  AppMetricaPush.getDefaultNotificationChannel()?.apply {
      description = "Push from AppMetrica"
      importance = NotificationManager.IMPORTANCE_HIGH
      // Modify NotificationChannel properties
  }
  ```

- Java

  ```java translate=no
  NotificationChannel channel = AppMetricaPush.getDefaultNotificationChannel();
  if (channel != null) {
      channel.setDescription("Push from AppMetrica");
      channel.setImportance(NotificationManager.IMPORTANCE_HIGH);
      // Modify NotificationChannel
  }
  ```

{% endlist %}

## Узнать больше {#learn-more}

- [Настройка приложения на базе Android для отправки push-уведомлений](android-settings.md)
- [Как проверить, что у меня установлены последние версии Android-библиотек?](../../../troubleshooting/troubleshooting.md#newest-android-version)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
