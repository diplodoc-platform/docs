# Протокол AppMetricaPlugins

Протокол `AppMetricaPlugins` — это расширение `AppMetricaCrashes`.

Экземпляр объекта, который реализует `AppMetricaPlugins`, может быть получен с помощью метода [pluginExtension](AppMetricaCrashes.md#method_pluginExtension) в [AppMetricaCrashes](AppMetricaCrashes.md).

Для каждого репортера создается один экземпляр `AppMetricaPlugins`. Можно запрашивать его каждый раз по необходимости или сохранить ссылку на него для повторного использования. 

## Методы экземпляра {#instance_summary}

#|
|| [reportUnhandledException(_:onFailure:)](#method_reportUnhandledException_onFailure) | Отправляет сообщение о необработанной ошибке. ||
|| [reportError(_:message:onFailure:)](#method_reportError_message_onFailure) | Отправляет сообщение об ошибке. ||
|| [reportError(:withIdentifier:message:details:onFailure:)](#method_reportErrorWithIdentifier_message_details_onFailure) | Отправляет сообщение об ошибке c кратким описанием. ||
|#

## Описание методов {#method_detail}

### reportUnhandledException(_:onFailure:) {#method_reportUnhandledException_onFailure}

```swift translate=no
class func reportUnhandledException(_ errorDetails: PluginErrorDetails?, onFailure: ((_ error: (any Error)?) -> Void)? = nil)
```

Отправляет сообщение о необработанной ошибке. Подробнее см. [PluginErrorDetails](PluginErrorDetails.md).

**Параметры:**

#|
|| `errorDetails` | Объект, который описывает ошибку. ||
|| `onFailure` | Callback-метод, который будет вызван при сбое передачи сообщения. Ошибка `error` передается в качестве аргумента. ||
|#

### reportError(_:message:onFailure:) {#method_reportError_message_onFailure}

```swift translate=no
class func reportError(_ errorDetails: PluginErrorDetails?, message: String?, onFailure: ((_ error: (any Error)?) -> Void)? = nil) 
```

Отправляет сообщение об ошибке. Для группировки используется обратная трассировка `backtrace`. Чтобы изменить параметр группировки, используйте [reportErrorWithIdentifier:message:details:onFailure:](#method_reportErrorWithIdentifier_message_details_onFailure). Подробнее см. [PluginErrorDetails](PluginErrorDetails.md).

**Параметры:**

#|
|| `errorDetails` | Объект с детальной информацией об ошибке. ||
|| `message` | Краткое описание ошибки. ||
|| `onFailure` | Callback-метод, который будет вызван при сбое передачи сообщения. Ошибка `error` передается в качестве аргумента. ||
|#

### reportError(:withIdentifier:message:details:onFailure:) {#method_reportErrorWithIdentifier_message_details_onFailure}

```swift translate=no
class func reportError(withIdentifier identifier: String?, message: String?, details errorDetails: PluginErrorDetails?, onFailure: ((_ error: (any Error)?) -> Void)? = nil) 
```

Отправляет сообщение об ошибке c кратким описанием. Для группировки ошибок используется переданный идентификатор. Чтобы вместо него использовать для группировки обратную трассировку `backtrace`, используйте метод [reportError:message:onFailure:](#method_reportError_message_onFailure). Подробнее см. [PluginErrorDetails](PluginErrorDetails.md).


**Параметры:**

#|
|| `identifier` | Идентификатор, который используется для группировки. ||
|| `message` | Краткое описание ошибки. ||
|| `errorDetails` | Объект с детальной информацией об ошибке.  ||
|| `onFailure` | Callback-метод, который будет вызван при сбое передачи сообщения. Ошибка `error` передается в качестве аргумента. ||
|#
