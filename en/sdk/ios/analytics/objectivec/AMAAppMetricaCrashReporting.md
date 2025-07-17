# AMAAppMetricaCrashReporting protocol

The `AMAAppMetricaCrashReporting` protocol contains methods for customizing error and crash messages.

## Instance methods {#instance_summary}

#|
|| [-reportNSError:onFailure:](#method_reportNSError_onFailure) | Sends an `NSError` message to AppMetrica. ||
|| [-reportNSError:options:onFailure:](#method_reportNSError_options_onFailure) | Sends an `NSError` message with additional options for message customization. ||
|| [-reportError:onFailure:](#method_reportNSError_onFailure) | Sends a message about an error matching the `AMAErrorRepresentable` protocol. ||
|| [-reportError:options:onFailure:](#method_reportNSError_options_onFailure) | Sends a message about an error matching the `AMAErrorRepresentable` protocol, with additional options for message customization. ||
|| [-setErrorEnvironmentValue:forKey:](#method_setErrorEnvironmentValue_forKey) | Sets the key-value pair that will be associated with errors and crashes. ||
|| [-pluginExtension:](#method_pluginExtension) | Creates an `AMAAppMetricaPlugins` instance that can send plugin events to the main API key. ||
|#

## Method descriptions {#method_detail}

### -reportNSError:onFailure: {#method_reportNSErro_onFailure}

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

### -pluginExtension: {#method_pluginExtension}

```objectivec translate=no
- (id<AMAAppMetricaPlugins>)pluginExtension;
```

Creates an `AMAAppMetricaPlugins` instance that can send plugin events to the main API key. You can request it every time or store a reference for future use. To use this extension, first activate AppMetrica with the `[AMAAppMetrica activateWithConfiguration:]` method.

**Returns:**

A plugin extension instance.
