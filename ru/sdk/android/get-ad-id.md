# Получение рекламных идентификаторов

Рекламный идентификатор — уникальный идентификатор сервисов Google Play для показа рекламы пользователям, которые согласны видеть персонализированные объявления. Пользователь может отключить персонализацию рекламы или сбросить идентификатор в настройках. В таком случае рекламные сети не смогут использовать его для подбора релевантной рекламы. Также значительно снизится точность атрибуции трафика.

## Интеграция библиотеки для получения рекламных идентификаторов {#enable}

Для получения рекламных идентификаторов AppMetrica SDK использует отдельную библиотеку `io.appmetrica.analytics:analytics-identifiers`. Эта библиотека содержит зависимость от `com.google.android.gms:play-services-ads-identifier:18.0.1`, которая используется для получения GAID. Версия библиотеки `io.appmetrica.analytics:analytics-identifiers` должна соответствовать версии библиотеки `io.appmetrica.analytics:analytics`.

{% note info %}

Зависимость от библиотеки `io.appmetrica.analytics:analytics-identifiers` добавляется по умолчанию.

{% endnote %}

### Исключение библиотеки рекламных идентификаторов из списка зависимостей {#disable}

Если получение рекламных идентификаторов нежелательно (например, для детских приложений), исключите библиотеку в файле `build.gradle` проекта:

{% list tabs %}

- build.gradle.kts

  ```kotlin translate=no
  configurations.configureEach {
      exclude(group = "io.appmetrica.analytics", module = "analytics-identifiers")
  }
  ```

- build.gradle

  ```groovy translate=no
  configurations.configureEach {
      exclude group: 'io.appmetrica.analytics', module: 'analytics-identifiers'
  }
  ```

{% endlist %}

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
