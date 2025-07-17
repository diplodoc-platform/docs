# Класс AMAAppMetrica

Методы класса используются для настройки работы библиотеки.

## Методы экземпляра {#instance_summary}

#|
|| +[activateReporterWithConfiguration:](#method_activateReporterWithConfiguration) | Инициализирует репортер с расширенной конфигурацией. ||
|| +[activateWithConfiguration:](#method_activateWithConfiguration) | Инициализирует библиотеку в приложении с [расширенной стартовой конфигурацией](../ios-operations.md). ||
|| +[clearAppEnvironment](#method_clearAppEnvironment) | Удаление всех данных ключ-значение, связанных со всеми будущими событиями. ||
|| +[pauseSession](#method_pauseSession) | Приостанавливает сессию. ||
|| +[reportAdRevenue:onFailure:](#method_reportAdRevenue__onFailure) | Отправляет информацию о рекламной выручке на сервер AppMetrica. ||
|| +[reportECommerce:onFailure:](#method_reportECommerce__onFailure) | Отправляет сообщение о ecommerce-событии. ||
|| +[reportEvent:onFailure:](#method_reportEvent__onFailure) | Отправляет [сообщение о событии](../ios-operations.md#report-event). ||
|| +[reportEvent:parameters:onFailure:](#method_reportEvent__parameters__onFailure) | Отправляет [сообщение о событии с дополнительными параметрами](../ios-operations.md#report-event-params). ||
|| [+reportExternalAttribution:source:onFailure:](#method_reportExternalAttribution__source__onFailure) | Отправляет данные о [внешней атрибуции](../../../../data-collection/attribution-integration.yaml) в AppMetrica. ||
|| +[reportRevenue:onFailure:](#method_reportRevenue__onFailure) | Отправляет информацию о покупке на сервер AppMetrica. ||
|| +[reportUserProfile:onFailure:](#method_reportUserProfile__onFailure) | Отправляет информацию об обновлении пользовательского профиля. ||
|| +[reporterForAPIKey:](#method_reporterForAPIKey) | Создает репортер для [отправки событий на дополнительный API key](../ios-operations.md#reporter-different-apikey-send). ||
|| +[requestStartupIdentifiersWithCompletionQueue:completionBlock:](#method_requestStartupIdentifiersWithCompletionQueue__completionBlock) | Запрашивает все предопределенные идентификаторы. ||
|| +[requestStartupIdentifiersWithKeys:completionQueue:completionBlock:](#method_requestStartupIdentifiersWithKeys__completionQueue__completionBlock) | Запрашивает идентификаторы для определенных ключей. ||
|| +[resumeSession](#method_resumeSession) | Возобновляет сессию или создает новую, если тайм-аут сессии истек. ||
|| +[sendEventsBuffer](#method_sendEventsBuffer) | Отправляет сохраненные события из буфера. ||
|| +[setAppEnvironmentValue:forKey:](#method_setAppEnvironmentValue__forKey) | Устанавливает пару ключ-значение, которая ассоциирована со всеми будущими событиями. ||
|| +[setDataSendingEnabled:](#method_setDataSendingEnabled) | Включает/отключает отправку статистики на сервер AppMetrica. ||
|| +[setupWebViewReporting:onFailure:](#method_setupWebViewReporting__onFailure) | Добавляет для указанной вебвью JavaScript-интерфейс с названием AppMetrica в window. Это позволяет отправлять клиентские события из JavaScript-кода. ||
|| +[trackOpeningURL:](#method_trackOpeningURL) | Обрабатывает URL, который открыл приложение. ||
|#

## Свойства {#property_summary}

#|
|| [UUID](#property_UUID) | Текущий UUID. ||
|| [accurateLocationTrackingEnabled](#property_accurateLocationTrackingEnabled) | Контролирует точность отслеживания местоположения, используемого внутренним менеджером местоположения. ||
|| [activated](#property_activated) | Указывает, была ли активирована AppMetrica. ||
|| [allowsBackgroundLocationUpdates](#property_allowsBackgroundLocationUpdates) | Включить/отключить фоновое отслеживание обновлений местоположения. ||
|| [customLocation](#property_customLocation) | Устанавливает [собственную информацию о местоположении устройства](../ios-operations.md#location-manual). ||
|| [deviceIDHash](#property_deviceIDHash) | Текущий appmetrica_device_id_hash. ||
|| [deviceID](#property_deviceID) | Текущий appmetrica_device_id. ||
|| [libraryVersion](#property_libraryVersion) | Текущая версию библиотеки AppMetrica. ||
|| [locationTrackingEnabled](#property_locationTrackingEnabled) | Включает/отключает [отправку информации о местоположении устройства](../ios-operations.md#track-location). ||
|| [userProfileID](#property_userProfileID) | Устанавливает ID для [пользовательского профиля](../../../../data-collection/about-profiles.md). ||
|#

## Описание методов {#method_detail}

### +activateReporterWithConfiguration: {#method_activateReporterWithConfiguration}

```objectivec translate=no
+ (void)activateReporterWithConfiguration:(AMAReporterConfiguration *)configuration;
```

Инициализирует репортер с расширенной конфигурацией.

Конфигурация репортера должна быть инициализирована до первого обращения к репортеру. Иначе конфигурация репортера игнорируется.

Репортер должен быть инициализирован с конфигурацией, которая содержит API key, отличный от API key приложения.

**Параметры:**

#|
|| `configuration` | Объект класса [AMAReporterConfiguration](AMAReporterConfiguration.md), который содержит расширенную конфигурацию репортера. ||
|#

### +activateWithConfiguration: {#method_activateWithConfiguration}

```objectivec translate=no
+ (void)activateWithConfiguration:(AMAAppMetricaConfiguration *)configuration;
```

Инициализирует библиотеку в приложении с [расширенной стартовой конфигурацией](../ios-operations.md#initialize).

**Параметры:**

#|
|| `configuration` | Объект класса [AMAAppMetricaConfiguration](AMAAppMetricaConfiguration.md), который содержит расширенную стартовую конфигурацию библиотеки. ||
|#

### +clearAppEnvironment {#method_clearAppEnvironment}

```objectivec translate=no
+ (void)clearAppEnvironment;
```

Очистка среды приложения, например, удаление всех данных ключ - значение, связанных со всеми будущими событиями.

### +pauseSession {#method_pauseSession}

```objectivec translate=no
+ (void)pauseSession;
```

Приостанавливает сессию.

{% note info %}

Длительность сессии зависит от [заданного таймаута](AMAAppMetricaConfiguration.md#property_sessionTimeout). Если интервал между приостановкой и возобновлением сессии меньше заданного времени тайм-аута, то текущая сессия будет возобновлена, если больше — будет создана новая.

Подробнее о сессиях в разделе [Отслеживание активности пользователей](../ios-listen.md).

{% endnote %}

### +reportAdRevenue:onFailure: {#method_reportAdRevenue__onFailure}

```objectivec translate=no
+ (void)reportAdRevenue:(AMAAdRevenueInfo *)adRevenue
              onFailure:(nullable void (^)(NSError *error))onFailure;
```

Отправляет информацию о рекламной выручке на сервер AppMetrica.

**Параметры:**

#|
|| `adRevenue` | Объект класса [AMAAdRevenueInfo](AMAAdRevenueInfo.md), который содержит информацию о рекламной выручке. ||
|| `onFailure` | Callback-метод, который будет вызван в случае ошибки. ||
|#

### +reportECommerce:onFailure: {#method_reportECommerce__onFailure}

```objectivec translate=no
+ (void)reportECommerce:(AMAECommerce *)eCommerce
              onFailure:(nullable void (^)(NSError *error))onFailure;
```

Отправляет сообщение о ecommerce-событии.

**Параметры:**

#|
|| `eCommerce` | Объект класса [AMAECommerce](AMAECommerce.md). ||
|| `onFailure` | Callback-метод, который будет вызван в случае ошибки. ||
|#

### +reportEvent:onFailure: {#method_reportEvent__onFailure}

```objectivec translate=no
+ (void)reportEvent:(NSString *)name
          onFailure:(nullable void (^)(NSError *error))onFailure;
```

Отправляет [сообщение о событии](../ios-operations.md#report-event).

**Параметры:**

#|
|| `name` | Короткое название или описание события. ||
|| `onFailure` | Блок, который выполняется при возникновении ошибки. Ошибка передается как блок-аргумент. ||
|#

### +reportEvent:parameters:onFailure: {#method_reportEvent__parameters__onFailure}

```objectivec translate=no
+ (void)reportEvent:(NSString *)name
         parameters:(nullable NSDictionary *)params
          onFailure:(nullable void (^)(NSError *error))onFailure;
```

Отправляет [сообщение о событии с дополнительными параметрами](../ios-operations.md#report-event-params).

**Параметры:**

#|
|| `name` | Короткое название или описание события. ||
|| `params` | Параметры в виде пар <q>ключ-значение</q>. ||
|| `onFailure` | Callback-метод, который будет вызван в случае ошибки. ||
|#

### +reportExternalAttribution:source:onFailure: {#method_reportExternalAttribution__source__onFailure}

```objectivec translate=no
+ (void)reportExternalAttribution:(NSDictionary *)attribution
                           source:(AMAAttributionSource)source
                        onFailure:(nullable void (^)(NSError *error))onFailure;
```

Отправляет данные о [внешней атрибуции](../../../../data-collection/attribution-integration.yaml) в AppMetrica.

**Параметры:**

#|
|| `attribution` | Словарь содержит данные об атрибуции. Должен быть конвертируемым в JSON, иначе метод завершится запуском блока с ошибкой — `onFailure`. ||
|| `source` | Источник с данными об атрибуции. [Список источников](AMAAttributionSource.md). ||
|| `onFailure` | Callback-метод, который будет вызван в случае ошибки. Ошибка передается в качестве аргумента. ||
|#

### +reportRevenue:onFailure: {#method_reportRevenue__onFailure}

```objectivec translate=no
+ (void)reportRevenue:(AMARevenueInfo *)revenueInfo
            onFailure:(nullable void (^)(NSError *error))onFailure;
```

Отправляет информацию о покупке на сервер AppMetrica.

**Параметры:**

#|
|| `revenueInfo` | Объект класса [AMARevenueInfo](AMARevenueInfo.md), который содержит информацию о покупке. ||
|| `onFailure` | Callback-метод, который будет вызван в случае ошибки. ||
|#

### +reportUserProfile:onFailure: {#method_reportUserProfile__onFailure}

```objectivec translate=no
+ (void)reportUserProfile:(AMAUserProfile *)userProfile
                onFailure:(nullable void (^)(NSError *error))onFailure;
```

Отправляет информацию об обновлении пользовательского профиля.

**Параметры:**

#|
|| `userProfile` | Объект класса [AMAUserProfile](AMAUserProfile.md), который содержит информацию о пользовательском профиле. ||
|| `onFailure` | Callback-метод, который будет вызван в случае ошибки. ||
|#

### +reporterForAPIKey: {#method_reporterForAPIKey}

```objectivec translate=no
+ (nullable id<AMAAppMetricaReporting>)reporterForAPIKey:(NSString *)APIKey;
```

Создает репортер для [отправки событий на дополнительный API key](../ios-operations.md#reporter-different-apikey-send).

Чтобы инициализировать репортер с расширенной конфигурацией, используйте метод [activateReporterWithConfiguration:](#method_activateReporterWithConfiguration). Конфигурация репортера должна быть инициализирована до первого обращения к репортеру. Иначе, конфигурация репортера игнорируется.

**Параметры:**

#|
|| `APIKey` | API key, отличный от API key приложения. ||
|#

**Возвращает:**

Объект, реализующий протокол [AMAAppMetricaReporting](AMAAppMetricaReporting.md) для заданного API key приложения.

### +requestStartupIdentifiersWithCompletionQueue:completionBlock: {#method_requestStartupIdentifiersWithCompletionQueue__completionBlock}

```objectivec translate=no
+ (void)requestStartupIdentifiersWithCompletionQueue:(nullable dispatch_queue_t)queue
                                     completionBlock:(AMAIdentifiersCompletionBlock)block;
```

Получение всех предопределенных идентификаторов

**Параметры:**

#|
|| `queue` | Очередь для отправки блока. Если значение равно нулю, используется основная очередь. ||
|| `block` | Блок будет отправлен при появлении доступных идентификаторов или в случае ошибки.

Предопределенными идентификаторами являются:
  - `kAMAUUIDKey`
  - `kAMADeviceIDKey`
  - `kAMADeviceIDHashKey`

Если они доступны на момент вызова - блок отправляется немедленно. Смотрите определение `AMAIdentifiersCompletionBlock` для получения более подробной информации о возвращаемых типах.

||
|#

### +requestStartupIdentifiersWithKeys:completionQueue:completionBlock: {#requestStartupIdentifiersWithKeys__completionQueue__completionBlock}

```objectivec translate=no
+ (void)requestStartupIdentifiersWithKeys:(NSArray<AMAStartupKey> *)keys
                          completionQueue:(nullable dispatch_queue_t)queue
                          completionBlock:(AMAIdentifiersCompletionBlock)block;
```

Получение идентификаторов для определенных ключей

**Параметры:**

#|
|| `keys` | Массив идентификационных ключей для запроса. Смотрите `AMAStartupKey`. ||
|| `queue` | Очередь для отправки блока. Если значение равно нулю, используется основная очередь. ||
|| `block` | Блок будет отправлен при появлении доступных идентификаторов или в случае ошибки. 

Если они доступны на момент вызова - блок отправляется немедленно. Смотрите определение `AMAIdentifiersCompletionBlock` для получения более подробной информации о возвращаемых типах.

||
|#

### +resumeSession {#method_resumeSession}

```objectivec translate=no
+ (void)resumeSession;
```

Возобновляет сессию или создает новую, если таймаут сессии истек.

{% note info %}

Длительность сессии зависит от [заданного таймаута](AMAAppMetricaConfiguration.md#property_sessionTimeout). Если интервал между приостановкой и возобновлением сессии меньше заданного времени тайм-аута, то текущая сессия будет возобновлена, если больше — будет создана новая.

Подробнее о сессиях в разделе [Отслеживание активности пользователей](../ios-listen.md).

{% endnote %}

### +sendEventsBuffer {#method_sendEventsBuffer}

```objectivec translate=no
+ (void)sendEventsBuffer;
```

Отправляет сохраненные события из буфера.

AppMetrica SDK не отправляет события сразу после того, как оно произошло. Библиотека хранит данные о событиях в буфере. Метод `+sendEventsBuffer` отправляет данные из буфера и очищает его. Используйте этот метод для принудительной отправки сохраненных событий после прохождения важных сценариев пользователя.

{% note alert %}

Частое использование метода может привести к повышению энергопотребления и расходу исходящего интернет-трафика.

{% endnote %}

### +setAppEnvironmentValue:forKey: {#method_setAppEnvironmentValue__forKey}

```objectivec translate=no
+ (void)setAppEnvironmentValue:(nullable NSString *)value
                        forKey:(NSString *)key;
```

Установка данных ключ - значение, которые будут использоваться в качестве дополнительной информации, связанной со всеми будущими событиями.

Если значение равно нулю, ранее установленное значение ключа удаляется. Ничего не делает, если ключ не был добавлен.

**Параметры:**

#|
|| `value` | Значение. ||
|| `key` | Ключ. ||
|#

### +setDataSendingEnabled: {#method_setDataSendingEnabled}

```objectivec translate=no
+ (void)setDataSendingEnabled:(BOOL)enabled;
```

Включает/отключает отправку статистики на сервер AppMetrica.

Подробнее об использовании метода в разделе [Отключение и включение отправки статистики](../ios-operations.md#stat).

{% note info %}

Отключение отправки для главного API key также отключает отправку данных со всех репортеров, которые были инициализированы с другим API key.

{% endnote %}

**Параметры:**

#|
|| `enabled` | Признак отправки статистики. Значение по умолчанию — `YES`.

Возможные значения:

- `YES` — отправка статистики включена.
- `NO` — отправка статистики выключена. ||
  |#

### +setupWebViewReporting:onFailure: {#method_setupWebViewReporting__onFailure}

```objectivec translate=no
+ (void)setupWebViewReporting:(id<AMAJSControlling>)controller
                    onFailure:(nullable void (^)(NSError *error))onFailure;
```

Добавляет для указанной вебвью JavaScript-интерфейс с названием AppMetrica в window. Это позволяет отправлять клиентские события из JavaScript-кода.

Замечания:

- Метод должен вызываться из главной очереди.
- Метод недоступен на tvOS.
- Метод необходимо вызывать до загрузки любого контента. Рекомендуется вызывать метод до создания вебвью и до добавления своих скриптов в WKUserContentController.
  Подробнее см. в разделе [Примеры использования методов](../ios-operations.md#js-event).

**Параметры:**

#|
|| `controller` | Объект `AMAJSControlling`. ||
|| `onFailure` | Callback-метод, который будет вызван в случае ошибки. ||
|#

### +trackOpeningURL: {#method_trackOpeningURL}

```objectivec translate=no
+ (void)trackOpeningURL:(NSURL *)URL;
```

Обрабатывает URL, который открыл приложение.

Используется для [регистрации открытия приложения с помощью deeplink](../ios-operations.md#deeplink).

**Параметры:**

#|
|| `URL` | URL, который открыл приложение. ||
|#

## Описание свойств {#property_detail}

### UUID {#property_UUID}

```objectivec translate=no
@property (class, nonatomic, readonly) NSString *UUID;
```

Извлекает текущий UUID.

### accurateLocationTrackingEnabled {#property_accurateLocationTrackingEnabled}

```objectivec translate=no
@property (class, nonatomic, getter=isAccurateLocationTrackingEnabled) BOOL accurateLocationTrackingEnabled;
```

Контролирует точность отслеживания местоположения, используемого внутренним менеджером местоположения.

Если установлено значение `YES`, диспетчер местоположений пытается использовать наиболее точные доступные данные о местоположении.
Это свойство вступает в силу только в том случае, если для параметра `isLocationTrackingEnabled` установлено значение `YES` и местоположение
не было задано вручную с помощью свойства `customLocation`.

### activated {#property_activated}

```objectivec translate=no
@property (class, assign, readonly, getter=isActivated) BOOL activated;
```

Указывает, была ли активирована AppMetrica.

{% note info %}

Используйте это свойство, чтобы проверить, была ли AppMetrica уже активирована, как правило, чтобы избежать избыточных вызовов активации или убедиться, что сбор статистики запущен.

{% endnote %}

### allowsBackgroundLocationUpdates {#property_allowsBackgroundLocationUpdates}

```objectivec translate=no
@property (class, nonatomic) BOOL allowsBackgroundLocationUpdates;
```

Включить/отключить фоновое отслеживание обновлений местоположения. По умолчанию отключен.

### customLocation {#property_customLocation}

```objectivec translate=no
@property (class, nonatomic, nullable) CLLocation *customLocation;
```

Устанавливает [собственную информацию о местоположении устройства](../ios-operations.md#location-manual).

### deviceIDHash {#property_deviceIDHash}

```objectivec translate=no
@property (class, nonatomic, nullable, readonly) NSString *deviceIDHash;
```

Извлекает appmetrica_device_id_hash.

### deviceID {#property_deviceID}

```objectivec translate=no
@property (class, nonatomic, nullable, readonly) NSString *deviceID;
```

Извлекает appmetrica_device_id.

### libraryVersion {#property_libraryVersion}

```objectivec translate=no
@property (class, nonatomic, readonly) NSString *libraryVersion;
```

Возвращает текущую версию библиотеки AppMetrica.

### locationTrackingEnabled {#property_locationTrackingEnabled}

```objectivec translate=no
@property (class, nonatomic, getter=isLocationTrackingEnabled) BOOL locationTrackingEnabled;
```

Включает/отключает [отправку информации о местоположении устройства](../ios-operations.md#track-location).

### userProfileID {#property_userProfileID}

```objectivec translate=no
@property (class, nonatomic, nullable) NSString *userProfileID;
```

Устанавливает ID для [пользовательского профиля](../../../../data-collection/about-profiles.md). Если отправка `ProfileId` не настроена, [предопределенные атрибуты](../../../../data-collection/profile-attributes.md#pre-defined) не отображаются в веб-интерфейсе.
