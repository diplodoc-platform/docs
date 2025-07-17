# История изменений

## Версия 3.3.0 {#v-3-3-0}

Релиз 4 октября 2024 г.

- В AppMetrica появилась возможность [импорта атрибуций из других SDK](../../data-collection/attribution-integration-react.md).

## Версия 3.2.0 {#v-3-2-0}

Релиз 25 сентября 2024 г.

- Обновлена версия AppMetrica Android SDK до [7.2.0](../../sdk/android/changelog-android.md#s-7-2-0).
  - Добавлена ускоренная отправка на сервер некоторых событий (атрибуций из внешних SDK, e-commerce, revenue, ad revenue (Impression Level Revenue Data)).
- Обновлена версия AppMetrica iOS SDK до [5.8.0](../../sdk/ios/changelog-ios.md#v-5-8-0).
  - Удалена поддержка работы iAd и ссылки на эту библиотеку.
  - Добавлено логирование параметров события.
  - Обновлена зависимость KSCrash до версии `2.0.0-rc.1`.
  - Удалены домены из `NSPrivacyTrackingDomains` в privacy манифесте `AppMetricaCore` [GitHub Issue #4](https://github.com/appmetrica/appmetrica-react-native-plugin/issues/4).
  - Добавлена форсированная отправка определенных типов событий на сервер (атрибуций из внешних SDK, e-commerce, revenue, ad revenue (Impression Level Revenue Data), apple privacy).

## Версия 3.1.0 {#v-3-1-0}

Релиз 11 июля 2024 г.

- Обновлена версия AppMetrica Android SDK до [7.0.0](../../sdk/android/changelog-android.md#s-7-0-0).
   - Текущая версия `minSdkVersion` повышена до `21` (Android 5.0).
   - Версии `sourceCompatibility` и `targetCompatibility` повышены до Java 1.8.
   - Добавлен лимит в 100 событий, отправляемых в одном запросе на сервер. Введение лимита повысит производительность SDK в условиях нестабильного сетевого канала.
   - Оптимизирована работа с потоками на клиентской стороне и удалены устаревшие проверки корректности интеграции SDK. Оптимизация снизит время синхронной части активации SDK.
- Обновлена версия AppMetrica iOS SDK до [5.6.0](../../sdk/ios/changelog-ios.md#v-5-6-0).
   - В Extensions теперь по умолчанию используется background сессия.
- Поддержан API отправки [пользовательских профилей](analytics/react-native-operations.md#send-attribute-profile).
- Исправлена отправка `payload` в `ECommerce` и `AdRevenue` событий, когда он был задан как `Map<string, string>`.
- Поддержан тип `Record<string, string>` для `payload` в `ECommerce` и `AdRevenue` событий.

## Версия 3.0.0 {#v-3-0-0}

Релиз 10 июня 2024 г.

- Глобальное обновление плагина. Подробнее в [инструкции по миграции](analytics/migration-io-3-0-0.md). 
- Добавлено описание [подключения AppMetrica SDK](../../sdk/react-native/analytics/quick-start.md#integration) в приложения на React Native Expo. 
- Обновлена версия AppMetrica SDK ([Android 6.5.0](../../sdk/android/changelog-android.md#s-6-5-0), [iOS 5.4.0](../../sdk/ios/changelog-ios.md#v-5-4-0)).
   - Поддержан Privacy Manifest в iOS.
- Добавлен API отправки E-Commerce событий.
- Добавлен API отправки Revenue событий.
- Добавлен API отправки AdRevenue событий.
- Исправлена ошибка, из-за которой старт сессий на Android не всегда отслеживался.
- Добавлен автотрекинг диплинков.

## Версия 2.0.0 {#v-2-0-0}

Релиз 8 июня 2020 г.

- Интеграция с AppMetrica SDK для платформ iOS и Android.
