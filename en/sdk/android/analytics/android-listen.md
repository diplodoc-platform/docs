# Tracking user activity

{% include notitle [Отслеживание активности пользователей](../../_includes/listen-intro.md) %}

## Setting the session timeout

{% include notitle [отсчет таймаута](../../_includes/timeout-notify-listen.md) %}

By default, the session timeout is 10 seconds. The minimum acceptable value for the `sessionTimeout` parameter is 10 seconds.

To change the timeout, pass the value in seconds to the `withSessionTimeout(int sessionTimeout)` method when creating the extended library configuration.

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

## Monitoring the app lifecycle {#listen}

If the app has the minimum Android version set to 4.0 or later, the AppMetrica library can track its lifecycle automatically. After library initialization, call the `AppMetrica.enableActivityAutoTracking(Application application)` method:

{% list tabs group=instructions %}

- Kotlin

   ```kotlin translate=no
   class YourApplication : Application() {
       override fun onCreate() {
           super.onCreate()

           // Initializing the AppMetrica SDK.
           AppMetrica.activate(...)
           // Automatic tracking user activity.
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

           // Initializing the AppMetrica SDK.
           AppMetrica.activate(...);
           // Automatic tracking user activity.
           AppMetrica.enableActivityAutoTracking(this);
       }
   }
   ```

{% endlist %}

{% note info %}

Automatic activity tracking only works for the main API key. When sending statistics to an additional API key, use the IReporter interface methods.

{% endnote %}

If the minimum Android version in the app is earlier than 4.0, use the following methods: `AppMetrica.resumeSession(activity)` and `AppMetrica.pauseSession(activity)` in the corresponding methods for your activity, which are `onResume()` and `onPause()`. When using those methods, make sure the active session is always terminated by calling the `AppMetrica.pauseSession(activity)` method. If that method is not called, the library considers the session active and commits regular data exchange with the service part of AppMetrica. This can lead to incorrect tracking of the session duration and energy consumption.

Example:

{% list tabs group=instructions %}

- Kotlin

   ```kotlin translate=no
   class YourActivity : Activity() {
       override fun onResume() {
           super.onResume()
           AppMetrica.resumeSession(this)
       }

       override fun onPause() {
           AppMetrica.pauseSession(this)
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
           AppMetrica.resumeSession(this);
       }

       @Override
       protected void onPause() {
           AppMetrica.pauseSession(this);
           super.onPause();
       }
   }
   ```

{% endlist %}

## Working with an additional API key

By sending data to an additional API key, you can control the access to statistics. Use reporters to transmit events. For more information, see [Usage examples](android-operations.md).

For correct tracking, manually configure the reporters to send events about the start and the pause of the session for each reporter. Use the `resumeSession()` and `pauseSession()` methods in the IReporter interface when implementing `onResume()` and `onPause()` for your activity:

{% list tabs group=instructions %}

- Kotlin

   ```kotlin translate=no
   class YourActivity : Activity() {
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

This helps the library accurately monitor:

- The number of active users.
- Session length.
- Frequency of app use.

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}

[*timeout-session]: Session timeout that you set in the SDK.
