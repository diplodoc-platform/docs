# История изменений

## AppMetrica SDK {#sdk}

### Версия 6.4.0 {#v-6-4-0}

Релиз 4 марта 2025 г.

- Обновлена версия AppMetrica Android SDK до [7.7.0](../../sdk/android/changelog-android.md#s-7-7-0).
  - Исправлена возможная проблема со статистикой (установки и новые пользователи) при одновременном использовании плагинов AppMetrica SDK (Unity, ReactNative, Flutter) и плагинов Yandex Ads SDK.
  - Доработан механизм обработки реферрера, что позволило исправить ошибку получения отложенного диплинка и его параметров при установке приложения по трекинговой ссылке на последних версиях браузера с движком chromium (Google Chrome, Yandex Browser и т.д.).
  - Исправлено несколько возможных ANR и крэшей
- Обновлена версия AppMetrica iOS SDK до [5.9.0](../../sdk/ios/changelog-ios.md#v-5-9-0).
  - Устранён конфликт между AppMetricaProtobuf и другими библиотеками, использующими protobuf-c.
- Добавлена интеграция с AppHud для трекинга подписок

### Версия 6.3.0 {#v-6-3-0}

Релиз 19 сентября 2024 г.

- Обновлена версия AppMetrica Android SDK до [7.2.0](../../sdk/android/changelog-android.md#s-7-2-0).
  - Добавлена ускоренная отправка на сервер некоторых событий (атрибуций из внешних SDK, e-commerce, revenue, ad revenue (Impression Level Revenue Data)).
- Обновлена версия AppMetrica iOS SDK до [5.8.0](../../sdk/ios/changelog-ios.md#v-5-8-0).
  - Удалена поддержка работы iAd и ссылки на эту библиотеку.
  - Добавлено логирование параметров события [GitHub Issue #2](https://github.com/appmetrica/appmetrica-unity-plugin/issues/2).
  - Обновлена зависимость KSCrash до версии `2.0.0-rc.1`.
  - Удалены домены из `NSPrivacyTrackingDomains` в privacy манифесте `AppMetricaCore`.
  - Добавлена форсированная отправка определенных типов событий на сервер (атрибуций из внешних SDK, e-commerce, revenue, ad revenue (Impression Level Revenue Data), apple privacy).

### Версия 6.2.0 {#v-6-2-0}

Релиз 9 июля 2024 г.

- Обновлена версия AppMetrica Android SDK до [7.0.0](../../sdk/android/changelog-android.md#s-7-0-0).
  - Текущая версия `minSdkVersion` повышена до `21` (Android 5.0).
  - Версии `sourceCompatibility` и `targetCompatibility` повышены до Java 1.8.
  - Добавлен лимит в 100 событий, отправляемых в одном запросе на сервер. Введение лимита повысит производительность SDK в условиях нестабильного сетевого канала.
  - Оптимизирована работа с потоками на клиентской стороне и удалены устаревшие проверки корректности интеграции SDK. Оптимизация снизит время синхронной части активации SDK.
- Обновлена версия AppMetrica iOS SDK до [5.6.0](../../sdk/ios/changelog-ios.md#v-5-6-0).
  - Исправлена ошибка, связанная с отправкой IDFA. IDFA не всегда отправлялся сразу после получения согласия пользователя на трекинг. Это могло повлиять на отправку тестовых пушей по IDFA.
  - В Extensions теперь по умолчанию используется background сессия.
- Добавлена возможность отправки атрибуции из [Singular](../../data-collection/attribution-integration-unity#singular).

### Версия 6.1.0 {#v-6-1-0}

Релиз 15 мая 2024 г.

- Обновлена версия AppMetrica SDK ([Android 6.5.0](../../sdk/android/changelog-android.md#s-6-5-0), [iOS 5.3.2](../../sdk/ios/changelog-ios.md#v-5-3-2)).
- Добавлены вспомогательные классы, методы и поля для AppMetrica Push Unity Plugin:
   - В классе `AppMetrica` добавлены: делегат `ActivationListener`, поля `ActivationConfig` и `OnActivation`.
   - В классе `AppMetricaConfig` добавлен метод `ToJsonString`.
   - Добавлены внутренние классы: для Android — `AppMetricaPushHelper`, для iOS — `AMAUAppMetricaPushHelper`.

### Версия 6.0.1 {#v-6-0-1}

Релиз 25 апреля 2024 г.

- Исправлено падение при запуске сцены из Unity Editor [GitHub Issue #1](https://github.com/appmetrica/appmetrica-unity-plugin/issues/1).

### Версия 6.0.0 {#v-6-0-0}

Релиз 10 апреля 2024 г.

- Глобальное обновление плагина. Подробнее в [инструкции по миграции](analytics/migration-io-6-0-0.md).
- Обновлена версия AppMetrica SDK ([Android 6.4.0](../../sdk/android/changelog-android.md#s-6-4-0), [iOS 5.2.0](../../sdk/ios/changelog-ios.md#v-5-2-0)).
  - Поддержан Privacy Manifest в iOS.
- Поддержан [Unity Package Manager](https://docs.unity3d.com/Manual/Packages.html).
- Поддержан [Assembly definition](https://docs.unity3d.com/Manual/cus-asmdef.html).
- Удален префаб. Вместо него рекомендуется активировать AppMetrica используя [RuntimeInitializeOnLoadMethodAttribute](https://docs.unity3d.com/ScriptReference/RuntimeInitializeOnLoadMethodAttribute.html).
- Добавлен новый API отправки E-Commerce событий.
- Добавлен новый API для отправки событий на дополнительный APIKey.
- Добавлена поддержка отправки атрибуций из сторонних библиотек. Подробности в статье [Интеграция атрибуций из других SDK](../../data-collection/attribution-integration-unity.md).

### Версии 5.2.0 — 5.0.0

{% cut "5.2.0 — 5.0.0" %}

#### Версия 5.2.0 {#v-5-2-0}

Релиз 3 октября 2022 г.

- Обновлена версия AppMetrica SDK ([Android 5.2.0](../../sdk/android/changelog-android.md), [iOS 4.4.0](../../sdk/ios/changelog-ios.md)).
- Добавлен API AdRevenue для передачи доходов рекламной монетизации: класс `YandexAppMetricaAdRevenue` и метод для отправки AdRevenue `ReportAdRevenue(YandexAppMetricaAdRevenue adRevenue)`.

#### Версия 5.0.1 {#v-5-0-1}

Релиз 1 сентября 2022 г.

- Обновлена версия AppMetrica SDK ([Android 5.0.1]( ../../sdk/android/changelog-android.md)).
- Исключения из Application.logMessageReceived отправляются как ошибки.

#### Версия 5.0.0 {#v-5-0-0}

Релиз 16 июля 2022 г.

- Обновлена версия AppMetrica SDK ([Android 5.0.0]( ../../sdk/android/changelog-android.md)).
- Удален вызов `LocationService.Start`.
- Удалено использование `APP_METRICA_TRACK_LOCATION_DISABLED`.

{% endcut %}

### Версии 4.3.0 — 4.0.0

{% cut "4.3.0 — 4.0.0" %}

#### Версия 4.3.0 {#v-4-3-0}

Релиз 19 мая 2022 г.

- Обновлены версии AppMetrica SDK ([Android 4.2.0]( ../../sdk/android/changelog-android.md), [iOS 4.2.0](../../sdk/ios/changelog-ios.md)).
- Добавлена поддержка [External Dependency Manager for Unity](https://github.com/googlesamples/unity-jar-resolver) для разрешения зависимостей.
- Улучшена обработка крэшей.
- Добавлены методы для отправки ошибок: `ReportError(Exception exception, string condition)`, `ReportErrorFromLogCallback(string condition, string stackTrace)`.
- Добавлен метод для отправки крэшей `ReportUnhandledException(Exception exception)`.
- Метод `ReportError(string condition, string stackTrace)` устарел. Используйте метод `ReportError(Exception exception, string condition)`.
- Метод `ReportError(string groupIdentifier, string condition, string stackTrace)` устарел. Используйте метод `ReportError(string groupIdentifier, string condition, Exception exception)`.

#### Версия 4.2.0 {#v-4-2-0}

- Исправлена проблема с выгрузкой приложения в AppStore:

  ```
  YandexMobileMetrica.framework/YandexMobileMetrica' is not permitted. Your app can’t contain standalone executables or libraries, other than a valid CFBundleExecutable of supported bundles
  ```

#### Версия 4.1.0 {#v-4-1-0}

- Обновлены версии AppMetrica SDK ([Android 4.1.1]( ../../sdk/android/changelog-android.md)).

#### Версия 4.0.0 {#v-4-0-0}

- Обновлены версии AppMetrica SDK ([iOS 4.0.0](../../sdk/ios/changelog-ios.md), [Android 4.0.0]( ../../sdk/android/changelog-android.md)).
- Удалено свойство `YandexAppMetricaConfig.InstalledAppCollecting`.
- В класс [YandexAppMetricaConfig](analytics/methods.md#ClassYandexAppMetricaConfig) добавлено свойство `RevenueAutoTrackingEnabled` — признак автоматического сбора и отправки информации об In-App покупках.
- В AppMetrica SDK для Android добавлена зависимость от [Install Referrer Library](https://developer.android.com/google/play/installreferrer/library) 2.2.

{% endcut %}

### Версии 3.8.0 — 3.0.0

{% cut "3.8.0 — 3.0.0" %}

#### Версия 3.8.0 {#v-3-8-0}

- Обновлены версии AppMetrica SDK ([iOS 3.16.0](../../sdk/ios/changelog-ios.md), [Android 3.21.1]( ../../sdk/android/changelog-android.md)).
- Добавлен метод [RequestTrackingAuthorization](analytics/methods.md#idfa-request) для запроса доступа к IDFA на iOS.

#### Версия 3.7.0 {#v-3-7-0}

- Обновлены версии AppMetrica SDK ([iOS 3.14.0](../../sdk/ios/changelog-ios.md), [Android 3.18.0]( ../../sdk/android/changelog-android.md)).
- Добавлены методы:
    1. [void ReportEvent(string message, string json)](analytics/methods.md#ReportEvent) — отправляет событие со значением в виде json-строки.
    2. [void PutErrorEnvironmentValue(string key, string value)](analytics/methods.md#PutErrorEnvironmentValue) — задает окружение ошибки.
    3. [void ReportError(string groupIdentifier, string condition, string stackTrace)](analytics/methods.md#ReportEvent) и [void ReportError(string groupIdentifier, string condition, Exception exception)](analytics/methods.md#ReportEvent) — методы для отправки ошибок с идентификатором, по которому будут группироваться ошибки.

#### Версия 3.6.0 {#v-3-6-0}

- Обновлены версии AppMetrica SDK ([iOS 3.11.1](../../sdk/ios/changelog-ios.md), [Android 3.14.3]( ../../sdk/android/changelog-android.md)).
- Добавлена поддержка детских приложений. Для этого используйте свойство `AppForKids` класса [YandexAppMetricaConfig](analytics/methods.md#ClassYandexAppMetricaConfig).

#### Версия 3.5.1 {#v-3-5-1}

- Добавлен метод [ReportReferralUrl](analytics/methods.md#ReportReferralUrl).
- Добавлен метод [ReportAppOpen](analytics/methods.md#ReportAppOpen).
- Добавлена возможность упрощенного подключения iAd фреймворка для iOS. Подробнее в разделе [Трекинг кампаний Apple Search Ads](../../mobile-tracking/searchads-settings.md).
- Добавлено свойство PriceDecimal в класс [YandexAppMetricaRevenue](analytics/methods.md#YandexAppMetricaRevenue). Используйте его вместо устаревшего Price.

#### Версия 3.5.0 {#v-3-5-0}

- Обновлены версии AppMetrica SDK ([iOS 3.9.4](../../sdk/ios/changelog-ios.md), [Android 3.13.1]( ../../sdk/android/changelog-android.md)).

#### Версия 3.4.0 {#v-3-4-0}

- Обновлены версии AppMetrica SDK ([iOS 3.7.1](../../sdk/ios/changelog-ios.md), [Android 3.6.4]( ../../sdk/android/changelog-android.md)).

#### Версия 3.3.0 {#v-3-3-0}

- Обновлены версии AppMetrica SDK ([iOS 3.6.0](../../sdk/ios/changelog-ios.md), [Android 3.6.0]( ../../sdk/android/changelog-android.md)).

#### Версия 3.2.0 {#v-3-2-0}

- Обновлены версии AppMetrica SDK ([iOS 3.4.0](../../sdk/ios/changelog-ios.md), [Android 3.4.0]( ../../sdk/android/changelog-android.md)).
- Исправлена ошибка при интеграции AppMetrica Push SDK для iOS.

#### Версия 3.1.0 {#v-3-1-0}

- Обновлены версии AppMetrica SDK ([iOS 3.2.0](../../sdk/ios/changelog-ios.md), [Android 3.2.2]( ../../sdk/android/changelog-android.md)).
- Добавлен метод отключения отправки статистики.
- Добавлен метод получения уникального идентификатора AppMetrica (`appmetrica_device_id`).
- Добавлен метод принудительной отправки событий из буфера.

#### Версия 3.0.1 {#v-3-0-1}

- Обновлена версия AppMetrica SDK ([iOS 3.1.2](../../sdk/ios/changelog-ios.md)).
- Внесены изменения в SDK для соответствия требованиям Apple App Store Review Team. Обновите плагин для прохождения модерации в App Store.

#### Версия 3.0.0 {#v-3-0-0}

- Обновлены версии AppMetrica SDK ([iOS 3.1.1](../../sdk/ios/changelog-ios.md), [Android 3.1.0]( ../../sdk/android/changelog-android.md)).
- Добавлена возможность создания пользовательских профилей.
- Добавлен [трекинг покупок](analytics/unity-operations.md#send-revenue) в приложении.
- Изменены методы API.

{% endcut %}

## Push SDK {#push}

### Версия 2.0.0 {#p-2-0-0}

Релиз 15 мая 2024 г.

- Глобальное обновление плагина. Подробнее в [инструкции по миграции](push/migration-io-2-0-0.md).
- Обновлены версии AppMetrica Push SDK ([Android 3.3.0](../android/changelog-android.md#v-3-3-0), [iOS 2.0.0](../ios/changelog-ios.md#v-push-2-0-0)).
  - Поддержан Privacy Manifest в iOS.
- Прекращена поддержка плагина AppMetrica Unity ниже версии 6.1.0.
- Поддержан [Unity Package Manager](https://docs.unity3d.com/Manual/Packages.html).
- Поддержан [Assembly definition](https://docs.unity3d.com/Manual/cus-asmdef.html).
- Удален префаб. Вместо него рекомендуется активировать AppMetrica Push используя [RuntimeInitializeOnLoadMethodAttribute](https://docs.unity3d.com/ScriptReference/RuntimeInitializeOnLoadMethodAttribute.html).

### Версия 1.1.0 {#p-1-1-0}

Релиз 15 августа 2022 г.

- Обновлены версии AppMetrica Push SDK ([iOS 1.3.0](../ios/changelog-ios.md#push-sdk), [Android 2.2.0](../android/changelog-android.md)).
- Поддержана Unity 2022.1.
- Исправлена работа плагина на устройствах с Андроид 7 и ниже из-за ошибки `java.lang.NoClassDefFoundError: android.app.NotificationChannel`.

### Версии 1.0.0 — 0.1.0

{% cut "1.0.0 — 0.1.0" %}

#### Версия 1.0.0 {#p-1-0-0}

Релиз 27 мая 2022 г.

- Обновлены версии AppMetrica Push SDK ([iOS 1.1.1](../ios/changelog-ios.md#push-sdk), [Android 2.1.1](../android/changelog-android.md)).
- Прекращена поддержка плагина AppMetrica Unity ниже версии 4.0.0.
- Добавлена поддержка [External Dependency Manager for Unity](https://github.com/googlesamples/unity-jar-resolver) для разрешения зависимостей.

#### Версия 0.2.0 {#p-0-2-0}

Релиз 11 июля 2018 г.

- Обновлены версии AppMetrica Push SDK ([iOS 0.6.0](../ios/changelog-ios.md#push-sdk), [Android 1.1.0](../android/changelog-android.md)).
- Прекращена поддержка плагина AppMetrica Unity ниже версии 3.0.0.
- Прекращена поддержка iOS 7.

#### Версия 0.1.1 {#p-0-1-1}

Релиз 27 ноября 2017 г.

- Обновлены версии AppMetrica Push SDK ([iOS 0.5.0](../ios/changelog-ios.md#push-sdk), [Android 0.6.1](../android/changelog-android.md)).
- Добавлена поддержка Android 8.
- Добавлена поддержка отображения push-уведомлений в открытых приложениях для iOS 10 и выше.
- Обновлены версии GCM и support-библиотек для Android.
- Минимальная версия Android API — 14.

#### Версия 0.1.0 {#p-0-1-0}

Релиз 31 января 2017 г.

- Произведена интеграция с AppMetrica Push SDK для платформ iOS и Android.

{% endcut %}
