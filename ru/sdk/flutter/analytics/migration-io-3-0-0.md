# Миграция на версию 3.0.0

## Совместимость AppMetrica SDK и AppMetrica Push SDK {#compatible-sdks}

Для AppMetrica SDK версии 3.0.0 и выше рекомендуется использовать AppMetrica Push SDK версии 2.0.0.

## Руководство по миграции {#instruction-for-migration}

Некоторые классы [были переименованы](#rename), чтобы из-за обновления нативной зависимости не произошел конфликт имен.

## Переименование {#rename}

- Класс `ReporterConfig` переименован в `AppMetricaReporterConfig`.
- Класс `Gender` переименован в `AppMetricaNameAttribute`.
- Класс `UserProfile` переименован в `AppMetricaUserProfile`.
- Класс `Reporter` переименован в `AppMetricaReporter`.
- Класс `ActivationConfigHolder` переименован в `AppMetricaActivationConfigHolder`. Класс является внутренним API и не рекомендуется для использования.
- Класс `AdType` переименован в `AppMetricaAdType`.
- Класс `setUpErrorHandling` переименован в `setUpErrorHandlingWithAppMetrica`. Класс является внутренним API и не рекомендуется для использования.
- Класс `setUpLogger` переименован в `setUpAppMetricaLogger`. Класс является внутренним API и не рекомендуется для использования.
- Класс `DeferredDeeplinkRequestException` переименован в `AppMetricaDeferredDeeplinkRequestException`.
- Класс `DeferredDeeplinkErrorReason` переименован в `AppMetricaDeferredDeeplinkErrorReason`.
- Класс `DeviceIdRequestException` переименован в `AppMetricaDeviceIdRequestException`.
- Класс `DeviceIdErrorReason` переименован в `AppMetricaDeviceIdErrorReason`.
- Класс `ECommerceAmount` переименован в `AppMetricaECommerceAmount`.
- Класс `ECommerceProduct` переименован в `AppMetricaECommerceProduct`.
- Класс `ECommercePrice` переименован в `AppMetricaECommercePrice`.
- Класс `ECommerceReferrer` переименован в `AppMetricaECommerceReferrer`.
- Класс `ECommerceScreen` переименован в `AppMetricaECommerceScreen`.
- Класс `ECommerceCartItem` переименован в `AppMetricaECommerceCartItem`.
- Класс `ECommerceOrder` переименован в `AppMetricaECommerceOrder`.
- Класс `ECommerce` переименован в `AppMetricaECommerce`.
- Класс `ECommerceEvent` переименован в `AppMetricaECommerceEvent`.
- Класс `Location` переименован в `AppMetricaLocation`.
- Класс `PreloadInfo` переименован в `AppMetricaPreloadInfo`.
- Класс `Receipt` переименован в `AppMetricaReceipt`.
- Класс `StartupParamsItemStatus` переименован в `AppMetricaStartupParamsItemStatus`.
- Класс `StartupParamsItem` переименован в `AppMetricaStartupParamsItem`.
- Класс `StartupParamsResult` переименован в `AppMetricaStartupParamsResult`.
- Класс `StartupParamsReason` переименован в `AppMetricaStartupParamsReason`.
- Класс `StartupParams` переименован в `AppMetricaStartupParams`.

**AdRevenue**

- Класс `AdRevenue` переименован в `AppMetricaAdRevenue`.

**Revenue**

- Класс `Revenue` переименован в `AppMetricaRevenue`.

**Атрибуты пользователя**

- Класс `BirthDateAttribute` переименован в `AppMetricaBooleanAttribute`.
- Класс `BooleanAttribute` переименован в `AppMetricaReporterConfig`.
- Класс `CounterAttribute` переименован в `AppMetricaCounterAttribute`.
- Класс `GenderAttribute` переименован в `AppMetricaGenderAttribute`.
- Класс `NotificationEnabledAttribute` переименован в `AppMetricaNotificationEnabledAttribute`.
- Класс `StringAttribute` переименован в `AppMetricaStringAttribute`.
