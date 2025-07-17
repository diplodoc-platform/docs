# ErrorRepresentable protocol

Protocol for errors that can be sent in AppMetrica.

Each class instance that implements the protocol must have an ID. AppMetrica uses IDs to group errors.

All error information that is sent is available in AppMetrica reports.

You can implement this protocol to send custom errors. You can also use the default [AppMetricaError](AppMetricaError.md) implementation.

## Properties {#property_summary}

#|
|| [identifier](#property_identifier) | Error ID. AppMetrica uses it to group errors. ||
|| [message](#property_message) | Arbitrary error description. ||
|| [parameters](#property_parameters) | Additional error parameters. ||
|| [backtrace](#property_backtrace) | Custom error backtrace. You can get it using the `Thread.callStackReturnAddresses` method. ||
|| [underlyingError](#property_underlyingError) | Error instance that matches the `ErrorRepresentable` protocol. ||
|#

## Property descriptions {#property_detail}

### identifier {#property_identifier}

```swift translate=no
var identifier: String { get }
```

Error ID. AppMetrica uses it to group errors.

The maximum value length is 300 characters. If the value exceeds the limit, AppMetrica truncates it.

{% note info %}

AppMetrica doesn't use nested error (underlyingError) IDs for grouping.

{% endnote %}

### message {#property_message}

```swift translate=no
optional var message: String? { get }
```

Arbitrary error description.

The maximum value length is 1000 characters. If the value exceeds the limit, AppMetrica truncates it.

### parameters {#property_parameters}

```swift translate=no
optional var parameters: [String : Any]? { get }
```

Additional error parameters.

Parameters are represented as key-value pairs, where the key and value are strings. If the key or value differs from the string type, AppMetrica calls the `description` method automatically.

The maximum number of parameters is 50. The maximum allowed parameter size is 100 characters for the key and 2000 characters for the value. If the value exceeds the limit, AppMetrica truncates it.

### backtrace {#property_backtrace}

```swift translate=no
optional var backtrace: [NSNumber]? { get }
```

Custom error backtrace. You can get it using the `Thread.callStackReturnAddresses` method.

The maximum number of stack frames is 200. If the value exceeds the limit, AppMetrica truncates it.

### underlyingError {#property_underlyingError}

```swift translate=no
optional var underlyingError: ErrorRepresentable? { get }
```

Error instance that matches the `ErrorRepresentable` protocol.

The maximum number of nested errors is 10. If the value exceeds the limit, AppMetrica truncates it.
