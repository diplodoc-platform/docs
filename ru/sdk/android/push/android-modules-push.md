# Список опциональных модулей для Push SDK

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

## Модули, включенные по умолчанию {#default}

- `provider-firebase` — позволяет AppMetrica Push SDK работать с `com.google.firebase:firebase-messaging`.

## Модули, не включенные по умолчанию {#not-default}

- `plugin-adapter` — plugin для разработчиков.
- `provider-gcm` — позволяет AppMetrica Push SDK работать с `com.google.android.gms:play-services-gcm`.
- `provider-hms` — позволяет AppMetrica Push SDK работать с `com.huawei.hms:push`.
- `provider-rustore` — позволяет AppMetrica Push SDK работать с `ru.rustore.sdk:pushclient`.

Актуальный список модулей можно проверить на [github](https://github.com/appmetrica/push-sdk-android/blob/main/README.md).

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
