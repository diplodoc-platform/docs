# Получение рекламных идентификаторов

Рекламный идентификатор GAID — уникальный идентификатор сервисов Google Play для показа рекламы пользователям, которые согласны видеть персонализированные объявления. Пользователь может отключить персонализацию рекламы или сбросить идентификатор в настройках. В таком случае рекламные сети не смогут использовать его для подбора релевантной рекламы. Также значительно снизится точность атрибуции трафика.

## Интеграция библиотеки для получения рекламных идентификаторов {#enable}

Для получения рекламных идентификаторов плагин AppMetrica Unity SDK использует отдельную библиотеку `io.appmetrica.analytics:analytics-identifiers`. Эта библиотека содержит зависимость от `com.google.android.gms:play-services-ads-identifier:18.0.1`, которая используется для получения GAID. Версия библиотеки `io.appmetrica.analytics:analytics-identifiers` должна соответствовать версии библиотеки `io.appmetrica.analytics:analytics`.

{% note info "" %}

Зависимость от библиотеки `io.appmetrica.analytics:analytics-identifiers` добавляется по умолчанию.

{% endnote %}

### Исключение библиотеки рекламных идентификаторов из списка зависимостей {#disable}

Если получение рекламных идентификаторов нежелательно (например, для детских приложений), исключите библиотеку в Custom Launcher Gradle Template проекта (файл `Assets/Plugins/Android/launcherTemplate.gradle`). Если такого файла нет, проверьте Custom Gradle Template (файл `Assets/Plugins/Android/mainTemplate.gradle`).

```csharp translate=no
configurations.configureEach {
  exclude(group = "io.appmetrica.analytics", module = "analytics-identifiers")
}
```

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
