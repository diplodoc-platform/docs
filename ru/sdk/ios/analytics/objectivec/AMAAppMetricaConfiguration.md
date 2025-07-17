# Класс AMAAppMetricaConfiguration

Класс содержит расширенную стартовую конфигурацию библиотеки.

Параметры расширенной конфигурации применяются с момента инициализации библиотеки.

## Методы экземпляра {#instance_summary}

#|
|| [-initWithAPIKey:](#method_initWithAPIKey) | Инициализирует экземпляр класса `AMAAppMetricaConfiguration` с указанным API key. ||
|#

## Свойства {#property_summary}

#|
|| [APIKey](#property_APIKey) | API key приложения. ||
|| [accurateLocationTracking](#property_accurateLocationTracking) | Включить/отключить точный поиск местоположения для внутреннего менеджера местоположений. ||
|| [allowsBackgroundLocationUpdates](#property_allowsBackgroundLocationUpdates) | Включить/отключить фоновое отслеживание обновлений местоположения. ||
|| [appBuildNumber](#property_appBuildNumber) | Установите произвольный номер сборки приложения для отчета AppMetrica. ||
|| [appEnvironment](#property_appEnvironment) | Устанавливает окружение приложения для всех событий с момента активации. ||
|| [appOpenTrackingEnabled](#property_appOpenTrackingEnabled) | Включает/выключает автоматический сбор и отправку информации о запуске приложения через deeplink. ||
|| [appVersion](#property_appVersion) | Версия приложения. ||
|| [customHosts](#property_customHosts) | Установите URL-адреса прокси-серверов для AppMetrica, которые будут использоваться для startup запросов. ||
|| [customLocation](#property_customLocation) | Устанавливает собственную информацию о местоположении устройства. ||
|| [dataSendingEnabled](#property_dataSendingEnabled) | Включает/отключает отправку статистики на сервер AppMetrica. ||
|| [dispatchPeriod](#property_dispatchPeriod) | Установите пользовательский период отправки. Интервал в секундах между отправкой событий на сервер. ||
|| [handleActivationAsSessionStart](#property_handleActivationAsSessionStart) | Определяет инициализацию AppMetrica как начало пользовательской сессии. По умолчанию опция отключена. ||
|| [handleFirstActivationAsUpdate](#property_handleFirstActivationAsUpdate) | Определяет первый запуск приложения как обновление. ||
|| [locationTracking](#property_locationTracking) | Включает/отключает отправку информации о местоположении устройства. ||
|| [logsEnabled](#property_logsEnabled) | Включает/отключает логирование работы библиотеки. ||
|| [maxReportsCount](#property_maxReportsCount) | Установите максимальное количество сохраненных событий. ||
|| [maxReportsInDatabaseCount](#property_maxReportsInDatabaseCount) | Максимальное число отчетов об ошибках, которое хранится во внутренней БД. ||
|| [preloadInfo](#property_preloadInfo) | Устанавливает объект класса [AMAAppMetricaPreloadInfo](AMAAppMetricaPreloadInfo.md) для отслеживания предустановленных приложений. ||
|| [revenueAutoTrackingEnabled](#property_revenueAutoTrackingEnabled) | Включает/выключает автоматический сбор информации об In-App покупках. ||
|| [sessionTimeout](#property_sessionTimeout) | Задает длительность таймаута сессии в секундах. ||
|| [sessionsAutoTracking](#property_sessionsAutoTracking) | Включает/отключает автоматическое отслеживание жизненного цикла приложений. ||
|| [userProfileID](#property_userProfileID) | Задает идентификатор пользовательского профиля (`ProfileID`) при активации. ||
|#

## Описание методов {#method_detail}

### -initWithAPIKey: {#method_initWithAPIKey}

```objectivec translate=no
- (instancetype)initWithAPIKey:(NSString *)APIKey
```

Инициализирует экземпляр класса `AMAAppMetricaConfiguration` с указанным API key.

**Параметры:**

#|
|| `APIKey` | API key приложения. ||
|#

**Возвращает:**

Объект класса `AMAAppMetricaConfiguration`.

## Описание свойств {#property_detail}

### APIKey {#property_APIKey}

```objectivec translate=no
@property (nonatomic, copy, readonly) NSString *APIKey;
```

API key приложения.

### accurateLocationTracking {#property_accurateLocationTracking}

```objectivec translate=no
@property (nonatomic, assign) BOOL accurateLocationTracking;
```

Включить/отключить точный поиск местоположения для внутреннего диспетчера местоположений. По умолчанию отключено.

Действует только в том случае, если включено отслеживание местоположения `YES` и местоположение не задано вручную.

### allowsBackgroundLocationUpdates {#property_allowsBackgroundLocationUpdates}

```objectivec translate=no
@property (nonatomic, assign) BOOL allowsBackgroundLocationUpdates;
```

Включить/отключить отслеживание фоновых обновлений местоположения. По умолчанию отключено.

Чтобы включить отслеживание фоновых обновлений местоположения, установите для свойства значение `YES`.

### appBuildNumber {#property_appBuildNumber}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSString *appBuildNumber;
```

Установите произвольный номер сборки приложения для отчета AppMetrica.

Если он не задан, AppMetrica будет использовать номер сборки приложения, указанный в файле конфигурации приложения `Info.plist` (`CFBundleVersion`).
Значение номера сборки должно быть числовой строкой, которая может быть преобразована в положительное целое число.

### appEnvironment {#property_appEnvironment}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSDictionary<NSString *, NSString *> *appEnvironment;
```

Устанавливает окружение приложения для всех событий с момента активации.

### appOpenTrackingEnabled {#property_appOpenTrackingEnabled}

```objectivec translate=no
@property (nonatomic, assign) BOOL appOpenTrackingEnabled;
```

Включает/выключает автоматический сбор и отправку информации о запуске приложения через deeplink.

{% note alert %}

Начиная с версии AppMetrica SDK iOS 4.0, отслеживание открытия приложения через deeplink работает автоматически. Для остальных вариантов настройте отслеживание вручную:

- Версия AppMetrica SDK iOS ниже 4.0. [Настройка](../../../../sdk/ios/analytics/ios-operations.md#ui-app-delegate) отслеживания deeplink для UIApplicationDelegate.
- [Настройка](../../../../sdk/ios/analytics/ios-operations#ui-scene-delegate) отслеживания deeplink для UISceneDelegate (AppMetrica не отслеживает такие открытия автоматически).

Автоматическое отслеживание будет фиксировать только те deeplink, которые привели к запуску приложения. Для отслеживания deeplink внутри запущенного приложения дополнительно настройте [отслеживание](../ios-operations.md).

{% endnote %}

По умолчанию опция включена.

Возможные значения:

- `YES` — режим автоматического сбора и отправки данных о запуске приложения через deeplink включен.
- `NO` — режим автоматического сбора и отправки данных о запуске приложения через deeplink выключен.

### appVersion {#property_appVersion}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSString *appVersion;
```

Версия приложения.

### customHosts {#property_customHosts}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSArray *customHosts;
```

Установите URL-адреса прокси-серверов для AppMetrica, которые будут использоваться для startup запросов.

### customLocation {#property_customLocation}

```objectivec translate=no
@property (nonatomic, strong, nullable) CLLocation *customLocation;
```

### dataSendingEnabled {#property_dataSendingEnabled}

```objectivec translate=no
@property (nonatomic, assign) BOOL dataSendingEnabled;
```

Устанавливает собственную информацию о местоположении устройства.

### dispatchPeriod {#property_dispatchPeriod}

```objectivec translate=no
@property (nonatomic, assign) NSUInteger dispatchPeriod;
```

Установите пользовательский период отправки. Интервал в секундах между отправкой событий на сервер.

По умолчанию 90 секунд. Установка значения 0 секунд предотвращает автоматическую отправку событий библиотекой с использованием таймера.

### handleActivationAsSessionStart {#property_handleActivationAsSessionStart}

```objectivec translate=no
@property (nonatomic, assign) BOOL handleActivationAsSessionStart;
```

Определяет инициализацию AppMetrica как начало пользовательской сессии.

По умолчанию опция отключена.

Возможные значения:

- `YES` — пользовательская сессия создается в момент инициализации библиотеки.
- `NO` — в момент инициализации библиотеки создается фоновая сессия, а пользовательская сессия создается после системного события [UIApplicationDidBecomeActiveNotification](https://developer.apple.com/documentation/uikit/uiapplicationdidbecomeactivenotification).

### handleFirstActivationAsUpdate {#property_handleFirstActivationAsUpdate}

```objectivec translate=no
@property (nonatomic, assign) BOOL handleFirstActivationAsUpdate;
```

Определяет первый запуск приложения как обновление.

{% note info %}

Если первый запуск приложения определяется как обновление, то установка не будет отображаться в отчетах как новая установка и не будет атрибутироваться партнерам.

{% endnote %}

Возможные значения:

- `YES` — первый запуск определяется как обновление.
- `NO` — первый запуск определяется как новая установка.

### locationTracking {#property_locationTracking}

```objectivec translate=no
@property (nonatomic, assign) BOOL locationTracking;
```

Включает/отключает отправку информации о местоположении устройства.

По умолчанию отправка включена.

### logsEnabled {#property_logsEnabled}

```objectivec translate=no
@property (nonatomic, assign, getter=areLogsEnabled) BOOL logsEnabled;
```

Включает/отключает логирование работы библиотеки.

По умолчанию логирование выключено.

### maxReportsCount {#property_maxReportsCount}

```objectivec translate=no
@property (nonatomic, assign) NSUInteger maxReportsCount;
```

Установите максимальное количество сохраненных событий. Минимальное количество кэшированных событий, которое приводит к автоматической отправке отчетов.

По умолчанию события отправляются автоматически, когда в хранилище имеется не менее 7 элементов.

Установка значения 0 предотвращает автоматическую отправку событий библиотекой при достижении заданного количества событий в хранилище.

### maxReportsInDatabaseCount {#property_maxReportsInDatabaseCount}

```objectivec translate=no
@property (nonatomic, assign) NSUInteger maxReportsInDatabaseCount;
```

Максимальное число отчетов об ошибках, которое хранится во внутренней БД.

Допускаются значения в интервале [100; 10000]. Значения, не попадающие в данный интервал, будут автоматически заменены на значение ближайшей границы интервала.

Значение по умолчанию — 1000.

{% note info %}

Для различных `apiKey` используются отдельные БД и для них могут быть установлены независимые ограничения числа событий. Данный параметр влияет на ограничение только для соответствующего `apiKey`. Чтобы изменить максимально допустимое число событий для других `apiKey`, используйте [AMAReporterConfiguration.maxReportsInDatabaseCount](AMAReporterConfiguration.md#property_maxReportsInDatabaseCount).

{% endnote %}

### preloadInfo {#property_preloadInfo}

```objectivec translate=no
@property (nonatomic, copy, nullable) AMAAppMetricaPreloadInfo *preloadInfo;
```

Устанавливает объект класса [AMAAppMetricaPreloadInfo](AMAAppMetricaPreloadInfo.md) для отслеживания предустановленных приложений.

Подробнее в разделе [Трекинг предустановленных приложений](../../../../mobile-tracking/preinstalled-app-attr.md).

### revenueAutoTrackingEnabled {#property_revenueAutoTrackingEnabled}

```objectivec translate=no
@property (nonatomic, assign) BOOL revenueAutoTrackingEnabled;
```

Включает/выключает автоматический сбор информации об In-App покупках.

По умолчанию опция включена.

Возможные значения:

- `YES` — режим автоматического сбора и отправки информации об In-App покупках включен.
- `NO` — режим автоматического сбора и отправки информации об In-App покупках выключен.

### sessionTimeout {#property_sessionTimeout}

```objectivec translate=no
@property (nonatomic, assign) NSUInteger sessionTimeout;
```

Задает длительность таймаута сессии в секундах.
Значение по умолчанию — `10` (минимально допустимое значение).

Подробнее о сессиях в разделе [Отслеживание активности пользователей](../ios-listen.md).

### sessionsAutoTracking {#property_sessionsAutoTracking}

```objectivec translate=no
@property (nonatomic, assign) BOOL sessionsAutoTracking;
```

Включает/отключает автоматическое отслеживание жизненного цикла приложений.

По умолчанию опция включена.

Если опция выключена, необходимо вручную настроить контроль продолжительности сессии с использованием методов [+pauseSession:](AMAAppMetrica.md#method_pauseSession) и [+resumeSession:](AMAAppMetrica.md#method_resumeSession). Подробнее в разделе [Отслеживание сессий вручную](../ios-listen.md).

Для отслеживания сессий AppMetrica использует [UIApplicationDidBecomeActiveNotification](https://developer.apple.com/documentation/uikit/uiapplicationdidbecomeactivenotification) и [UIApplicationWillResignActiveNotification](https://developer.apple.com/documentation/uikit/uiapplicationwillresignactivenotification). Максимальная длительность сессии — 24 часа. Чтобы продлить сессию после 24 часов, необходимо вызвать метод [+resumeSession:](AMAAppMetrica.md#method_resumeSession) вручную.

### userProfileID {#property_userProfileID}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSString *userProfileID;
```

Задает идентификатор пользовательского профиля (`ProfileID`) при активации.

{% note alert %}

Максимальная длина строки `ProfileID` — 200 символов.

{% endnote %}
