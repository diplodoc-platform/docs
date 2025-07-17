# Логирование

AppMetrica SDK записывает в логи:

- факт активации SDK;
- факт получения события от приложения;
- факт отправки события на сервис;
- факт сохранения события в локальную БД;
- факт отправки события на сервер;
- факт удаления отправленного события из локальной БД;
- различные ошибки и предупреждения, которые могут повлиять на ожидаемое поведение библиотеки.

Чтобы использовать логи SDK, выполните действия:

1. Включите логирование при активации SDK, используя расширенную конфигурацию. 

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

2. Выгрузите логи через adb командой `adb logcat -v time >> ${PATH_TO_FILE}` или откройте их в IDE logcat.

3. Если нужно, отфильтруйте логи AppMetrica SDK по тегу `AppMetrica`.   

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
