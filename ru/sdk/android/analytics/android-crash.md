# Анализ крэшей

AppMetrica бесконфликтно работает с другими библиотеками, которые собирают и обрабатывают крэши. Если вы используете такие библиотеки, произведите инициализацию AppMetrica после установки данных библиотек.

Отчет о крэше сразу сохраняется в файл и отправляется при следующем запуске.

{% note info "" %}

Символизация и деобфускация крэшей не производятся библиотекой. Данные операции выполняются на сервере или стороне клиента.

Для загрузки mapping-файлов в AppMetrica используется [AppMetrica Gradle Plugin](android-gradle-plugin.md). Он автоматически загружает mapping и SO-файлы при сборке приложения. Подробнее в разделе [Загрузка mapping-файлов и отладочных символов на Android](../../../data-collection/upload-mapping.md).

{% endnote %}

Для автоматического сбора сведений об аварийных остановках приложения AppMetrica использует стандартный обработчик [Thread.UncaughtExceptionHandler](https://developer.android.com/reference/java/lang/Thread.UncaughtExceptionHandler.html). Если вы используете обработчик аварийных остановок непосредственно в приложении, используйте следующий пример реализации корректной обработки данных:

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

Так вы, обработав исключение самостоятельно, передаете его дальше и AppMetrica сможет отправить сведения о нем.

Если вы хотите передать дополнительную информацию об аварийном отключении приложения, используйте данный пример до [инициализации библиотеки в приложении](quick-start.md).

## Узнайте больше

- [AppMetrica Gradle Plugin](android-gradle-plugin.md)
- [Загрузка mapping-файлов и отладочных символов на Android](../../../data-collection/upload-mapping.md)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
