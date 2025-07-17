# Список модулей

## Опциональные модули {#optional-modules}

Перечисленные ниже модули опциональные и при необходимости могут быть принудительно исключены из AppMetrica SDK. Чтобы отключить их, добавьте в файл `app/build.gradle.kts` или `app/build.gradle` следующий код:

{% list tabs %}

- build.gradle.kts

    ```kotlin translate=no
    configurations.configureEach {
        exclude(group = "io.appmetrica.analytics", module = "analytics-{module_name}")
    }
    ```

- build.gradle

   ```groovy translate=no
   configurations.configureEach {
       exclude group: 'io.appmetrica.analytics', module: 'analytics-{module_name}'
   }
   ```

{% endlist %}

- `ad-revenue` — включает все модули Ad-Revenue из AppMetrica SDK.
- `ad-revenue-admob-v23` — добавляет хэндлер для событий Ad-Revenue из `com.google.android.gms:play-services-ads`.
- `ad-revenue-applovin-v12` — добавляет хэндлер для событий Ad-Revenue из `com.applovin:applovin-sdk`.
- `ad-revenue-fyber-v3` — добавляет хэндлер для событий Ad-Revenue из `com.fyber:fairbid-sdk`.
- `ad-revenue-ironsource-v7` — позволяет AppMetrica SDK получать события Ad-Revenue из `com.ironsource.sdk:mediationsdk`.
- `apphud` — добавляет интеграцию с `com.apphud:ApphudSDK-Android`.
- `appsetid` — позволяет AppMetrica SDK получать App Set ID.
- `identifiers` — позволяет AppMetrica SDK получать ADV ID.
- `location` — позволяет AppMetrica SDK получать геолокацию.
- `ndkcrashes` — позволяет AppMetrica SDK управлять нативными крэшами на Android.
- `screenshot` — позволяет AppMetrica SDK получать события снятия скриншотов.

## Модули с опциональными зависимостями {#optional-dependencies}

Перечисленные ниже модули не опциональные, но для корректной работы используют внешние зависимости. Эти зависимости перечислены в README-файлах модулей.

- `billing-v6` — обертка для `com.android.billingclient:billing`.
- `gpllibrary` — обертка для `com.google.android.gms:play-services-location`.

## Зависимости {#module-dependencies}

Список зависимостей и поддерживаемые версии модулей можно посмотреть в файле [dependencies_versions.yaml](https://github.com/appmetrica/appmetrica-sdk-android/blob/main/dependencies_versions.yaml) на github.

Актуальный список модулей также можно проверить на [github](https://github.com/appmetrica/appmetrica-sdk-android/blob/main/README.md).

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
