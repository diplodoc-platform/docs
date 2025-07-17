# Протокол AppMetricaCrashReporting

Протокол `AppMetricaCrashReporting` содержит методы, которые используются для кастомизации сообщений об ошибках и сбоях.

## Методы экземпляра {#instance_summary}

#|
|| [reportNSError(_:onFailure:)](#method_reportNSErro_onFailure) | Отправляет сообщение об ошибке типа `NSError` в AppMetrica. ||
|| [reportNSError(_:options:onFailure:)](#method_reportNSError_options_onFailure) | Отправляет сообщение об ошибке типа `NSError` с дополнительными возможностями кастомизации сообщения. ||
|| [reportError(_:onFailure:)](#method_reportNSError_onFailure) | Отправляет сообщение об ошибке, соответствующей протоколу `ErrorRepresentable`. ||
|| [reportError(_:options:onFailure:)](#method_reportNSError_options_onFailure) | Отправляет сообщение об ошибке, соответствующей протоколу `ErrorRepresentable`, с дополнительными возможностями кастомизации сообщения. ||
|| [setErrorEnvironmentValue(_:forKey:)](#method_setErrorEnvironmentValue_forKey) | Устанавливает пару «ключ-значение», которая будет связана с ошибками и сбоями. ||
|| [pluginExtension()](#method_pluginExtension) | Создает `AppMetricaPlugins`, который может отправлять события плагина в основной ключ API. ||
|#

## Описание методов {#method_detail}

### reportNSError(_:onFailure:) {#method_reportNSErro_onFailure} 

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

### pluginExtension() {#method_pluginExtension}

```swift translate=no
class func pluginExtension() -> (any AppMetricaPlugins)?
```

Создает экземпляр `AppMetricaPlugins`, который может отправлять события плагина на основной ключ API. Можно запрашивать его каждый раз по необходимости или сохранить ссылку на него для повторного использования. Для использования этого расширения нужно сначала активировать AppMetrica с помощью `[AppMetrica activateWithConfiguration:]`.

**Возвращает:**

Экземпляр расширения плагина.
