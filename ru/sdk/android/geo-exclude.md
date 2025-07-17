# Исключение гео из списка зависимостей

Работа с гео вынесена в отдельную зависимость `io.appmetrica.analytics:analytics-location`. Эта библиотека содержит зависимость от `com.google.android.gms:play-services-location:19.0.1`, которая используется для получения локации. Версия библиотеки `io.appmetrica.analytics:analytics-location` должна соответствовать версии библиотеки `io.appmetrica.analytics:analytics`.

Если вам необходимо отключить гео, например, для отдельных категорий приложений в соответствии с политиками Google Play, просто исключите модуль из списка зависимостей:

{% list tabs %}

- build.gradle.kts

  ```kotlin translate=no
  configurations.configureEach {
      exclude(group = "io.appmetrica.analytics", module = "analytics-location")
  }
  ```

- build.gradle

  ```groovy translate=no
  configurations.configureEach {
      exclude group: 'io.appmetrica.analytics', module: 'analytics-location'
  }
  ```

{% endlist %}

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
