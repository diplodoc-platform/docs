# Миграция на версию 3.0.0

Миграция приложения с `com.yandex.android:mobmetricapushlib` на `io.appmetrica.analytics:push` не должна вызвать проблем.

## Одновременное использование 2 версий AppMetrica Push SDK

Так как были переименованы группа и названия основных артефактов, может сложиться ситуация, при которой в одном приложении будут использоваться сразу 2 версии AppMetrica Push SDK: `com.yandex.android:mobmetricapushlib` и `io.appmetrica.analytics:push`.

{% note alert %}

Это делать не рекомендуется, так как может приводить к аномалиям в отчетах.

{% endnote %}

## Руководство по миграции

Руководство содержит примеры, демонстрирующие различия между версиями SDK версий `2.3.3` и `3.0.0`.
В разделе рассматриваются только те методы, в которых нарушена обратная совместимость.

Для миграции на новую версию необходимо выполнить следующие шаги

1. Убедиться, что используется AppMetrica SDK версии не ниже `io.appmetrica.analytics:analytics:6.0.0`.
2. Поменять зависимость `com.yandex.android:mobmetricapushlib:2.3.3` на `io.appmetrica.analytics:push:3.0.0`.
3. В коде проекта заменить те, классы и методы, которые были просто переименованы или поменяли только пакет.
   Необходимые изменения указаны в [пункте про переименование классов](#rename_classes).
4. Код с остальными ошибками временно закомментировать чтобы проект можно было собрать.
5. Поменять `exclude` правила, если они имелись.
   Необходимые изменения указаны в [пункте про переименование зависимостей](#rename_dep).
6. Исправить закомментированный код, используя остальные пункты данной инструкции.
   При возникновении вопросов написать в поддержку.

### Переименованные зависимости {#rename_dep}

* Модуль `com.yandex.android:mobmetricapushlib` переименован в `io.appmetrica.analytics:push`.
* Модуль `com.yandex.android:appmetricapush-provider-firebase` переименован в `io.appmetrica.analytics:push-provider-firebase`.
* Модуль `com.yandex.android:appmetricapush-provider-hms` переименован в `io.appmetrica.analytics:push-provider-hms`.
* Модуль `com.yandex.android:appmetricapush-provider-rustore` переименован в `io.appmetrica.analytics:push-provider-rustore`.
* Модуль `com.yandex.android:appmetricapush-core` распался на `io.appmetrica.analytics:push-core-utils` и `io.appmetrica.analytics:push-provider-api`.

### Переименованные классы {#rename_classes}

* Класс `com.yandex.metrica.push.TokenUpdateListener` переименован в `io.appmetrica.analytics.push.TokenUpdateListener`.
* Класс `com.yandex.metrica.push.YandexMetricaPush` переименован в `io.appmetrica.analytics.push.AppMetricaPush`.
    * изменена константа `EXTRA_ACTION_INFO`.
    * метод `getToken` удален.
    * метод `init` переименован в `activate`.
* Класс `com.yandex.appmetrica.push.firebase.FirebasePushServiceControllerProvider` переименован в `io.appmetrica.analytics.push.provider.firebase.FirebasePushServiceControllerProvider`.
* Класс `com.yandex.appmetrica.push.hms.HmsPushServiceControllerProvider` переименован в `io.appmetrica.analytics.push.provider.hms.HmsPushServiceControllerProvider`.
* Класс `com.yandex.appmetrica.push.hms.MetricaHmsMessagingService` переименован в `io.appmetrica.analytics.push.provider.hms.AppMetricaHmsMessagingService`.
* Класс `com.yandex.appmetrica.push.rustore.MetricaRuStoreMessagingService` переименован в `io.appmetrica.analytics.push.provider.rustore.AppMetricaRuStoreMessagingService`.
* Класс `com.yandex.appmetrica.push.rustore.RuStorePushServiceControllerProvider` переименован в `io.appmetrica.analytics.push.provider.rustore.RuStorePushServiceControllerProvider`.
* Класс `com.yandex.metrica.push.common.core.PushServiceControllerProvider` переименован в `io.appmetrica.analytics.push.provider.api.PushServiceControllerProvider`.
* Класс `com.yandex.metrica.push.common.core.PushServiceController` переименован в `io.appmetrica.analytics.push.provider.api.PushServiceController`.
* Класс `com.yandex.metrica.push.firebase.MetricaMessagingService` переименован в `io.appmetrica.analytics.push.provider.firebase.AppMetricaMessagingService`.

Класс `io.appmetrica.analytics.push.provider.firebase.AppMetricaMessagingService` вынесен в отдельную [зависимость](android-other-push-services-settings.md#dependencies).

### Другое

* Дефолтный канал уведомлений переименован в `appmetrica_push`.
  Старые дефолтные каналы не удаляются.

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
