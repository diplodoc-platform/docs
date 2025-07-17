# Класс AppMetricaCrashes

Класс предоставляет функции отправки сообщений об ошибках и сбоях для интеграции с AppMetrica.

## Методы экземпляра {#instance_summary}

#|
|| [crashes(crashes())](#method_crashes) | Получает доступ к синглтону `AppMetricaCrashes`. ||
|| [setConfiguration()](#method_setConfiguration) | Настраивает для приложения конфигурацию механизма отправки сообщений о сбоях. ||
|| [reportNSError(_:onFailure:)](#method_reportNSError_onFailure) | Отправляет сообщение об ошибке типа `NSError` в AppMetrica. ||
|| [reportNSError(_:options:onFailure:)](#method_reportNSError_options_onFailure) | Отправляет сообщение об ошибке типа `NSError` с дополнительными возможностями кастомизации сообщения. ||
|| [reportError(_:onFailure:)](#method_reportNSError_onFailure) | Отправляет сообщение об ошибке, соответствующей протоколу `ErrorRepresentable`. ||
|| [reportError(_:options:onFailure:)](#method_reportNSError_options_onFailure) | Отправляет сообщение об ошибке, соответствующей протоколу `ErrorRepresentable`, с дополнительными возможностями кастомизации сообщения. ||
|| [setErrorEnvironmentValue(_:forKey:)](#method_setErrorEnvironmentValue_forKey) | Устанавливает пару «ключ-значение», которая будет связана с ошибками и сбоями. ||
|| [clearErrorEnvironment()](#method_clearErrorEnvironment) | Удаляет все пары «ключ-значение», связанные с ошибками и сбоями. ||
|| [requestCrashReportingState(WithCompletionQueue:completionBlock:)](#method_requestCrashReportingStateWithCompletionQueue_completionBlock) | Запрашивает текущее состояние о сбоях. ||
|| [enableANRMonitoring()](#method_enableANRMonitoring) | Включает ANR-мониторинг с параметрами по умолчанию. ||
|| [enableANRMonitoring(WithWatchdogInterval:pingInterval:)](#method_enableANRMonitoringWithWatchdogInterval_pingInterval) | Включает ANR-мониторинг с указанными параметрами. ||
|| [reporter(ForAPIKey:)](#method_reporterForAPIKey) | Возвращает `id<AppMetricaCrashReporting>`, который может отправлять ошибки на определенный ключ API. ||
|| [pluginExtension()](#method_pluginExtension) | Создает `AppMetricaPlugins`, который может отправлять события плагина в основной ключ API. ||
|#

## Описание методов {#method_detail}

### crashes(crashes()) {#method_crashes}

```swift translate=no
class crashes(crashes()) as? Self!
```

Получает доступ к синглтону `AppMetricaCrashes`.

**Возвращает:**

Экземпляр синглтона `AppMetricaCrashes`.

### setConfiguration() {#method_setConfiguration}

```swift translate=no
class func setConfiguration(_ configuration: AppMetricaCrashesConfiguration?)
```

Настраивает для приложения конфигурацию механизма отправки сообщений о сбоях. Чтобы включить или отключить определенные типы сообщений о сбоях, а также настроить связанные параметры, используйте свойства класса [AppMetricaCrashesConfiguration](AppMetricaCrashesConfiguration.md). После настройки конфигурация будет управлять тем, как приложение обрабатывает различные типы сбоев и проблем.

**Параметр:**

#|
|| `configuration` | Объект [AppMetricaCrashesConfiguration](AppMetricaCrashesConfiguration.md), который определяет, как приложение должно обрабатывать сбои и сообщать о них. ||
|#

**Пример:**

```swift translate=no
let config = AppMetricaCrashesConfiguration()
config.autoCrashTracking = true
config.probablyUnhandledCrashReporting = false
config.applicationNotRespondingDetection = true
config.applicationNotRespondingWatchdogInterval = 5.0
AppMetricaCrashes().configuration = config
```

### reportNSError(_:onFailure:) {#method_reportNSError_onFailure} 

```swift translate=no
class func reportNSError(_ error: (any Error)?, onFailure: ((_ error: (any Error)?) -> Void)? = nil) 
```

Отправляет сообщение об ошибке типа `NSError`, которые соответствуют определенным ограничениям на `domain`, `userInfo` и другие свойства.

Можно включить обратную трассировку в `NSError`, используя константу `BacktraceErrorKey` в `userInfo`.

Ограничения:

- `domain` — не более 200 символов.
- `userInfo` — Не более 50 пар «ключ-значение», длина ключа — не более 100 символов, длина значения — не более 2000 символов.
- `NSUnderlyingErrorKey` — Используя этот ключ в `userInfo`, можно включить не более 10 ошибок.
- `BacktraceErrorKey` — Используя этот ключ в `userInfo`, можно включить максимум 200 стековых кадров в обратную трассировку.

Если значение превысит указанное ограничение, AppMetrica обрежет его.

**Параметры:**

#|
|| `error` | Объект `NSError` — ошибка, о которой нужно сообщить. Свойства `domain` и `code` используются для группировки ошибок. ||
|| `OnFailure` | Callback-метод, который будет вызван при сбое передачи сообщения. Ошибка `error` передается в качестве аргумента. ||
|#

### reportNSError(_:options:onFailure:) {#method_reportNSError_options_onFailure}

```swift translate=no
class func reportNSError(_ error: (any Error)?, options: ErrorReportingOptions, onFailure: ((_ error: (any Error)?) -> Void)? = nil) 
```

Отправляет кастомизированное сообщение об ошибке типа `NSError`, соблюдая ограничения для свойств `domain`, `userInfo` и других.

Можно включить обратную трассировку в `NSError`, используя константу `BacktraceErrorKey` в `userInfo`.

Ограничения:

- `domain` — не более 200 символов.
- `userInfo` — Не более 50 пар «ключ-значение», длина ключа — не более 100 символов, длина значения — не более 2000 символов.
- `NSUnderlyingErrorKey` — Используя этот ключ в `userInfo`, можно включить не более 10 ошибок.
- `BacktraceErrorKey` — Используя этот ключ в `userInfo`, можно включить максимум 200 стековых кадров в обратную трассировку.

Если значение превысит любое из этих ограничений, AppMetrica обрежет его.

**Параметры:**

#|
|| `error` | Объект `NSError` — ошибка, о которой нужно сообщить. Свойства `domain` и `code` используются для группировки ошибок. ||
|| `options` | Дополнительные опции [ErrorReportingOptions](ErrorReportingOptions.md), которые определяют, как должно быть передано сообщение об ошибке. ||
|| `OnFailure` | Callback-метод, который будет вызван при сбое передачи сообщения. Ошибка `error` передается в качестве аргумента. ||
|#

### reportError(_:onFailure:) {#method_reportNSError_onFailure}

```swift translate=no
class func reportError(_ error: (any ErrorRepresentable)?, onFailure: ((_ error: (any Error)?) -> Void)? = nil) 
```

Отправляет сообщение об ошибке, соответствующей протоколу [ErrorRepresentable](ErrorRepresentable.md). 

**Параметры:**

#|
|| `error` | Ошибка, соответствующая протоколу `ErrorRepresentable`. ||
|| `OnFailure` | Callback-метод, который будет вызван при сбое передачи сообщения. Ошибка `error` передается в качестве аргумента. ||
|#

### reportError(_:options:onFailure:) {#method_reportNSError_options_onFailure}

```swift translate=no
class func reportError(_ error: (any ErrorRepresentable)?, options: ErrorReportingOptions, onFailure: ((_ error: (any Error)?) -> Void)? = nil)
```

Отправляет сообщение об ошибке, соответствующей протоколу [ErrorRepresentable](ErrorRepresentable.md), с дополнительными возможностями кастомизации сообщения.

**Параметры:**

#|
|| `error` | Ошибка, соответствующая протоколу `ErrorRepresentable`. ||
|| `options` | Дополнительные опции [ErrorReportingOptions](ErrorReportingOptions.md), которые определяют, как должно быть передано сообщение об ошибке. ||
|| `OnFailure` | Callback-метод, который будет вызван при сбое передачи сообщения. Ошибка `error` передается в качестве аргумента. ||
|#

### setErrorEnvironmentValue(_:forKey:) {#method_setErrorEnvironmentValue_forKey}

```swift translate=no
class func setErrorEnvironmentValue(_ value: String?, forKey key: String?)
```

Устанавливает пару «ключ-значение», которая будет связана с ошибками и сбоями. AppMetrica использует ее как дополнительную информацию для необработанных исключений.

**Параметры:**

#|
|| `value` | Значение, которое нужно связать с ключом. Если передать `nil`, ранее установленная пара «ключ-значение» с этим ключом будет удалена. ||
|| `key` | Ключ, с которым должно быть связано значение. ||
|#

### clearErrorEnvironment() {#method_clearErrorEnvironment}

```swift translate=no
class func clearErrorEnvironment()
```

Удаляет все ранее установленные пары «ключ-значение», связанные с ошибками и сбоями. 

Использование этого метода гарантирует, что никакая дополнительная информация не будет добавлена к будущим необработанным исключениям, если только не будут установлены новые пары «ключ-значение».

Чтобы установить пару «ключ-значение», используйте [-setErrorEnvironmentValue:forKey:](#method_setErrorEnvironmentValue_forKey).


### requestCrashReportingState(WithCompletionQueue:completionBlock:) {#method_requestCrashReportingStateWithCompletionQueue_completionBlock}

```swift translate=no
class func requestCrashReportingState(withCompletionQueue completionQueue: DispatchQueue, completionBlock: CrashReportingStateCompletionBlock) 
```

Метод асинхронно получает текущее состояние сообщений об ошибках и возвращает его через блок завершения.

Подробнее о словаре с ключами и связанными с ними значениями см. `CrashReportingStateCompletionBlock`.

**Параметры:**

#|
|| `completionQueue` | Очередь отправки сообщений, в которой выполняется блок завершения. ||
|| `completionBlock` | Блок, который должен быть выполнен после завершения запроса. ||
|#

### enableANRMonitoring() {#method_enableANRMonitoring}

```swift translate=no
class func enableANRMonitoring()
```

Включает мониторинг состояния «Приложение не отвечает» (ANR) с параметрами по умолчанию. 

Используйте этот метод, чтобы включить ANR-мониторинг только после активации. Чтобы включить ANR-мониторинг во время активации, используйте свойство `applicationNotRespondingDetection` в [AppMetricaCrashesConfiguration](AppMetricaCrashesConfiguration.md).

Параметры по умолчанию:

- `watchdog` — интервал 4 секунды;
- `ping`  — интервал 0,1 секунды.

### enableANRMonitoring(WithWatchdogInterval:pingInterval:) {#method_enableANRMonitoringWithWatchdogInterval_pingInterval}

```swift translate=no
class func enableANRMonitoring(withWatchdogInterval watchdog: TimeInterval, pingInterval ping: TimeInterval) 
```

Включает мониторинг состояния «Приложение не отвечает» (ANR) только после активации. Чтобы включить ANR-мониторинг во время активации, используйте свойство `applicationNotRespondingDetection` в [AppMetricaCrashesConfiguration](AppMetricaCrashesConfiguration.md).

**Параметры:**

#|
|| `watchdog` | Интервал времени, который будет ожидать `watchdog`, прежде чем сообщить о состоянии «Приложение не отвечает» (ANR). ||
|| `ping` | Частота, с которой `watchdog` будет проверять состояние «Приложение не отвечает» (ANR). Уменьшение интервала `ping` может привести к снижению производительности приложения. ||
|#

### reporter(ForAPIKey:) {#method_reporterForAPIKey}

```swift translate=no
class func reporter(forAPIKey apiKey: String?) -> (any AppMetricaCrashReporting)?
```

Возвращает `id<AppMetricaCrashReporting>`, который может отправлять ошибки на определенный ключ API.

**Параметр:**

#|
|| `apiKey` | API-ключ, на который нужно отправлять ошибки. ||
|#

**Возвращает:**

Идентификатор `id<AppMetricaCrashReporting>`, который соответствует `AppMetricaCrashReporting` и обеспечивает
отправку ошибок на определенный ключ API.

### pluginExtension() {#method_pluginExtension}

```swift translate=no
class func pluginExtension() -> (any AppMetricaPlugins)? 
```

Создает экземпляр `AppMetricaPlugins`, который может отправлять события плагина на основной ключ API. Можно запрашивать его каждый раз по необходимости или сохранить ссылку на него для повторного использования. Для использования этого расширения нужно сначала активировать AppMetrica с помощью `[AppMetrica activateWithConfiguration:]`.

**Возвращает:**

Экземпляр расширения плагина.
