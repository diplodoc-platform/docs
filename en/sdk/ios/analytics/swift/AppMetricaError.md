# AppMetricaError class

A simple implementation of the [ErrorRepresentable](ErrorRepresentable.md) protocol.

## Instance methods {#instance_summary}

#|
|| [init(identifier:)](#method_errorWithIdentifier) | Creates the `AppMetricaError` instance with the specified ID. ||
|| [init(identifier:message:parameters:)](#method_errorWithIdentifier_message_params) | Creates the `AppMetricaError` instance with the specified ID and other parameters. ||
|| [init(identifier:message:parameters:backtrace:underlyingError:)](#method_errorWithIdentifier_message_params_backtrace_underlyingError) | Creates the `AppMetricaError` instance of the user with the specified ID and other parameters. ||
|#

## Method descriptions {#method_detail}

### init(identifier:) {#method_errorWithIdentifier}

```swift translate=no
convenience init(identifier: String)
```

Creates the `AppMetricaError` instance with the specified ID.

**Parameters:**

#|
|| `identifier` | Error ID. AppMetrica uses it to group errors. ||
|#

**Returns:**

The `AppMetricaError` class instance.

### init(identifier:message:parameters:) {#method_errorWithIdentifier_message_params}

```swift translate=no
convenience init(identifier: String, message: String?, parameters: [String : Any]?)
```

Creates the `AppMetricaError` instance with the specified ID and other parameters.

**Parameters:**

#|
|| `identifier` | Error ID. AppMetrica uses it to group errors. ||
|| `message` | Arbitrary error description. ||
|| `parameters` | Additional error parameters. ||
|#

**Returns:**

The `AppMetricaError` class instance.

### init(identifier:message:parameters:backtrace:underlyingError:) {#method_errorWithIdentifier_message_params_backtrace_underlyingError}

```swift translate=no
convenience init(identifier: String, message: String?, parameters: [String : Any]?, backtrace: [NSNumber]?, underlyingError: ErrorRepresentable?)
```

Creates the `AppMetricaError` instance of the user with the specified ID and other parameters.

**Parameters:**

#|
|| `identifier` | Error ID. AppMetrica uses it to group errors. ||
|| `message` | Arbitrary error description. ||
|| `parameters` | Additional error parameters. ||
|| `backtrace` | Custom error backtrace. ||
|| `underlyingError` | Error instance that matches the [ErrorRepresentable](ErrorRepresentable.md) protocol. ||
|#

**Returns:**

The `AppMetricaError` class instance.
