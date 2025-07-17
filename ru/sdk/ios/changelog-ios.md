# История изменений

## AppMetrica SDK {#sdk}

### Версия 5.11.0 {#v-5-11-0}

Релиз 22 Мая 2025 г.

- Добавлена поддержка двойного экранирования для reattribution параметров.
- Добавлена поддержка для будущего автосбора ad revenue данных из плагинов.
- Локация, переданная приложением через API `AppMetrica.setCustomLocation(Location)`, будет отправляться с событиями, даже если отключить трекинг гео в конфигурации: `AppMetrica.setLocationTrackingEnabled(Boolean)`, `AppMetricaConfiguration.setLocationTracking(Boolean)`.

### Версия 5.10.0 {#v-5-10-0}

Релиз 21 Апреля 2025 г.

- Исправлена ошибка отката счетчика сессий при последовательной миграции на версию 5.0 и последующем обновлении до 5.8.0 и выше.
- Добавлена возможность отключения использования IDFA в модуле `AppMetricaLibraryAdapter`.
- Добавлен модуль `AppMetricaScreenshot` для отслеживания факта создания скриншота пользователем.
- Обновлена зависимость KSCrash до версии 2.0.0.
- Миграция с алгоритма хеширования MD5 на SHA256.
- В enum AMAAdType добавлено новое значение `AppOpen`.
- Исправлена ошибка при отправке внутренних событий `TransactionFailure`, повышена надежность доставки отчетов о сбоях.
- Минимальная версия deployment_target для iOS и tvOS увеличена до 13.0.

### Версия 5.9.0 {#v-5-9-0}

Релиз 12 Декабря 2024 г.

- Реализован обмен идентификаторов между приложением и его расширением.
- Устранен конфликт между `AppMetricaProtobuf` и другими библиотеками, использующими `protobuf-c`.
- Улучшена детализация внутренних сообщений об ошибках.
- Улучшена валидация app environment.

### Версия 5.8.2 {#v-5-8-2}

Релиз 25 Октября 2024 г.

- Технический релиз.

### Версия 5.8.1 {#v-5-8-1}

Релиз 3 Октября 2024 г.

- Исправлена ошибка отправки `EVENT_UPDATE` вместо `EVENT_INIT` на 42 API key.

### Версия 5.8.0 {#v-5-8-0}

Релиз 3 Сентября 2024 г.

- Обновлена зависимость KSCrash до версии `2.0.0-rc.1`.
- Удалены домены из NSPrivacyTrackingDomains в privacy манифесте AppMetricaCore.
- Добавлен адаптер AppMetricaLibraryAdapter для интеграции со сторонними библиотеками.
- Добавлена форсированная отправка определенных типов событий на сервер (external SDKs attribution, e-commerce, revenue, ad revenue (Impression Level Revenue Data), apple privacy).

### Версия 5.7.1 {#v-5-7-1}

Релиз 7 Ноября 2024 г.

- Удалены домены из NSPrivacyTrackingDomains в privacy манифесте AppMetricaCore.

### Версия 5.7.0 {#v-5-7-0}

Релиз 3 Августа 2024 г.

- Удалена поддержка работы iAd и ссылки на эту библиотеку.
- Добавлено логирование параметров события.

### Версия 5.6.0 {#v-5-6-0}

Релиз 27 Июня 2024 г.

- В `AppMetricaConfiguration` добавлено свойство `appEnvironment`, позволяющее установить окружение приложения для всех событий с момента активации.

### Версия 5.5.0 {#v-5-5-0}

Релиз 26 Июня 2024 г.

- В Extensions теперь по умолчанию используется background сессия.
- В AppMetricaCrashes добавлена утилита для загрузки dSYM файлов.

### Версия 5.4.0 {#v-5-4-0}

Релиз 24 мая 2024 г.

- Исправлена ошибка, связанная с отправкой IDFA. IDFA не всегда отправлялся сразу после получения согласия пользователя на трекинг. Это могло повлиять на отправку тестовых пушей по IDFA.

### Версия 5.3.2 {#v-5-3-2}

Релиз 13 мая 2024 г.

- Исправлен крэш в `[AMAReportersContainer restartPrivacyTimer]`.
- По умолчанию отключены логи в файл из-за возможности крэша при нехватке места на диске.

### Версия 5.3.1 {#v-5-3-1}

Релиз 6 мая 2024 г.

- Исправлена ошибка валидации модулей AppMetrica_FMDB , AppMetrica_Protobuf в AppStore при поставке через SPM.

### Версия 5.3.0 {#v-5-3-0}

Релиз 26 апреля 2024 г.

- Поддержка Singular для внешних атрибуций: добавлена возможность отправки атрибуции из Singular:
  ```
  AppMetrica.reportExternalAttribution(attributionData, from: .singular) { error in
      print("AppMetrica reporting error: \(error)")
  }
  ```
- Исправление assert: Удаление внутренних assert для оптимизации кода и предотвращения возможных ошибок во время разработки.
- Обновление KSCrash: строгая зависимость от библиотеки KSCrash изменена на диапазон версий ~> 1.17.0.

### Версия 5.2.0 {#v-5-2-0}

Релиз 16 апреля 2024 г.

- В AppMetrica появилась возможность [импорта атрибуций из других SDK](../../data-collection/attribution-integration.yaml) для iOS.
- Для работы с внешней атрибуцией добавлены: метод `AppMetrica.reportExternalAttribution(_:from:onFailure:)` ([Swift](../ios/analytics/swift/AppMetrica.md#method_reportexternalattribution__from__onfailure), [Objective-C](../ios/analytics/objectivec/AMAAppMetrica.md#method_reportexternalattribution__source__onfailure)), struct/typedef `AttributionSource` ([Swift](../ios/analytics/swift/AttributionSource.md), [Objective-C](../ios/analytics/objectivec/AMAAttributionSource.md)).

### Версия 5.1.0 {#v-5-1-0}

Релиз 6 марта 2024 г.

- Добавлена поддержка [Privacy Manifest](https://developer.apple.com/documentation/bundleresources/privacy_manifest_files).

### Версия 5.0.0 {#v-5-0-0}

Релиз 13 февраля 2024 г.

- Обновлены идентификатор библиотеки и API. Подробнее в [инструкции по миграции](analytics/migration-io-5-0-0.md).

### Версия 4.5.2 {#v-4-5-2}

Релиз 22 мая 2023 г.

- Исправлен `posix_spawn` крэш Xcode с включенным санитайзером.

### Версия 4.5.0 {#v-4-5-0}

Релиз 21 марта 2023 г.

- Исправлена ошибка `locationServicesEnabled invoked on the main thread` на iOS 16.

### Версия 4.4.0 {#v-4-4-0}

Релиз 19 сентября 2022 г.

- Добавлен API AdRevenue для передачи доходов рекламной монетизации на уровне показа (Impression-Level Revenue Data):
    - классы `YMMAdRevenueInfo`, `YMMMutableAdRevenueInfo`.
    - методы `reportAdRevenue` в классе `YMMYandexMetrica`, `reportAdRevenue` в протоколе `YMMYandexMetricaReporting`.
    - перечисление `YMMAdType`.

### Версия 4.2.0 {#v-4-2-0}

Релиз 18 февраля 2022 г.

- Добавлен новый API для отслеживания крэшей и ошибок из произвольных плагинов.

    Протоколы:
    - `YMMYandexMetricaPlugins`.
    - `YMMYandexMetricaPluginReporting`.

    Классы:
    - `YMMPluginErrorDetails`.
    - `YMMStackTraceElement`.

- Добавлен API для полноценной работы SDK в контексте автотрекинга сессий при условии активации из плагинов: `YMMYandexMetricaPlugins.handlePluginInitFinished`.
- Добавлена возможность отправлять ошибки из репортеров без активации главного ключа. В этом случае будет отсутствовать мета-инфоромация из KSCrash (данные о системе).

### Версии 4.0.0 — 3.0.0

{% cut "4.0.0 — 3.0.0" %}

#### Версия 4.0.0 {#v-4-0-0}

Релиз 20 сентября 2021 г.

- Поддержана возможность задавать идентификатор пользовательского профиля при активации (`[YMMYandexMetricaConfiguration userProfileID]`) или до активации (`[YMMYandexMetrica setUserProfileID]`) главного ключа, а также при активации репортера (`[YMMReporterConfiguration userProfileID]`).
- Добавлено свойство `appOpenTrackingEnabled` для автоматического трекинга открытия приложения по deeplink.
- Добавлено свойство `revenueAutoTrackingEnabled` для автоматического сбора данных по in-app покупкам.
- Добавлено [управление Conversion Value](../../mobile-tracking/conversion-value.md).

#### Версия 3.17.0 {#v-3-17-0}

Релиз 8 июня 2021 г.

- Исправлена возможная ошибка
   ```
   Main Thread Checker: UI API called on a background thread: -[WKUserScript initWithSource:injectionTime:forMainFrameOnly:]
   ```
- Добавлена версия библиотеки для симуляторов iOS, запускаемых на Mac c процессорами Apple Silicon M1 (`ios-arm64-simulator`).
- Библиотека поставляется теперь только в виде XCFramework, что повлекло следующие изменения:
    - Минимальные поддерживаемые версии CocoaPods — 1.10, Carthage — 0.38. В этих версиях добавлена поддержка XCFramework.
    - Подключение AppMetrica SDK на tvOS теперь выполняется также, как на iOS: сабспеки `YandexMobileMetrica/Dynamic-TV` и `YandexMobileMetrica/Static-TV` больше недоступны.

#### Версия 3.16.0 {#v-3-16-0}

Релиз 27 мая 2021 г.

- Добавлен метод `initWebViewReporting` для отправки событий из JS-кода WebView.
- Исправлены ошибки и повышена стабильность.

#### Версия 3.15.1 {#v-3-15-1}

Релиз 20 апреля 2021 г.

- Доработана атрибуция Apple Search Ads через AdServices Framework. Обновитесь на эту версию, чтобы сохранить трекинг Apple Search Ads на iOS 14.5+.

#### Версия 3.15.0 {#v-3-15-0}

Релиз 30 марта 2021 г.

- Добавлена поддержка атрибуции установок на устройствах с версией iOS 14.5+ через [SKAdNetwork](https://developer.apple.com/documentation/storekit/skadnetwork). Передача ценности конверсии будет реализована в следующих версиях SDK.
- Добавлено получение данных, необходимых для атрибуции установок из Apple Search Ads через [AdServices Framework](https://developer.apple.com/documentation/adservices) (для устройств с версией iOS 14.3+). Атрибуция реализуется в серверной части AppMetrica и не потребует повторного обновления.
- Отключен сбор Оператора и Типа соединений.

#### Версия 3.14.0 {#v-3-14-0}

Релиз 29 декабря 2020 г.

- Добавлена дистрибуция AppMetrica с помощью Swift Package Manager. Подробности можно узнать в статье [Подключение и инициализация](analytics/quick-start.md).
- Минимальная поддерживаемая версия iOS 9.0.
- Исправлена проблема привязки крэша к сессии.

#### Версия 3.12.0 {#v-3-12-0}

Релиз 14 октября 2020 г.

- Добавлен новый API отправки E-Commerce событий:
    - В класс `YMMYandexMetrica` и протокол `YMMYandexMetricaReporting` добавлен метод `+reportECommerce:onFailure:`.
    - Добавлены новые классы:
       - `YMMECommerce`.
       - `YMMECommerceAmount`.
       - `YMMECommerceCartItem`.
       - `YMMECommerceOrder`.
       - `YMMECommercePrice`.
       - `YMMECommerceProduct`.
       - `YMMECommerceReferrer`.
       - `YMMECommerceScreen`.

    Подробнее о E-Commerce событиях в разделе [ECommerce](../../data-collection/about-ecommerce.md).

- Повышены производительность и качество статистических данных.

#### Версия 3.11.1 {#v-3-11-1}

Релиз 8 июля 2020 г.

- Добавлен новый API отправки крэшей и ошибок:
    - класс `YMMError`.
    - протокол `YMMErrorRepresentable`.
    - перечисление `YMMErrorReportingOptions`.
    - константа `YMMBacktraceErrorKey`.
    - в класс `YMMYandexMetrica` и протокол `YMMYandexMetricaReporting` добавлены методы:
       - `+reportError:onFailure:`.
       - `+reportError:options:onFailure:`.
       - `+reportNSError:onFailure:`.
       - `+reportNSError:options:onFailure:`.
       - `+setErrorEnvironmentValue:forKey:`.
    - В классы `YMMYandexMetricaConfiguration`, `YMMReporterConfiguration` и `YMMMutableReporterConfiguration` добавлено свойство `maxReportsInDatabaseCount`.
- Прекращена поддержка метода `+reportError:exception:onFailure:`. Используйте вместо него новые методы `+reportError:onFailure:`, `+reportError:options:onFailure:`, `+reportNSError:onFailure:` или `+reportNSError:options:onFailure:`.
- Добавлена поддержка детских приложений. Для этого используйте свойство `appForKids` конфигурации `YMMYandexMetricaConfiguration`. Подробнее в разделе [Примеры использования](analytics/ios-operations.md).
- Исправлена поддержка tvOS.
- Повышены производительность и качество статистических данных.

#### Версия 3.9.4 {#v-3-9-4}

Релиз 3 февраля 2020 г.

- Исправлены крэши, которые могли возникать в AppMetrica SDK 3.9.1 и 3.9.2.

#### Версия 3.9.2 {#v-3-9-2}

Релиз 27 декабря 2019 г.

- Исправлена генерация неправильного `appmetrica_device_id`.
- Исправлен возможный дэдлок при активации.
- Возобновлена поддержка метода `reportReferralUrl`.
- Исправлена ошибка с получением информации о `code` и `sudcode` для Mach-крэшей.
- Исправлена ошибка фреймворка для tvOS.
- Повышены производительность и качество статистических данных.

#### Версия 3.8.2 {#v-3-8-2}

Релиз 4 октября 2019 г.

- Исправлена ошибка сериализации `priceDecimal`, которая приводила к появлению отрицательных значений Revenue.

#### Версия 3.8.1 {#v-3-8-1}

Релиз 30 сентября 2019 г.

- Исправлена ошибка в динамическом фреймворке.
- Исправлен сбор информации о местоположении. При установке собственного местоположения отключается автоматическое определение.

#### Версия 3.8.0 {#v-3-8-0}

Релиз 25 сентября 2019 г.

- Добавлен инструмент командной строки `helper` для [Загрузка dSYM-файлов на iOS](../../data-collection/upload-dsym.md).

#### Версия 3.7.1 {#v-3-7-1}

Релиз 11 июля 2019 г.

- В класс `YMMRevenueInfo` добавлены:
    - Метод `-initWithPriceDecimal:currency:`. Используйте его вместо устаревшего `‑initWithPrice:currency:`.
    - Метод `-initWithPriceDecimal:currency:quantity:productID:transactionID:receiptData:payload:`. Используйте его вместо устаревшего `-initWithPrice:currency:quantity:productID:transactionID:receiptData:payload:`.
    - Свойство `priceDecimal`. Используйте его вместо устаревшего `price`.
    
- В класс `YMMYandexMetrica` добавлены методы для ручного контроля сессий:
    - Метод `+pauseSession:`.
    - Метод `+resumeSession:`.
    
- В класс `YMMYandexMetricaConfiguration` добавлены свойства для контроля сессий:
    - Свойство `handleActivationAsSessionStart`.
    - Свойство `sessionsAutoTracking`.
- Прекращена поддержка метода `+reportReferralUrl:`. Метод устарел.
- Исправлена ошибка с дополнительной информацией в крэш-логах: `active_time_since_launch`, `active_time_since_last_crash` и т. д.

#### Версия 3.6.0 {#v-3-6-0}

Релиз 18 февраля 2019 г.

- Исправлена потенциальная потеря сообщений о крэшах на устройствах с 32-разрядным процессором.
- Исправлена ошибка, которая влияла на работу AppMetrica SDK версий 3.1.0–3.5.0.
- Повышены производительность и качество статистических данных.

#### Версия 3.5.0 {#v-3-5-0}

Релиз 25 декабря 2018 г.

- Добавлена поддержка tvOS 9 и выше.
- Повышены производительность и качество статистических данных.

#### Версия 3.4.1 {#v-3-4-1}

Релиз 15 ноября 2018 г.

- Исправлена [проблема](https://github.com/yandexmobile/metrica-sdk-ios/issues/76) с подключением статического фреймворка в проект на Swift.

#### Версия 3.4.0 {#v-3-4-0}

Релиз 2 ноября 2018 г.

- Библиотека разделена на два фреймворка: один содержит основной функционал SDK, другой — обработку крэшей. Подробнее в разделе [Подключение и инициализация](../ios/analytics/quick-start.md).
- Исправлена работа метода `+sendEventsBuffer:` в фоне.
- Повышены производительность и качество статистических данных.

#### Версия 3.3.0 {#v-3-3-0}

Релиз 6 сентября 2018 г.

- Улучшена обработка информации, которая передается методами `+reportUserProfile:onFailure:` и `+reportRevenue:onFailure:`.
- Повышены производительность и качество статистических данных.

#### Версия 3.2.0 {#v-3-2-0}

Релиз 20 июля 2018 г.

- Добавлен метод `+setStatisticsSending:` для отключения отправки статистики.
- Добавлен метод `+requestAppMetricaDeviceIDWithCompletionQueue:block:` для получения уникального идентификатора AppMetrica (`appmetrica_device_id`).
- Добавлен метод `+sendEventsBuffer:` для принудительной отправки событий из буфера.
- Повышены производительность и качество статистических данных.

#### Версия 3.1.2 {#v-3-1-2}

Релиз 2 июля 2018 г.

- Внесены изменения в SDK для соответствия требованиям Apple App Store Review Team. Обновите AppMetrica SDK для прохождения модерации в App Store.

    {% note alert %}

    Предыдущие версии iOS SDK (2.8.0–3.1.1) недоступны для скачивания. Если вы используете библиотеку версии 2.9.х, обновите SDK до версии 2.9.8.

    {% endnote %}

#### Версия 3.1.1 {#v-3-1-1}

Релиз 13 июня 2018 г.

- Исправлена проблема в AppMetrica SDK 3.1.0, связанная с потерей внутренних данных.

#### Версия 3.1.0 {#v-3-1-0}

Релиз 8 июня 2018 г.

- Добавлена возможность атрибуции через deeplink (Re-engagement).
- Исправлен возможный дэдлок, затронувший версии AppMetrica SDK 3.0.0 и 3.0.1.
- Повышены производительность и качество статистических данных.

#### Версия 3.0.1 {#v-3-0-1}

Релиз 21 мая 2018 г.

- Повышена стабильность работы библиотеки.

#### Версия 3.0.0 {#v-3-0-0}

Релиз 18 апреля 2018 г.

- Добавлена возможность создания пользовательских профилей.
- Добавлен трекинг покупок в приложении.
- Изменены методы API.
- Изменен порядок представления информации в отчетах по крэшам (для соответствия формату Apple).
- Расширено логирование для событий.
- Прекращена поддержка iOS 6 и iOS 7.
- Повышены производительность и качество статистических данных.

{% endcut %}

## Push SDK {#push}

### Версия 3.1.0 {#v-push-3-1-0}

Релиз 15 мая 2025 г.

- Deployment target обновлен для версии iOS 13.

### Версия 3.0.2 {#v-push-3-0-2}

Релиз 27 февраля 2025 г.

- Исправлено открытие url.

### Версия 3.0.0 {#v-push-3-0-0}

Релиз 17 января 2025 г.

- Убран режим работы через App Group. Поддерживается только режим работы, при котором события отправляются напрямую в AppMetrica (требуется [настройка](analytics/ios-appgroup.md)). 
- Обновлена зависимость: AppMetrica-5.9.0.

### Версия 2.2.1 {#v-push-2-2-1}

Релиз 1 ноября 2024 г.

- Технический релиз.

### Версия 2.2.0 {#v-push-2-2-0}

Релиз 10 октября 2024 г.

- Добавлена возможность удалять уведомления через silent-пуши.

### Версия 2.1.0 {#v-push-2-1-0}

Релиз 23 сентября 2024 г.

- Повышена частота отправки пуш-событий доставки.

### Версия 2.0.0 {#v-push-2-0-0}

Релиз 15 апреля 2024 г.

- Обновлены идентификатор библиотеки и API. Библиотека разделена на модули. Подробнее в [инструкции по миграции](push/migration-io-push-2-0-0.md).
- Добавлена поддержка [Privacy Manifest](https://developer.apple.com/documentation/bundleresources/privacy_manifest_files).

### Версия 1.3.0 {#v-push-1-3-0}

Релиз 1 июля 2022 г.

- Добавлен метод `YMPYandexMetricaPush.handleSceneWillConnectToSession` для работы с [UIScene](https://developer.apple.com/documentation/uikit/uiscene) (с iOS версии 13 и выше).

### Версия 1.1.1 {#v-push-1-1-1}

Релиз 29 сентября 2021 г.

- Добавлена поддержка AppMetrica SDK [4.0.0](#v-4-0-0).

### Версии 1.0.0 — 0.3.0

{% cut "1.0.0 — 0.3.0" %}

#### Версия 1.0.0 {#v-push-1-0-0}

Релиз 13 июля 2021 г.

- Минимальная поддерживаемая версия iOS 9.0.
- Библиотека поставляется теперь только в виде XCFramework, что повлекло следующие изменения:
    - Минимальные поддерживаемые версии CocoaPods — 1.10, Carthage — 0.38. В этих версиях добавлена поддержка XCFramework.
- Добавлена версия библиотеки для симуляторов iOS, запускаемых на Mac c процессорами Apple Silicon M1 (`ios-arm64-simulator`).
- Добавлена дистрибуция Push SDK с помощью Swift Package Manager. Подробности можно узнать в статье [Подключение и инициализация](push/quick-start.md).

#### Версия 0.9.2 {#v-push--0-9-2}

Релиз 12 июля 2021 г.

- Добавлена возможность загрузки прикрепленных файлов в push-уведомлениях с помощью метода `downloadAttachmentsForNotificationRequest` для iOS 10 и выше. С примером интеграции можно ознакомиться в статье [Загрузка прикрепленных файлов](push/ios-push-download-file.md).

#### Версия 0.8.0 {#v-push-0-8-0}

Релиз 26 апреля 2019 г.

- Добавлена возможность отслеживания push-уведомлений с собственной реализацией [UNUserNotificationCenterDelegate](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate?language=objc):
    - Добавлен метод `+userNotificationCenterHandler`.
    - Добавлен протокол `YMPUserNotificationCenterHandling`.

#### Версия 0.7.2 {#v-push-0-7-2}

Релиз 27 ноября 2018 г.

- Исправлена ошибка в динамическом фреймворке.

#### Версия 0.7.1 {#v-push-0-7-1}

Релиз 19 ноября 2018 г.

- Добавлено проксирование [userNotificationCenter:openSettingsForNotification:](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/2981869-usernotificationcenter?language=objc) в `YMPUserNotificationCenterDelegate`.
- Исправлена ошибка, которая возникает при передаче `nil` в метод `+setDeviceTokenFromData:`
- Добавлена поддержка [AppMetrica SDK 3.4.0](#v3-4-0).

#### Версия 0.7.0 {#v-push-0-7-0}

Релиз 31 августа 2018 г.

- Добавлена возможность отслеживать [cбор статистики показов/отклонений push-уведомлений](push/ios-settings.md) для iOS 10 и выше.

#### Версия 0.6.0 {#v-push-0-6-0}

Релиз 20 апреля 2018 г.

- Добавлена поддержка [AppMetrica SDK 3.0.0](#v-3-0-0).

#### Версия 0.5.1 {#v-push-0-5-1}

Релиз 21 марта 2018 г.

- Исправлен крэш при открытии URL из push-уведомления.
- Исправлена ошибка, которая возникает при открытии URL одного и того же push-уведомления более одного раза.

#### Версия 0.5.0 {#v-push-0-5-0}

Релиз 26 октября 2017 г.

- Добавлена поддержка отображения push-уведомлений в iOS 10 и выше. Требует [дополнительной интеграции](push/quick-start.md#opening).
- Добавлен механизм отслеживания push-уведомлений, которые отправлены в [AppMetrica Push SDK](push/quick-start.md).
- Добавлена возможность отправлять окружение APNs (Apple Push Notifications Service) вместе с [device token](push/quick-start.md#apns).

#### Версия 0.4.0 {#v-push-0-4-0}

Релиз 24 ноября 2016 г.

- Добавлено открытие ссылки из push-уведомления.
- Добавлен динамический фреймворк.
- Динамический фреймворк DynamicDependencies заменен на Dynamic.
- Статический фреймворк StaticDependencies заменен на Static.

#### Версия 0.3.0 {#v-push-0-3-0}

Релиз 10 октября 2016 г.

- Произведена интеграция с библиотекой AppMetrica Mobile SDK.

{% endcut %}

