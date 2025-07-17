# Analyzing crashes

AppMetrica doesn't conflict with other libraries that collect and process app crashes. If you use such libraries, initialize AppMetrica after installing these libraries. 

AppMetrica SDK saves the crash report to a file and sends them the next time it is run.

{% note info "" %}

The library does not symbolicate or deobfuscate app crashes. These operations are performed on the server or on the client side.

To upload mapping files to AppMetrica, use the [AppMetrica Gradle Plugin](android-gradle-plugin.md). It automatically uploads the mapping and SO files when building an app. For more information, see [uploading mapping files and debugging symbols on Android](../../../data-collection/upload-mapping.md).

{% endnote %}

For automatically collecting information about app crashes, AppMetrica uses the standard handler [Thread.UncaughtExceptionHandler](https://developer.android.com/reference/java/lang/Thread.UncaughtExceptionHandler.html). If you are using an app crash handler directly inside the app, use the following example of implementing correct data handling:

{% list tabs group=instructions %}

- Kotlin

   ```kotlin translate=no
   val previousUncaughtExceptionHandler = Thread.getDefaultUncaughtExceptionHandler()
   // Creating a new handler.
   val uncaughtExceptionHandler = Thread.UncaughtExceptionHandler { thread, exception ->
       try {
           // Put your logic here.
       } finally {
           // Sending a message about an app crash to the system handler.
           previousUncaughtExceptionHandler?.uncaughtException(thread, exception)
       }
   }
   // Setting the default handler.
   Thread.setDefaultUncaughtExceptionHandler(uncaughtExceptionHandler)
   ```

- Java

   ```java translate=no
   final Thread.UncaughtExceptionHandler previousUncaughtExceptionHandler = Thread.getDefaultUncaughtExceptionHandler();
   // Creating a new handler.
   Thread.UncaughtExceptionHandler uncaughtExceptionHandler = new Thread.UncaughtExceptionHandler() {
       @Override
       public void uncaughtException(@NotNull Thread thread, @NotNull Throwable exception) {
           try {
               // Put your logic here.
           } finally {
               // Sending a message about an app crash to the system handler.
               if (previousUncaughtExceptionHandler != null) {
                   previousUncaughtExceptionHandler.uncaughtException(thread, exception);
               }
           }
       }
   };
   // Setting the default handler.
   Thread.setDefaultUncaughtExceptionHandler(uncaughtExceptionHandler);
   ```

{% endlist %}

This way you handle the exception yourself, then pass it on, and AppMetrica can send information about it.

If you want to transmit additional information about an app crash, use this example up to [initializing the library in the app](quick-start.md).

## Learn more

- [AppMetrica Gradle Plugin](android-gradle-plugin.md)
- [Uploading mapping files and debugging symbols on Android](../../../data-collection/upload-mapping.md)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
