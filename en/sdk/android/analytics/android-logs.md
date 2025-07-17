# Logging

The AppMetrica SDK logs:

- Activation of the SDK.
- Events received from the app.
- Events sent to the service.
- Events saved to the local database.
- Events sent to the server.
- Deletion of saved events from the local database.
- Various errors and warnings that may affect the expected behavior of the library.

To use the SDK logs:

1. When activating the SDK, enable logging using an extended configuration.

    {% list tabs group=instructions %}

    - Kotlin

      ```kotlin translate=no
      class YourApplication : Application() {
          override fun onCreate() {
              super.onCreate()
              // Creating an extended library configuration.
              val config = AppMetricaConfig.newConfigBuilder(API_KEY).build()
              // Initializing the AppMetrica SDK.
              AppMetrica.activate(this, config)
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
              AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_KEY).build();
              // Initializing the AppMetrica SDK.
              AppMetrica.activate(this, config);
          }
      }
      ```

    {% endlist %}

2. Export the logs using adb by running the `adb logcat -v time >> ${PATH_TO_FILE}` command or open them in the Logcat IDE.

3. If needed, filter the AppMetrica SDK logs by the `AppMetrica` tag.

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
