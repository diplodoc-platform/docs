# AppMetricaCrashes class

This class provides functions for sending error and crash messages for AppMetrica integration.

## Instance methods {#instance_summary}

#|
|| [crashes(crashes())](#method_crashes) | Accesses the `AppMetricaCrashes` singleton. ||
|| [setConfiguration()](#method_setConfiguration) | Configures the error reporting mechanism for the app. ||
|| [reportNSError(_:onFailure:)](#method_reportNSError_onFailure) | Sends an `NSError` message to AppMetrica. ||
|| [reportNSError(_:options:onFailure:)](#method_reportNSError_options_onFailure) | Sends an `NSError` message with additional options for message customization. ||
|| [reportError(_:onFailure:)](#method_reportNSError_onFailure) | Sends a message about an error matching the `ErrorRepresentable` protocol. ||
|| [reportError(_:options:onFailure:)](#method_reportNSError_options_onFailure) | Sends a message about an error matching the `ErrorRepresentable` protocol, with additional options for message customization. ||
|| [setErrorEnvironmentValue(_:forKey:)](#method_setErrorEnvironmentValue_forKey) | Sets the key-value pair that will be associated with errors and crashes. ||
|| [clearErrorEnvironment()](#method_clearErrorEnvironment) | Deletes all key-value pairs associated with errors and crashes. ||
|| [requestCrashReportingState(WithCompletionQueue:completionBlock:)](#method_requestCrashReportingStateWithCompletionQueue_completionBlock) | Requests the current crash status. ||
|| [enableANRMonitoring()](#method_enableANRMonitoring) | Enables ANR monitoring with default parameters. ||
|| [enableANRMonitoring(WithWatchdogInterval:pingInterval:)](#method_enableANRMonitoringWithWatchdogInterval_pingInterval) | Enables ANR monitoring with custom parameters. ||
|| [reporter(ForAPIKey:)](#method_reporterForAPIKey) | Returns an `id<AppMetricaCrashReporting>` that can send messages to a specific API key. ||
|| [pluginExtension()](#method_pluginExtension) | Creates an `AppMetricaPlugins` instance that can send plugin events to the main API key. ||
|#

## Method descriptions {#method_detail}

### crashes(crashes()) {#method_crashes}

```swift translate=no
class crashes(crashes()) as? Self!
```

Accesses the `AppMetricaCrashes` singleton.

**Returns:**

The `AppMetricaCrashes` singleton.

### setConfiguration() {#method_setConfiguration}

```swift translate=no
class func setConfiguration(_ configuration: AppMetricaCrashesConfiguration?)
```

Configures the error messaging mechanism for the app. To enable or disable specific types of error messages and configure associated parameters, use the properties of the [AppMetricaCrashesConfiguration](AppMetricaCrashesConfiguration.md) class. Once set up, the configuration controls how the app handles different types of errors and issues.

**Parameter:**

#|
|| `configuration` | [AppMetricaCrashesConfiguration](AppMetricaCrashesConfiguration.md) object that defines how the app handles and reports errors. ||
|#

**Example:**

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

### clearErrorEnvironment() {#method_clearErrorEnvironment}

```swift translate=no
class func clearErrorEnvironment()
```

Deletes all previously set key-value pairs associated with errors and crashes.

This method ensures that future unhandled exceptions won't have any extra information added, unless you set new key-value pairs.

To set a key-value pair, use [-setErrorEnvironmentValue:forKey:](#method_setErrorEnvironmentValue_forKey).


### requestCrashReportingState(WithCompletionQueue:completionBlock:) {#method_requestCrashReportingStateWithCompletionQueue_completionBlock}

```swift translate=no
class func requestCrashReportingState(withCompletionQueue completionQueue: DispatchQueue, completionBlock: CrashReportingStateCompletionBlock)
```

This method asynchronously fetches the current status of error messages and returns it via the completion block.

For more information about the dictionary with keys and their associated values, see `CrashReportingStateCompletionBlock`.

**Parameters:**

#|
|| `completionQueue` | Message queue that executes the completion block. ||
|| `completionBlock` | Block to execute after completing the request. ||
|#

### enableANRMonitoring() {#method_enableANRMonitoring}

```swift translate=no
class func enableANRMonitoring()
```

Enables "Application Not Responding" (ANR) status monitoring with default parameters.

Use this method to enable ANR monitoring after activation only. To enable ANR monitoring during activation, use the `applicationNotRespondingDetection` property in [AppMetricaCrashesConfiguration](AppMetricaCrashesConfiguration.md).

Default parameters:

- `watchdog`: 4 seconds
- `ping`: 0.1 seconds

### enableANRMonitoring(WithWatchdogInterval:pingInterval:) {#method_enableANRMonitoringWithWatchdogInterval_pingInterval}

```swift translate=no
class func enableANRMonitoring(withWatchdogInterval watchdog: TimeInterval, pingInterval ping: TimeInterval)
```

Enables "Application Not Responding" (ANR) status monitoring after activation only. To enable ANR monitoring during activation, use the `applicationNotRespondingDetection` property in [AppMetricaCrashesConfiguration](AppMetricaCrashesConfiguration.md).

**Parameters:**

#|
|| `watchdog` | The timeout period before `watchdog` reports the "Application Not Responding" (ANR) status. ||
|| `ping` | Frequency at which `watchdog` checks for the "Application Not Responding" (ANR) status. Reducing the `ping` interval may lead to a decrease in app performance. ||
|#

### reporter(ForAPIKey:) {#method_reporterForAPIKey}

```swift translate=no
class func reporter(forAPIKey apiKey: String?) -> (any AppMetricaCrashReporting)?
```

Returns an `id<AppMetricaCrashReporting>` that can send messages to a specific API key.

**Parameter:**

#|
|| `apiKey` | API key to send error reports to. ||
|#

**Returns:**

An `id<AppMetricaCrashReporting>` that matches the `AppMetricaCrashReporting` protocol and allows
sending messages to a specific API key.

### pluginExtension() {#method_pluginExtension}

```swift translate=no
class func pluginExtension() -> (any AppMetricaPlugins)?
```

Creates an `AppMetricaPlugins` instance that can send plugin events to the main API key. You can request it every time or store a reference for future use. To use this extension, first activate AppMetrica with the `[AppMetrica activateWithConfiguration:]` method.

**Returns:**

A plugin extension instance.
