# AMAAppMetricaCrashes class

This class provides functions for sending error and crash messages for AppMetrica integration.

## Instance methods {#instance_summary}

#|
|| [+crashes:](#method_crashes) | Accesses the `AMAAppMetricaCrashes` singleton. ||
|| [-setConfiguration:](#method_setConfiguration) | Configures the error messaging mechanism for the app. ||
|| [-reportNSError:onFailure:](#method_reportNSError_onFailure) | Sends an `NSError` message to AppMetrica. ||
|| [-reportNSError:options:onFailure:](#method_reportNSError_options_onFailure) | Sends an `NSError` message with additional options for message customization. ||
|| [-reportError:onFailure:](#method_reportNSError_onFailure) | Sends a message about an error matching the `AMAErrorRepresentable` protocol. ||
|| [-reportError:options:onFailure:](#method_reportNSError_options_onFailure) | Sends a message about an error matching the `AMAErrorRepresentable` protocol, with additional options for message customization. ||
|| [-setErrorEnvironmentValue:forKey:](#method_setErrorEnvironmentValue_forKey) | Sets the key-value pair that will be associated with errors and crashes. ||
|| [-clearErrorEnvironment:](#method_clearErrorEnvironment) | Deletes all key-value pairs associated with errors and crashes. ||
|| [-requestCrashReportingStateWithCompletionQueue:completionBlock:](#method_requestCrashReportingStateWithCompletionQueue_completionBlock) | Requests the current crash status. ||
|| [-enableANRMonitoring:](#method_enableANRMonitoring) | Enables ANR monitoring with default parameters. ||
|| [-enableANRMonitoringWithWatchdogInterval:pingInterval:](#method_enableANRMonitoringWithWatchdogInterval_pingInterval) | Enables ANR monitoring with custom parameters. ||
|| [-reporterForAPIKey:](#method_reporterForAPIKey) | Returns an `id<AMAAppMetricaCrashReporting>` that can send messages to a specific API key. ||
|| [-pluginExtension:](#method_pluginExtension) | Creates an `AMAAppMetricaPlugins` instance that can send plugin events to the main API key. ||
|#

## Method descriptions {#method_detail}

### +crashes: {#method_crashes}

```objectivec translate=no
+ (instancetype)crashes (crashes())
```

Accesses the `AMAAppMetricaCrashes` singleton.

**Returns:**

The `AMAAppMetricaCrashes` singleton.

### -setConfiguration: {#method_setConfiguration}

```objectivec translate=no
- (void)setConfiguration:(AMAAppMetricaCrashesConfiguration *)configuration;
```

Configures the error messaging mechanism for the app. To enable or disable specific types of error messages and configure associated parameters, use the properties of the [AMAAppMetricaCrashesConfiguration](AMAAppMetricaCrashesConfiguration.md) class. Once set up, the configuration controls how the app handles different types of errors and issues.

**Parameter:**

#|
|| `configuration` | [AMAAppMetricaCrashesConfiguration](AMAAppMetricaCrashesConfiguration.md) object that defines how the app handles and reports errors. ||
|#

**Example:**

```objectivec translate=no
AMAAppMetricaCrashesConfiguration *config = [AMAAppMetricaCrashesConfiguration new];
config.autoCrashTracking = YES;
config.probablyUnhandledCrashReporting = NO;
config.applicationNotRespondingDetection = YES;
config.applicationNotRespondingWatchdogInterval = 5.0;
[[AMAAppMetricaCrashes crashes] setConfiguration:config];
```

### -reportNSError:onFailure: {#method_reportNSError_onFailure}

```objectivec translate=no
- (void)reportNSError:(NSError *)error
            onFailure:(nullable void (^)(NSError *error))onFailure report(nserror:onFailure:);
```

Sends an `NSError` message that is subject to certain restrictions on `domain`, `userInfo`, and other properties.

You can enable `NSError` backtracing by using the `AMABacktraceErrorKey` constant in the `userInfo` property.

Restrictions:

- `domain`: No more than 200 characters.
- `userInfo`: No more than 50 key-value pairs with keys no longer than 100 characters and values no longer than 2000 characters.
- `NSUnderlyingErrorKey`: Using this key in `userInfo` enables you to include up to 10 errors.
- `AMABacktraceErrorKey`: Using this key in `userInfo` enables you to include up to 200 stack frames in the backtrace.

AppMetrica truncates the value if it exceeds the specified limit.

**Parameters:**

#|
|| `error` | The `NSError` object that represents the error to be reported. AppMetrica uses the `domain` and `code` properties to group errors. ||
|| `OnFailure` | Callback method to call if an error occurs while sending the message. The `error` is passed as an argument. ||
|#

### -reportNSError:options:onFailure: {#method_reportNSError_options_onFailure}

```objectivec translate=no
- (void)reportNSError:(NSError *)error
              options:(AMAErrorReportingOptions)options
            onFailure:(nullable void (^)(NSError *error))onFailure report(nserror:options:onFailure:);
```

Sends a custom `NSError` message that adheres to the restrictions on `domain`, `userInfo`, and other properties.

You can enable `NSError` backtracing by using the `AMABacktraceErrorKey` constant in the `userInfo` property.

Restrictions:

- `domain`: No more than 200 characters.
- `userInfo`: No more than 50 key-value pairs with keys no longer than 100 characters and values no longer than 2000 characters.
- `NSUnderlyingErrorKey`: Using this key in `userInfo` enables you to include up to 10 errors.
- `AMABacktraceErrorKey`: Using this key in `userInfo` enables you to include up to 200 stack frames in the backtrace.

AppMetrica truncates the value if it exceeds any of these limits.

**Parameters:**

#|
|| `error` | The `NSError` object that represents the error to be reported. AppMetrica uses the `domain` and `code` properties to group errors. ||
|| `options` | Additional [AMAErrorReportingOptions](AMAErrorReportingOptions.md) options that define how the error message is sent. ||
|| `OnFailure` | Callback method to call if an error occurs while sending the message. The `error` is passed as an argument. ||
|#

### -reportError:onFailure: {#method_reportNSError_onFailure}

```objectivec translate=no
- (void)reportError:(id<AMAErrorRepresentable>)error
          onFailure:(nullable void (^)(NSError *error))onFailure report(error:onFailure:);
```

Sends a message about an error matching the [AMAErrorRepresentable](AMAErrorRepresentable.md) protocol.

**Parameters:**

#|
|| `error` | Error that matches the `AMAErrorRepresentable` protocol. ||
|| `OnFailure` | Callback method to call if an error occurs while sending the message. The `error` is passed as an argument. ||
|#

### -reportError:options:onFailure: {#method_reportNSError_options_onFailure}

```objectivec translate=no
- (void)reportError:(id<AMAErrorRepresentable>)error
            options:(AMAErrorReportingOptions)options
          onFailure:(nullable void (^)(NSError *error))onFailure report(error:options:onFailure:);
```

Sends a message about an error matching the [AMAErrorRepresentable](AMAErrorRepresentable.md) protocol, with additional options for message customization.

**Parameters:**

#|
|| `error` | Error that matches the `AMAErrorRepresentable` protocol. ||
|| `options` | Additional [AMAErrorReportingOptions](AMAErrorReportingOptions.md) options that define how the error message is sent. ||
|| `OnFailure` | Callback method to call if an error occurs while sending the message. The `error` is passed as an argument. ||
|#

### -setErrorEnvironmentValue:forKey: {#method_setErrorEnvironmentValue_forKey}

```objectivec translate=no
- (void)setErrorEnvironmentValue:(nullable NSString *)value
                          forKey:(NSString *)key set(errorEnvironmentValue:forKey:);
```

Sets the key-value pair that will be associated with errors and crashes. AppMetrica uses it as additional information for unhandled exceptions.

**Parameters:**

#|
|| `value` | Value to associate with the key. Passing `nil` deletes the previously set key-value pair. ||
|| `key` | Key associated with the value. ||
|#

### -clearErrorEnvironment: {#method_clearErrorEnvironment}

```objectivec translate=no
- (void)clearErrorEnvironment;
```

Deletes all previously set key-value pairs associated with errors and crashes.

This method ensures that future unhandled exceptions won't have any extra information added, unless you set new key-value pairs.

To set a key-value pair, use [-setErrorEnvironmentValue:forKey:](#method_setErrorEnvironmentValue_forKey).


### -requestCrashReportingStateWithCompletionQueue:completionBlock: {#method_requestCrashReportingStateWithCompletionQueue_completionBlock}

```objectivec translate=no
- (void)requestCrashReportingStateWithCompletionQueue:(dispatch_queue_t)completionQueue
                                      completionBlock:(AMACrashReportingStateCompletionBlock)completionBlock;
```

This method asynchronously fetches the current status of error messages and returns it via the completion block.

For more information about the dictionary with keys and their associated values, see `AMACrashReportingStateCompletionBlock`.

**Parameters:**

#|
|| `completionQueue` | Message queue that executes the completion block. ||
|| `completionBlock` | Block to execute after completing the request. ||
|#

### -enableANRMonitoring: {#method_enableANRMonitoring}

```objectivec translate=no
- (void)enableANRMonitoring;
```

Enables "Application Not Responding" (ANR) status monitoring with default parameters.

Use this method to enable ANR monitoring after activation only. To enable ANR monitoring during activation, use the `applicationNotRespondingDetection` property in [AMAAppMetricaCrashesConfiguration](AMAAppMetricaCrashesConfiguration.md).

Default parameters:

- `watchdog`: 4 seconds
- `ping`: 0.1 seconds

### -enableANRMonitoringWithWatchdogInterval:pingInterval: {#method_enableANRMonitoringWithWatchdogInterval_pingInterval}

```objectivec translate=no
- (void)enableANRMonitoringWithWatchdogInterval:(NSTimeInterval)watchdog
                                   pingInterval:(NSTimeInterval)ping;
```

Enables "Application Not Responding" (ANR) status monitoring after activation only. To enable ANR monitoring during activation, use the `applicationNotRespondingDetection` property in [AMAAppMetricaCrashesConfiguration](AMAAppMetricaCrashesConfiguration.md).

**Parameters:**

#|
|| `watchdog` | The timeout period before `watchdog` reports the "Application Not Responding" (ANR) status. ||
|| `ping` | Frequency at which `watchdog` checks for the "Application Not Responding" (ANR) status. Reducing the `ping` interval may lead to a decrease in app performance. ||
|#

### -reporterForAPIKey: {#method_reporterForAPIKey}

```objectivec translate=no
- (nullable id<AMAAppMetricaCrashReporting>)reporterForAPIKey:(NSString *)apiKey reporter(for:);
```

Returns an `id<AMAAppMetricaCrashReporting>` that can send messages to a specific API key.

**Parameter:**

#|
|| `apiKey` | API key to send error reports to. ||
|#

**Returns:**

An `id<AMAAppMetricaCrashReporting>` that matches the `AMAAppMetricaCrashReporting` protocol and allows
sending messages to a specific API key.

### -pluginExtension: {#method_pluginExtension}

```objectivec translate=no
- (id<AMAAppMetricaPlugins>)pluginExtension;
```

Creates an `AMAAppMetricaPlugins` instance that can send plugin events to the main API key. You can request it every time or store a reference for future use. To use this extension, first activate AppMetrica with the `[AMAAppMetrica activateWithConfiguration:]` method.

**Returns:**

A plugin extension instance.
