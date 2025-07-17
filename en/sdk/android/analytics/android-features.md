# How the AppMetrica library works

The AppMetrica library consists of two parts: the client and the service. You should take their features into account during initialization:

- Client part: Pre-validates data and transmits it to the service part. An instance of the client part is created for each process in the application.

- Service part: It is responsible for storing data and sending it to the server. The service runs in the main application process. Therefore AppMetrica SDK saves the crash report to a file and sends them the next time it is run.

## Recommendations for initialization {#recommendations}

- If the application has multiple processes where you want to use AppMetrica, initialize the library with the same configuration for each process. Otherwise, the configuration may depend on which of the processes starts first.

   {% note info "" %}

   You can use reporters for sending data. They can be initialized with different configurations. For more information, see [Sending statistics to an additional API key](android-operations.md#reporter-different-apikey).

   {% endnote %}

- Initialize the AppMetrica library in the [Application.onCreate()](https://developer.android.com/reference/android/app/Application.html#onCreate%28%29) method. As a result, the library will be initialized within each process.

- Keep in mind that the [ContentProvider](https://developer.android.com/intl/ru/reference/android/content/ContentProvider.html) instance is created before the [Application](https://developer.android.com/intl/ru/reference/android/app/Application.html) instance. If you initialize the library in the `Application.onCreate()` method, you can't send data from the `ContentProvider.onCreate()` method.

- Don't add the code to the `Application.onCreate()` method that should not be executed more than once. Run this code when creating other components, or run it in a separate [Service](https://developer.android.com/intl/ru/reference/android/app/Service.html).

- Avoid long-term operations in the `Application.onCreate()` method and do not initialize other libraries in it. The execution time of this method directly affects the opening speed of the first `Activity`, `Service`, or `Receiver`.

## Learn more {#learn-more}

<!-- - [Пример интеграции библиотеки ССЫЛКА НУЖНА](ССЫЛКА) -->
- [How do I enable user location sending?](../../../troubleshooting/troubleshooting.md#region)
- [How can I make sure that I have the latest versions of the Android libraries installed?](../../../troubleshooting/troubleshooting.md#newest-android-version)
- [Why aren't new installs shown in reports?](../../../troubleshooting/troubleshooting.md#no-installs)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
