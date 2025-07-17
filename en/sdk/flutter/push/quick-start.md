# Installation and initialization

To integrate AppMetrica Push SDK into Flutter, use the [AppMetrica Push SDK for Flutter](https://pub.dev/packages/appmetrica_push_plugin) plugin:

1. Install the AppMetrica Push SDK plugin in your project. From the root of the project, run the command:

   ```bash translate=no
   flutter pub add appmetrica_push_plugin
   ```

   After adding the plugin, you'll see a line with the following dependency in the `pubspec.yaml` file:

   ```java translate=no
   dependencies:
       appmetrica_push_plugin: ^{{ appmetrica-push-flutter-plugin }}
   ```

2. Add `appmetrica_plugin` and `appmetrica_push_plugin` import:

   ```java translate=no
   import 'package:appmetrica_plugin/appmetrica_plugin.dart';
   import 'package:appmetrica_push_plugin/appmetrica_push_plugin.dart';
   ```

3. Initialize the AppMetrica SDK library using `AppMetrica.activate` and your API key:

   ```bash translate=no
   AppMetrica.activate(AppMetricaConfig("insert_your_api_key_here"));
   ```

4. Initialize the AppMetrica Push SDK using `AppMetricaPush.activate` and your API key:

   ```bash translate=no
   AppMetricaPush.activate();
   ```

5. To complete the integration of sending push notifications, use the documentation for each native platform:

   {% list tabs %}

   - Android

      1\. [Set up](../../android/push/android-settings.md#firebase) the app for using Firebase. [Get and add to AppMetrica](../../android/push/android-settings.md#firebase-key) a server key for using Firebase Cloud Messaging:

      2\. Connect Firebase transport by adding the following dependencies to the `android/app/build.gradle` file:

      ```kotlin translate=no
      dependencies {
         implementation "com.google.firebase:firebase-messaging: {{ push-sdk-android-version-firebase-messaging }}"
         implementation "com.google.android.gms:play-services-base: {{ com-google-android-gms-play-services-base }}"
      }
      ```

      3\. Initialize Firebase transport using one of the following methods:

      {% cut "Using Google Services Plugin" %}

      1\. [Download](https://support.google.com/firebase/answer/7015592) the configuration file `google-services.json` and put it in the project module's directory (such as `app`).

      2\. For the file to work correctly, enable the Google Services plugin in the project by adding the following lines to the Gradle file:

      ##### project

      * **build.gradle.kts**

         ```kotlin translate=no
         buildscript {
               dependencies {
                  classpath("com.google.gms:google-services:{{ com-google-gms-google-services  }}")
               }
            }
         ```

      * **build.gradle**

         ```groovy translate=no
         buildscript {
            dependencies {
               classpath "com.google.gms:google-services:{{ com-google-gms-google-services  }}"
            }
         }
         ```

      ##### application (module)

      * **app/build.gradle.kts**

         ```kotlin translate=no
         apply(plugin = "com.google.gms.google-services")
         ```

      * **app/build.gradle**

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

      4\. If needed, [configure silent push notifications](../../android/push/quick-start.md#settings-of-silent-push) or [enable push tokens update](../../android/push/quick-start.md#actualization).


   - iOS

      1\. Add the SSL certificate to AppMetrica according to the [instructions](../../ios/push/ios-settings.md).

      2\. Add **Capability Push Notifications** to your XCode project.

      3\. If needed, [enable push tokens update](../../ios/push/quick-start.md#actualization) or [configure uploading of attached files](../../ios/push/quick-start.md#download-file).

      4\. [Set up](../../ios/push/ios-settings.md) statistics collection.

   {% endlist %}

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
