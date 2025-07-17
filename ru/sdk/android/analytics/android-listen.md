# Отслеживание активности пользователей

{% include notitle [Отслеживание активности пользователей](../../_includes/listen-intro.md) %}

## Установка длительности таймаута сессии

{% include notitle [отсчет таймаута](../../_includes/timeout-notify-listen.md) %}

По умолчанию длительность таймаута сессии равна 10 секундам. Это минимально допустимое значение параметра `sessionTimeout`.

Чтобы изменить длительность таймаута, передайте значение в секундах в метод `withSessionTimeout(int sessionTimeout)` при создании расширенной конфигурации библиотеки.

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

## Отслеживание жизненного цикла приложения {#listen}

Если для приложения минимальная версия Android задана 4.0 или выше, то библиотека AppMetrica может отслеживать жизненный цикл приложения в автоматическом режиме — после инициализации библиотеки вызовите метод `AppMetrica.enableActivityAutoTracking(Application application)`:

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

Автоматическое отслеживание активности работает только для главного API key. При отправке статистики на дополнительный API key используйте методы интерфейса IReporter.

{% endnote %}

Если заданная в приложении минимальная версия Android ниже 4.0, используйте следующие методы: `AppMetrica.resumeSession(activity)` и `AppMetrica.pauseSession(activity)` в соответствующих методах ваших Activity: `onResume()` и `onPause()`. При использовании этих методов необходимо отслеживать, чтобы активная сессия всегда завершалась вызовом метода `AppMetrica.pauseSession(activity)`. Если метод не вызван, библиотека считает сессию активной и совершает регулярный обмен данными с сервисной частью AppMetrica. Это может привести к некорректному отслеживанию длительности сессии и повышению энергопотребления.

Пример:

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

## Работа с дополнительным API key

С помощью отправки данных на дополнительный API key можно управлять доступом к статистике. Для передачи событий используйте репортеры. Подробнее см. в разделе [Примеры использования методов](android-operations.md).

Для корректного отслеживания сессий взаимодействия пользователя с приложением настройте отправку событий о начале и приостановке сессии для каждого репортера. Для этого используйте методы `resumeSession()` и `pauseSession()` интерфейса IReporter в реализации `onResume()` и `onPause()` ваших Activity:

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

Это поможет библиотеке правильно отслеживать:

- количество активных пользователей;
- продолжительность сессий;
- частоту использования приложения.

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}

[*timeout-session]: Таймаут сессии, который настраивается в SDK.
