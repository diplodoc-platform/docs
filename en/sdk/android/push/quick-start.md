# Installation and initialization

The Push SDK for Android is a library in the AAR format.
The library is available in the [Maven repository](https://search.maven.org/search?q=g:io.appmetrica.analytics%20AND%20a:push).

This section describes the steps to enable and initialize AppMetrica Push SDK:

## Step 1.  Prepare your app {#preparation}

Before integrating the AppMetrica Push SDK library, prepare your app:

1. [Integrate the AppMetrica SDK library](../analytics/quick-start.md) at least version 6.0.0.
2. [Configure your app](android-settings.md) for sending push notifications.

## Step 2. Enable the library {#installation}

Push SDK uses the [OKHttp](https://github.com/square/okhttp) library to cache images displayed in push notifications.
Caching rules are taken from the `cache-control` HTTP header.
If you do not want the images to be cached, connect the library without caching.

1. If you use Gradle to build the app, add the dependency to the app's Gradle file:

   {% cut "With caching" %}

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

   {% cut "Without caching" %}

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

1. Connect the transport.

   {% list tabs %}

   - Firebase

     1. If you use Gradle to build the app, add the dependency to the app's Gradle file:

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
        The version used in development is listed in [repository](https://github.com/appmetrica/push-sdk-android/blob/main/build-logic/src/main/kotlin/io/appmetrica/analytics/gradle/PushConstants.kt#L30).

     1. Initialize Firebase using one of the following methods:

        {% cut "Using Google Services Plugin" %}

        1. [Download](https://support.google.com/firebase/answer/7015592) the configuration file `google-services.json` and put it in the project module's directory (such as `app`).
        1. For the file to work correctly, enable the Google Services plugin in the project by adding the following lines to the Gradle file:

            **project**

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

            **application (module)**

            - **app/build.gradle.kts**

              ```kotlin translate=no
              apply(plugin = "com.google.gms.google-services")
              ```
            - **app/build.gradle**

              ```groovy translate=no
              apply plugin: "com.google.gms.google-services"
              ```

        {% endcut %}

        {% cut "Without using the plugin" %}

        Make changes in the `application` element in the `AndroidManifest.xml` file:

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

        {% cut "Using with other Firebase projects" %}

        Make changes in the `application` element in the `AndroidManifest.xml` file:

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

        You should initialize default Firebase project.

        {% endnote %}

        {% endcut %}

   - HMS

     1. Add [HMS Push Kit](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/android-app-quickstart-0000001071490422) to the project. The version used in development is listed in [repository](https://github.com/appmetrica/push-sdk-android/blob/main/build-logic/src/main/kotlin/io/appmetrica/analytics/gradle/PushConstants.kt#L33).
     1. If you use Gradle to build the app, add the dependency to the app's Gradle file:

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

        If you're only going to use HMS, exclude the Firebase dependency from the main library:

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

     1. Make changes in the `application` element in the `AndroidManifest.xml` file:

        ```xml translate=no
        <meta-data android:name="ymp_hms_default_app_id" android:value="number:APP_ID"/>
        ```

        `APP_ID` — App ID in HMS. You can find it in the `app_id` field of the `agconnect-services.json` file. The file can be downloaded from the [Huawei console](https://developer.huawei.com/consumer/{{ locale }}/service/josp/agc/index.html).

   {% endlist %}

The AppMetrica Push SDK can simultaneously work with Firebase and HMS.

## Step 3. Initialize the library {#initialization}

Initialize the library in the app — extend the `Application` class and override the `onCreate()` method as follows:

{% cut "Firebase only" %}

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

{% cut "HMS only" %}

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

{% cut "Firebase and HMS" %}

{% list tabs group=instructions %}

- Kotlin

  Add the following dependency to allow calling `FirebasePushServiceControllerProvider(this)`:

  ```kotlin translate=no
  dependencies {
      implementation("io.appmetrica.analytics:push-provider-firebase:$appmetrica_push_version")
  }
  ```

  Override the class:

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

  Add the following dependency to allow calling `FirebasePushServiceControllerProvider(this)`:

  ```java translate=no
  dependencies {
      implementation "io.appmetrica.analytics:push-provider-firebase:$appmetrica_push_version"
  }
  ```

  Override the class:

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

The AppMetrica Push SDK library must be initialized in the main process.

{% endnote %}

## Step 4. (_Optional_) Configure Silent Push Notifications {#settings-of-silent-push}

Configure processing silent push notifications.

1. Create a special `BroadcastReceiver`:

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

2. Make changes in the `application` element in the `AndroidManifest.xml` file:

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

    `applicationId` — Unique app ID in Gradle (package name).
    For example, `com.example.name`.

## Step 5. (_Optional_) Enable push tokens update {#actualization}

{% note alert "" %}

If you have your own service to handle push notifications (a class inherited from `FirebaseMessagingService` or `HmsMessageService`), check that you are not handling push notifications from AppMetrica.

To check that the push notification is not from AppMetrica, use the `AppMetricaMessagingService.isNotificationRelatedToSDK` or `AppMetricaHmsMessagingService.isNotificationRelatedToSDK` method.

{% endnote %}

The FCM service can withdraw the push token of the device, for example, if the user did not launch the application for a long time. AppMetrica stores push tokens on the server and can not send a push notification to a device with an obsolete token.

To automatically collect current push token go to the application settings in the AppMetrica interface and enable the **Update tokens with a Silent Push notification** option in the **Push Notifications** tab.

## Step 6. (_Optional_) Configure usage with other push SDKs {#other-push-services}

If you have integrated multiple SDKs for handling push notifications into your app, follow the guide [{#T}](android-other-push-services-settings.md).

{% note info "" %}

You need to make additional settings, otherwise, you may encounter issues with processing push notifications.

{% endnote %}

## Sending additional information {#send-additional-info}

You can send additional information with the push notification if necessary. This data is specified in the AppMetrica web interface when [configuring the push campaign](../../../push/marketing.md).

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

## Detecting the application launch via push notification {#track-start-via-push}

To distinguish app launches initiated by opening an AppMetrica push notification from the total number of app starts, you should check the [Intent action](https://developer.android.com/reference/android/content/Intent.html#getAction()) of the app:

- If you specified a deeplink as the action, this will be the Intent action.

- If the action is set as opening the app, the Intent action passes the value `AppMetricaPush#OPEN_DEFAULT_ACTIVITY_ACTION`.

## Setting the default icon {#icon}

To set the default push notification icon, make changes in the `application` element in the `AndroidManifest.xml` file:

```
<meta-data android:name="io.appmetrica.analytics.push.default_notification_icon"
           android:resource="ICON_RESOURCE"/>
```

`ICON_RESOURCE` — Icon resource.
For example, `@drawable/large_icon`.

## Changing the notification channel settings {#notification-channel}

You can change the settings of the default notification channel. For example, add a description to it or change its priority.

{% note info "" %}

You can change the channel settings only before it is created, that is, before sending the first push via AppMetrica.

{% endnote %}

To get the default channel, call the `getDefaultNotificationChannel()` method:

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

## Learn more {#learn-more}

- [Configuring an Android application to send push notifications](android-settings.md)
- [How can I make sure that I have the latest versions of the Android libraries installed?](../../../troubleshooting/troubleshooting.md#newest-android-version)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
