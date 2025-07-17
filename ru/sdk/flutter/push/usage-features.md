# Особенности использования

Совместное использование `appmetrica_push_plugin` и плагинов других провайдеров (`flutter_rustore_push`, `huawei_push`, `firebase_messaging`) может блокировать доставку уведомлений. Чтобы это исправить, удалите из приложения сервис, который подключает дополнительный push-плагин.


В файле `android/app/src/main/AndroidManifest.xml` внутри тега `<application>` добавьте код:

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
