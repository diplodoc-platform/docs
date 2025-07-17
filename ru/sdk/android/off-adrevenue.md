# Выключение автосбора Ad Revenue

{% note alert %}

Автосбор Ad Revenue для Fyber не поддерживается. Его использование на версиях от 6.4.0 до 7.0.0 приводит к [конфликту в коде](analytics/android-errors.md#fyber-unsupport-adrevenue).

{% endnote %}

Автосбор Ad Revenue вынесен в отдельную зависимость `io.appmetrica.analytics:analytics-ad-revenue`. Версия библиотеки `io.appmetrica.analytics:analytics-ad-revenue` должна соответствовать версии библиотеки `io.appmetrica.analytics:analytics`.

Если вам необходимо отключить автосбор Ad Revenue, то исключите модуль из списка зависимостей:

{% list tabs %}

- build.gradle.kts

  ```kotlin translate=no
  configurations.configureEach {
      exclude(group = "io.appmetrica.analytics", module = "analytics-ad-revenue")
  }
  ```

- build.gradle

  ```groovy translate=no
  configurations.configureEach {
      exclude group: 'io.appmetrica.analytics', module: 'analytics-ad-revenue'
  }
  ```

{% endlist %}

В настоящий момент автосбор поддерживается для ironSource. Если необходимо отключить автосбор Ad Revenue, то исключите модуль `io.appmetrica.analytics:ad-revenue-ironsource-v7`.

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
