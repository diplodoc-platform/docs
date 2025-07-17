# AppMetricaCrashReporting protocol

The `AppMetricaCrashReporting` protocol contains methods for customizing error and crash messages.

## Instance methods {#instance_summary}

#|
|| [reportNSError(_:onFailure:)](#method_reportNSErro_onFailure) | Sends an `NSError` message in AppMetrica. ||
|| [reportNSError(_:options:onFailure:)](#method_reportNSError_options_onFailure) | Sends an `NSError` message with additional options for message customization. ||
|| [reportError(_:onFailure:)](#method_reportNSError_onFailure) | Sends a message about an error matching the `ErrorRepresentable` protocol. ||
|| [reportError(_:options:onFailure:)](#method_reportNSError_options_onFailure) | Sends a message about an error matching the `ErrorRepresentable` protocol, with additional options for message customization. ||
|| [setErrorEnvironmentValue(_:forKey:)](#method_setErrorEnvironmentValue_forKey) | Sets the key-value pair that will be associated with errors and crashes. ||
|| [pluginExtension()](#method_pluginExtension) | Creates an `AppMetricaPlugins` instance that can send plugin events to the main API key. ||
|#

## Method descriptions {#method_detail}

### reportNSError(_:onFailure:) {#method_reportNSErro_onFailure}

```swift translate=no
class func reportNSError(_ error: (any Error)?, onFailure: ((_ error: (any Error)?) -> Void)? = nil)
```

Sends an `NSError` message that is subject to certain restrictions on `domain`, `userInfo`, and other properties.

You can enable `NSError` backtracing by using the `BacktraceErrorKey` constant in the `userInfo` property.

Restrictions:

- `domain`: No more than 200 characters.
- `userInfo`: No more than 50 key-value pairs with keys no longer than 100 characters and values no longer than 2000 characters.
- `NSUnderlyingErrorKey`: Using this key in `userInfo` enables you to include up to 10 errors.
- `BacktraceErrorKey`: Using this key in `userInfo` allows you to include up to 200 stack frames in the backtrace.

AppMetrica truncates the value if it exceeds the specified limit.

**Parameters:**

#|
|| `error` | The `NSError` object that represents the error to be reported. AppMetrica uses the `domain` and `code` properties to group errors. ||
|| `OnFailure` | Callback method to call if an error occurs while sending the message. The `error` is passed as an argument. ||
|#

### reportNSError(_:options:onFailure:) {#method_reportNSError_options_onFailure}

```swift translate=no
class func reportNSError(_ error: (any Error)?, options: ErrorReportingOptions, onFailure: ((_ error: (any Error)?) -> Void)? = nil)
```

Sends a custom `NSError` message that adheres to the restrictions on `domain`, `userInfo`, and other properties.

You can enable `NSError` backtracing by using the `BacktraceErrorKey` constant in the `userInfo` property.

Restrictions:

- `domain`: No more than 200 characters.
- `userInfo`: No more than 50 key-value pairs with keys no longer than 100 characters and values no longer than 2000 characters.
- `NSUnderlyingErrorKey`: Using this key in `userInfo` enables you to include up to 10 errors.
- `BacktraceErrorKey`: Using this key in `userInfo` allows you to include up to 200 stack frames in the backtrace.

AppMetrica truncates the value if it exceeds any of these limits.

**Parameters:**

#|
|| `error` | The `NSError` object that represents the error to be reported. AppMetrica uses the `domain` and `code` properties to group errors. ||
|| `options` | Additional [ErrorReportingOptions](ErrorReportingOptions.md) options that define how the error message is sent. ||
|| `OnFailure` | Callback method to call if an error occurs while sending the message. The `error` is passed as an argument. ||
|#

### reportError(_:onFailure:) {#method_reportNSError_onFailure}

```swift translate=no
class func reportError(_ error: (any ErrorRepresentable)?, onFailure: ((_ error: (any Error)?) -> Void)? = nil)
```

Sends a message about an error matching the [ErrorRepresentable](ErrorRepresentable.md) protocol.

**Parameters:**

#|
|| `error` | Error that matches the `ErrorRepresentable` protocol. ||
|| `OnFailure` | Callback method to call if an error occurs while sending the message. The `error` is passed as an argument. ||
|#

### reportError(_:options:onFailure:) {#method_reportNSError_options_onFailure}

```swift translate=no
class func reportError(_ error: (any ErrorRepresentable)?, options: ErrorReportingOptions, onFailure: ((_ error: (any Error)?) -> Void)? = nil)
```

Sends a message about an error matching the [ErrorRepresentable](ErrorRepresentable.md) protocol, with additional options for message customization.

**Parameters:**

#|
|| `error` | Error that matches the `ErrorRepresentable` protocol. ||
|| `options` | Additional [ErrorReportingOptions](ErrorReportingOptions.md) options that define how the error message is sent. ||
|| `OnFailure` | Callback method to call if an error occurs while sending the message. The `error` is passed as an argument. ||
|#

### setErrorEnvironmentValue(_:forKey:) {#method_setErrorEnvironmentValue_forKey}

```swift translate=no
class func setErrorEnvironmentValue(_ value: String?, forKey key: String?)
```

Sets the key-value pair that will be associated with errors and crashes. AppMetrica uses it as additional information for unhandled exceptions.

**Parameters:**

#|
|| `value` | Value to associate with the key. Passing `nil` deletes the previously set key-value pair. ||
|| `key` | Key associated with the value. ||
|#

### pluginExtension() {#method_pluginExtension}

```swift translate=no
class func pluginExtension() -> (any AppMetricaPlugins)?
```

Creates an `AppMetricaPlugins` instance that can send plugin events to the main API key. You can request it every time or store a reference for future use. To use this extension, first activate AppMetrica with the `[AppMetrica activateWithConfiguration:]` method.

**Returns:**

A plugin extension instance.
