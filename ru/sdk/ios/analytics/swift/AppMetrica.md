# Класс AppMetrica

Методы класса используются для настройки работы библиотеки.

## Методы экземпляра {#instance_summary}

#|
|| [activate(with:)](#method_activateWithConfiguration) | Инициализирует библиотеку в приложении с [расширенной стартовой конфигурацией](../ios-operations.md). ||
|| [activateReporter(with:)](#method_activateReporterWithConfiguration) | Инициализирует репортер с расширенной конфигурацией. ||
|| [clearAppEnvironment()](#method_clearAppEnvironment) | Удаление всех данных ключ-значение, связанных со всеми будущими событиями. ||
|| [pauseSession()](#method_pauseSession) | Приостанавливает сессию. ||
|| [reportAdRevenue(_:onFailure:)](#method_reportAdRevenue__onFailure) | Отправляет информацию о рекламной выручке на сервер AppMetrica. ||
|| [reportECommerce(_:onFailure:)](#method_reportECommerce__onFailure) | Отправляет сообщение о ecommerce-событии. ||
|| [reportEvent(name:onFailure:)](#method_reportEvent__onFailure) | Отправляет [сообщение о событии](../ios-operations.md#report-event). ||
|| [reportEvent(name:parameters:onFailure:)](#method_reportEvent__parameters__onFailure) | Отправляет [сообщение о событии с дополнительными параметрами](../ios-operations.md#report-event-params). ||
|| [reportExternalAttribution(_:from:onFailure:)](#method_reportExternalAttribution__from__onFailure) | Отправляет данные о [внешней атрибуции](../../../../data-collection/attribution-integration.yaml) в AppMetrica. ||
|| [reportRevenue(_:onFailure:)](#method_reportRevenue__onFailure) | Отправляет информацию о покупке на сервер AppMetrica. ||
|| [reportUserProfile(_:onFailure:)](#method_reportUserProfile__onFailure) | Отправляет информацию об обновлении пользовательского профиля. ||
|| [reporter(for:)](#method_reporterForAPIKey) | Создает репортер для [отправки событий на дополнительный API key](../ios-operations.md#reporter-different-apikey-send). ||
|| [requestStartupIdentifiers(for:on:completion:)](#method_requestStartupIdentifiersWithKeys__completionQueue__completionBlock) | Запрашивает идентификаторы для определенных ключей. ||
|| [requestStartupIdentifiers(on:completion:)](#method_requestStartupIdentifiersWithCompletionQueue__completionBlock) | Запрашивает все предопределенные идентификаторы. ||
|| [resumeSession()](#method_resumeSession) | Возобновляет сессию или создает новую, если тайм-аут сессии истек. ||
|| [sendEventsBuffer()](#method_sendEventsBuffer) | Отправляет сохраненные события из буфера. ||
|| [setAppEnvironment(:forKey:)](#method_setAppEnvironmentValue__forKey) | Устанавливает пару ключ-значение, которая ассоциирована со всеми будущими событиями. ||
|| [setDataSendingEnabled(_:)](#method_setDataSendingEnabled) | Включает/отключает отправку статистики на сервер AppMetrica. ||
|| [setupWebViewReporting(with:onFailure:)](#method_setupWebViewReporting__onFailure) | Добавляет для указанной вебвью JavaScript-интерфейс с названием AppMetrica в window. Это позволяет отправлять клиентские события из JavaScript-кода. ||
|| [trackOpeningURL(_:)](#method_trackOpeningURL) | Обрабатывает URL, который открыл приложение. ||
|#

## Свойства {#property_summary}

#|
|| [allowsBackgroundLocationUpdates](#property_allowsBackgroundLocationUpdates) | Включить/отключить фоновое отслеживание обновлений местоположения. ||
|| [customLocation](#property_customLocation) | Устанавливает [собственную информацию о местоположении устройства](../ios-operations.md#location-manual). ||
|| [deviceIDHash](#property_deviceIDHash) | Текущий appmetrica_device_id_hash. ||
|| [deviceID](#property_deviceID) | Текущий appmetrica_device_id. ||
|| [isAccurateLocationTrackingEnabled](#property_accurateLocationTrackingEnabled) | Контролирует точность отслеживания местоположения, используемого внутренним менеджером местоположения. ||
|| [isActivated](#property_activated) | Указывает, была ли активирована AppMetrica. ||
|| [isLocationTrackingEnabled](#property_locationTrackingEnabled) | Включает/отключает [отправку информации о местоположении устройства](../ios-operations.md#track-location). ||
|| [libraryVersion](#property_libraryVersion) | Текущая версию библиотеки AppMetrica. ||
|| [userProfileID](#property_userProfileID) | Устанавливает ID для [пользовательского профиля](../../../../data-collection/about-profiles.md). ||
|| [uuid](#property_UUID) | Текущий UUID. ||
|#

## Описание методов {#method_detail}

### activate(with:) {#method_activateWithConfiguration}

```swift translate=no
class func activate(with: AppMetricaConfiguration)
```

Инициализирует библиотеку в приложении с [расширенной стартовой конфигурацией](../ios-operations.md#initialize).

**Параметры:**

#|
|| `with` | Объект класса [AppMetricaConfiguration](AppMetricaConfiguration.md), который содержит расширенную стартовую конфигурацию библиотеки. ||
|#

### activateReporter(with:) {#method_activateReporterWithConfiguration}

```swift translate=no
class func activateReporter(with: ReporterConfiguration)
```

Инициализирует репортер с расширенной конфигурацией.

Конфигурация репортера должна быть инициализирована до первого обращения к репортеру. Иначе конфигурация репортера игнорируется.

Репортер должен быть инициализирован с конфигурацией, которая содержит API key, отличный от API key приложения.

**Параметры:**

#|
|| `with` | Объект класса [ReporterConfiguration](ReporterConfiguration.md), который содержит расширенную конфигурацию репортера. ||
|#

### clearAppEnvironment() {#method_clearAppEnvironment}

```swift translate=no
class func clearAppEnvironment()
```

Очистка среды приложения, например, удаление всех данных ключ - значение, связанных со всеми будущими событиями.

### pauseSession() {#method_pauseSession}

```swift translate=no
class func pauseSession()
```

Приостанавливает сессию.

{% note info %}

Длительность сессии зависит от [заданного таймаута](AppMetricaConfiguration.md#property_sessionTimeout). Если интервал между приостановкой и возобновлением сессии меньше заданного времени тайм-аута, то текущая сессия будет возобновлена, если больше — будет создана новая.

Подробнее о сессиях в разделе [Отслеживание активности пользователей](../ios-listen.md).

{% endnote %}

### reportAdRevenue(_:onFailure:) {#method_reportAdRevenue__onFailure}

```swift translate=no
class func reportAdRevenue(_ adRevenue: AdRevenueInfo, onFailure: ((Error) -> Void)?)
```

Отправляет информацию о рекламной выручке на сервер AppMetrica.

**Параметры:**

#|
|| `adRevenue` | Объект класса [AdRevenueInfo](AdRevenueInfo.md), который содержит информацию о рекламной выручке. ||
|| `onFailure` | Callback-метод, который будет вызван в случае ошибки. ||
|#

### reportECommerce(_:onFailure:) {#method_reportECommerce__onFailure}

```swift translate=no
class func reportECommerce(_ eCommerce: ECommerce, onFailure: ((Error) -> Void)?)
```

Отправляет сообщение о ecommerce-событии.

**Параметры:**

#|
|| `eCommerce` | Объект класса [ECommerce](ECommerce.md). ||
|| `onFailure` | Callback-метод, который будет вызван в случае ошибки. ||
|#

### reportEvent(name:onFailure) {#method_reportEvent__onFailure}

```swift translate=no
class func reportEvent(name: String, onFailure: ((Error) -> Void)?)
```

Отправляет [сообщение о событии](../ios-operations.md#report-event).

**Параметры:**

#|
|| `name` | Короткое название или описание события. ||
|| `onFailure` | Блок, который выполняется при возникновении ошибки. Ошибка передается как блок-аргумент. ||
|#

### reportEvent(name:parameters:onFailure) {#method_reportEvent__parameters__onFailure}

```swift translate=no
class func reportEvent(name: String, parameters: [AnyHashable : Any]?, onFailure: ((Error) -> Void)?)
```

Отправляет [сообщение о событии с дополнительными параметрами](../ios-operations.md#report-event-params).

**Параметры:**

#|
|| `name` | Короткое название или описание события. ||
|| `parameters` | Параметры в виде пар <q>ключ-значение</q>. ||
|| `onFailure` | Callback-метод, который будет вызван в случае ошибки. ||
|#

### reportExternalAttribution(_:from:onFailure:) {#method_reportExternalAttribution__from__onFailure}

```swift translate=no
class func reportExternalAttribution(_ attribution: [AnyHashable : Any], from source: AttributionSource, onFailure: ((any Error) -> Void)? = nil)
```

Отправляет данные о [внешней атрибуции](../../../../data-collection/attribution-integration.yaml) в AppMetrica.

#|
|| `attribution` | Словарь содержит данные об атрибуции. Должен быть конвертируемым в JSON, иначе метод завершится запуском блока с ошибкой — `onFailure`. ||
|| `source` | Источник с данными об атрибуции. [Список источников](AttributionSource.md). ||
|| `onFailure` | Callback-метод, который будет вызван в случае ошибки. Ошибка передается в качестве аргумента. ||
|#

### reportRevenue(_:onFailure:) {#method_reportRevenue__onFailure}

```swift translate=no
class func reportRevenue(_ revenueInfo: RevenueInfo, onFailure: ((Error) -> Void)?)
```

Отправляет информацию о покупке на сервер AppMetrica.

**Параметры:**

#|
|| `revenueInfo` | Объект класса [RevenueInfo](RevenueInfo.md), который содержит информацию о покупке. ||
|| `onFailure` | Callback-метод, который будет вызван в случае ошибки. ||
|#

### reportUserProfile(_:onFailure:) {#method_reportUserProfile__onFailure}

```swift translate=no
class func reportUserProfile(_ userProfile: UserProfile, onFailure: ((Error) -> Void)?)
```

Отправляет информацию об обновлении пользовательского профиля.

**Параметры:**

#|
|| `userProfile` | Объект класса [UserProfile](UserProfile.md), который содержит информацию о пользовательском профиле. ||
|| `onFailure` | Callback-метод, который будет вызван в случае ошибки. ||
|#

### reporter(for:) {#method_reporterForAPIKey}

```swift translate=no
class func reporter(for: String) -> AppMetricaReporting
```

Создает репортер для [отправки событий на дополнительный API key](../ios-operations.md#reporter-different-apikey-send).

Чтобы инициализировать репортер с расширенной конфигурацией, используйте метод [activateReporter(with:)](#method_activateReporterWithConfiguration). Конфигурация репортера должна быть инициализирована до первого обращения к репортеру. Иначе, конфигурация репортера игнорируется.

**Параметры:**

#|
|| `for` | API key, отличный от API key приложения. ||
|#

**Возвращает:**

Объект, реализующий протокол [AppMetricaReporting](AppMetricaReporting.md) для заданного API key приложения.

### requestStartupIdentifiers(for:on:completion:) {#requestStartupIdentifiersWithKeys__completionQueue__completionBlock}

```swift translate=no
class func requestStartupIdentifiers(for: [StartupKey], on: dispatch_queue_t?, completion: ([StartupKey : Any]?, Error?) -> Void)
```

Получение идентификаторов для определенных ключей

**Параметры:**

#|
|| `for` | Массив идентификационных ключей для запроса. Смотрите `StartupKey`. ||
|| `on` | Очередь для отправки блока. Если значение равно нулю, используется основная очередь. ||
|| `completion` | Блок будет отправлен при появлении доступных идентификаторов или в случае ошибки.

Если они доступны на момент вызова - блок отправляется немедленно. Смотрите определение `AMAIdentifiersCompletionBlock` для получения более подробной информации о возвращаемых типах.

||
|#

### requestStartupIdentifiers(on:completion:) {#method_requestStartupIdentifiersWithCompletionQueue__completionBlock}

```swift translate=no
class func requestStartupIdentifiers(on: dispatch_queue_t?, completion: ([StartupKey : Any]?, Error?) -> Void)
```

Получение всех предопределенных идентификаторов

**Параметры:**

#|
|| `on` | Очередь для отправки блока. Если значение равно нулю, используется основная очередь. ||
|| `completion` | Блок будет отправлен при появлении доступных идентификаторов или в случае ошибки.

Предопределенными идентификаторами являются:
- `StartupKey.uuidKey`
- `StartupKey.deviceIDHashKey`
- `StartupKey.deviceIDKey`

Если они доступны на момент вызова - блок отправляется немедленно. Смотрите определение `AMAIdentifiersCompletionBlock` для получения более подробной информации о возвращаемых типах.

||
|#

### resumeSession() {#method_resumeSession}

```swift translate=no
class func resumeSession()
```

Возобновляет сессию или создает новую, если таймаут сессии истек.

{% note info %}

Длительность сессии зависит от [заданного таймаута](AppMetricaConfiguration.md#property_sessionTimeout). Если интервал между приостановкой и возобновлением сессии меньше заданного времени тайм-аута, то текущая сессия будет возобновлена, если больше — будет создана новая.

Подробнее о сессиях в разделе [Отслеживание активности пользователей](../ios-listen.md).

{% endnote %}

### sendEventsBuffer() {#method_sendEventsBuffer}

```swift translate=no
class func sendEventsBuffer()
```

Отправляет сохраненные события из буфера.

AppMetrica SDK не отправляет события сразу после того, как оно произошло. Библиотека хранит данные о событиях в буфере. Метод `sendEventsBuffer()` отправляет данные из буфера и очищает его. Используйте этот метод для принудительной отправки сохраненных событий после прохождения важных сценариев пользователя.

{% note alert %}

Частое использование метода может привести к повышению энергопотребления и расходу исходящего интернет-трафика.

{% endnote %}

### setAppEnvironment(_:forKey:) {#method_setAppEnvironmentValue__forKey}

```swift translate=no
class func setAppEnvironment(_ value: String?, forKey: String)
```

Установка данных ключ - значение, которые будут использоваться в качестве дополнительной информации, связанной со всеми будущими событиями.

Если значение равно нулю, ранее установленное значение ключа удаляется. Ничего не делает, если ключ не был добавлен.

**Параметры:**

#|
|| `value` | Значение. ||
|| `key` | Ключ. ||
|#

### setDataSendingEnabled(_:) {#method_setDataSendingEnabled}

```swift translate=no
class func setDataSendingEnabled(_ enabled: Bool)
```

Включает/отключает отправку статистики на сервер AppMetrica.

Подробнее об использовании метода в разделе [Отключение и включение отправки статистики](../ios-operations.md#stat).

{% note info %}

Отключение отправки для главного API key также отключает отправку данных со всех репортеров, которые были инициализированы с другим API key.

{% endnote %}

**Параметры:**

#|
|| `enabled` | Признак отправки статистики. Значение по умолчанию — `true`.

Возможные значения:

- `true` — отправка статистики включена.
- `false` — отправка статистики выключена. ||
  |#

### setupWebViewReporting(with:onFailure:) {#method_setupWebViewReporting__onFailure}

```swift translate=no
class func setupWebViewReporting(with: JSControlling, onFailure: ((Error) -> Void)?)
```

Добавляет для указанной вебвью JavaScript-интерфейс с названием AppMetrica в window. Это позволяет отправлять клиентские события из JavaScript-кода.

Замечания:

- Метод должен вызываться из главной очереди.
- Метод недоступен на tvOS.
- Метод необходимо вызывать до загрузки любого контента. Рекомендуется вызывать метод до создания вебвью и до добавления своих скриптов в WKUserContentController.
  Подробнее см. в разделе [Примеры использования методов](../ios-operations.md#js-event).

**Параметры:**

#|
|| `with` | Объект `JSControlling`. ||
|| `onFailure` | Callback-метод, который будет вызван в случае ошибки. ||
|#

### trackOpeningURL(_:) {#method_trackOpeningURL}

```swift translate=no
class func trackOpeningURL(_ URL: URL)
```

Обрабатывает URL, который открыл приложение.

Используется для [регистрации открытия приложения с помощью deeplink](../ios-operations.md#deeplink).

**Параметры:**

#|
|| `URL` | URL, который открыл приложение. ||
|#

## Описание свойств {#property_detail}

### allowsBackgroundLocationUpdates {#property_allowsBackgroundLocationUpdates}

```swift translate=no
var allowsBackgroundLocationUpdates: Bool { get; set; }
```

Включить/отключить фоновое отслеживание обновлений местоположения. По умолчанию отключен.

### customLocation {#property_customLocation}

```swift translate=no
var customLocation: CLLocation? { get; set; }
```

Устанавливает [собственную информацию о местоположении устройства](../ios-operations.md#location-manual).

### deviceIDHash {#property_deviceIDHash}

```swift translate=no
var deviceIDHash: String? { get; }
```

Извлекает appmetrica_device_id_hash.

### deviceID {#property_deviceID}

```swift translate=no
var deviceID: String? { get; }
```

Извлекает appmetrica_device_id.

### isAccurateLocationTrackingEnabled {#property_accurateLocationTrackingEnabled}

```swift translate=no
var isAccurateLocationTrackingEnabled: Bool { get; set; }
```

Контролирует точность отслеживания местоположения, используемого внутренним менеджером местоположения.

Если установлено значение `true`, диспетчер местоположений пытается использовать наиболее точные доступные данные о местоположении.
Это свойство вступает в силу только в том случае, если для параметра `isLocationTrackingEnabled` установлено значение `true` и местоположение
не было задано вручную с помощью свойства `customLocation`.

### isActivated {#property_activated}

```swift translate=no
var isActivated: Bool { get; }
```

Указывает, была ли активирована AppMetrica.

{% note info %}

Используйте это свойство, чтобы проверить, была ли AppMetrica уже активирована, как правило, чтобы избежать избыточных вызовов активации или убедиться, что сбор статистики запущен.

{% endnote %}

### isLocationTrackingEnabled {#property_locationTrackingEnabled}

```swift translate=no
var isLocationTrackingEnabled: Bool { get; set; }
```

Включает/отключает [отправку информации о местоположении устройства](../ios-operations.md#track-location).

### libraryVersion {#property_libraryVersion}

```swift translate=no
var libraryVersion: String { get; }
```

Возвращает текущую версию библиотеки AppMetrica.

### userProfileID {#property_userProfileID}

```swift translate=no
var userProfileID: String? { get; set; }
```

Устанавливает ID для [пользовательского профиля](../../../../data-collection/about-profiles.md). Если отправка `ProfileId` не настроена, [предопределенные атрибуты](../../../../data-collection/profile-attributes.md#pre-defined) не отображаются в веб-интерфейсе.

### uuid {#property_UUID}

```swift translate=no
var uuid: String { get; }
```

Извлекает текущий UUID.
