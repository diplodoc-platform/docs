# Using with other push services

You can use AppMetrica Push SDK and other push services at the same time. To do this, you need to create a FCM or HMS service that will redirect messages between integrated SDKs.

## Using with other Firebase push services {#fcm}

### Step 1. Make changes in AndroidManifest.xml {#fcm-settings}

Make changes in the `application` element in the `AndroidManifest.xml` file:

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

### Step 2. Add dependencies to your project {#dependencies}

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

### Step 3. Add push notifications handling {#handling}

Declare the derived `FirebaseMessagingMainService` class from the base `FirebaseMessagingService` class for handling push notifications:

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

### Step 4. Add push token processing {#tokens}

Add push token processing to the `FirebaseMessagingMainService` class code:

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

## Using with other HMS push services {#hms}

### Step 1. Make changes in AndroidManifest.xml {#hms-settings}

Make changes in the `application` element in the `AndroidManifest.xml` file:

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

### Step 2. Add push notifications handling {#hms-handling}

Declare the derived `HmsMessagingMainService` class from the base `HmsMessageService` class for handling push notifications:

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

### Step 3. Add push token processing {#hms-tokens}

Add push token processing to the `HmsMessagingMainService` class code:

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

#### See also

- [Connecting the AppMetrica Push SDK](quick-start.md)
- [Launching a push campaign](../../../push/marketing.md)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
