# Migrating to version 3.0.0

## AppMetrica SDK and AppMetrica Push SDK compatibility {#compatible-sdks}

We recommend using AppMetrica SDK version 3.0.0 and higher with AppMetrica Push SDK version 2.0.0.

## Migration guide {#instruction-for-migration}

Some of the classes [were renamed](#rename) to avoid a name conflict when updating native dependencies.

## Renamings {#rename}

- Renamed the `ReporterConfig` class as `AppMetricaReporterConfig`.
- Renamed the `Gender` class as `AppMetricaNameAttribute`.
- Renamed the `UserProfile` class as `AppMetricaUserProfile`.
- Renamed the `Reporter` class as `AppMetricaReporter`.
- Renamed the `ActivationConfigHolder` class as `AppMetricaActivationConfigHolder`. This is an internal API class and we discourage its use.
- Renamed the `AdType` class as `AppMetricaAdType`.
- Renamed the `setUpErrorHandling` class as `setUpErrorHandlingWithAppMetrica`. This is an internal API class and we discourage its use.
- Renamed the `setUpLogger` class as `setUpAppMetricaLogger`. This is an internal API class and we discourage its use.
- Renamed the `DeferredDeeplinkRequestException` class as `AppMetricaDeferredDeeplinkRequestException`.
- Renamed the `DeferredDeeplinkErrorReason` class as `AppMetricaDeferredDeeplinkErrorReason`.
- Renamed the `DeviceIdRequestException` class as `AppMetricaDeviceIdRequestException`.
- Renamed the `DeviceIdErrorReason` class as `AppMetricaDeviceIdErrorReason`.
- Renamed the `ECommerceAmount` class as `AppMetricaECommerceAmount`.
- Renamed the `ECommerceProduct` class as `AppMetricaECommerceProduct`.
- Renamed the `ECommercePrice` class as `AppMetricaECommercePrice`.
- Renamed the `ECommerceReferrer` class as `AppMetricaECommerceReferrer`.
- Renamed the `ECommerceScreen` class as `AppMetricaECommerceScreen`.
- Renamed the `ECommerceCartItem` class as `AppMetricaECommerceCartItem`.
- Renamed the `ECommerceOrder` class as `AppMetricaECommerceOrder`.
- Renamed the `ECommerce` class as `AppMetricaECommerce`.
- Renamed the `ECommerceEvent` class as `AppMetricaECommerceEvent`.
- Renamed the `Location` class as `AppMetricaLocation`.
- Renamed the `PreloadInfo` class as `AppMetricaPreloadInfo`.
- Renamed the `Receipt` class as `AppMetricaReceipt`.
- Renamed the `StartupParamsItemStatus` class as `AppMetricaStartupParamsItemStatus`.
- Renamed the `StartupParamsItem` class as `AppMetricaStartupParamsItem`.
- Renamed the `StartupParamsResult` class as `AppMetricaStartupParamsResult`.
- Renamed the `StartupParamsReason` class as `AppMetricaStartupParamsReason`.
- Renamed the `StartupParams` class as `AppMetricaStartupParams`.

**AdRevenue**

- Renamed the `AdRevenue` class as `AppMetricaAdRevenue`.

**Revenue**

- Renamed the `Revenue` class as `AppMetricaRevenue`.

**User attributes**

- Renamed the `BirthDateAttribute` class as `AppMetricaBooleanAttribute`.
- Renamed the `BooleanAttribute` class as `AppMetricaReporterConfig`.
- Renamed the `CounterAttribute` class as `AppMetricaCounterAttribute`.
- Renamed the `GenderAttribute` class as `AppMetricaGenderAttribute`.
- Renamed the `NotificationEnabledAttribute` class as `AppMetricaNotificationEnabledAttribute`.
- Renamed the `StringAttribute` class as `AppMetricaStringAttribute`.
