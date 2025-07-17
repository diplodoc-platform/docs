# Usage

Using `appmetrica_push_plugin` together with plugins from other providers (`flutter_rustore_push`, `huawei_push`, `firebase_messaging`) may block the delivery of notifications. To fix this, remove the service that adds an extra push plugin from your app.


Add the following code to the `android/app/src/main/AndroidManifest.xml` file within the `<application>` tag:

{% list tabs %}

- RuStore

  ```xml translate=no
  <service
    android:name="ru.rustore.flutter_rustore_push.FlutterRustorePushService"
    tools:node="remove"
  />
  ```

- HMS

  ```xml translate=no
  <service
      android:name="com.huawei.hms.flutter.push.hms.FlutterHmsMessageService"
      tools:node="remove"
  />
  ```

- Firebase

  ```xml translate=no
  <service
      android:name="io.flutter.plugins.firebase.messaging.FlutterFirebaseMessagingService"
      tools:node="remove"
  />
  ```

{% endlist %}
