# AMAErrorRepresentable protocol

Protocol for errors that can be sent in AppMetrica.

Each class instance that implements the protocol must have an ID. AppMetrica uses IDs to group errors.

All error information that is sent is available in AppMetrica reports.

You can implement this protocol to send custom errors. You can also use the default [AMAError](AMAError.md) implementation.

## Properties {#property_summary}

#|
|| [identifier](#property_identifier) | Error ID. AppMetrica uses it to group errors. ||
|| [message](#property_message) | Arbitrary error description. ||
|| [parameters](#property_parameters) | Additional error parameters. ||
|| [backtrace](#property_backtrace) | Custom error backtrace. You can get it using the `NSThread.callStackReturnAddresses` method. ||
|| [underlyingError](#property_underlyingError) | Error instance that matches the `AMAErrorRepresentable` protocol. ||
|#

## Property descriptions {#property_detail}

### identifier {#property_identifier}

```objectivec translate=no
@required
@property (readonly, copy, nonatomic) NSString *_Nonnull identifier;
```

Error ID. AppMetrica uses it to group errors.

The maximum value length is 300 characters. If the value exceeds the limit, AppMetrica truncates it.

{% note info %}

AppMetrica doesn't use nested error (`underlyingError`) IDs for grouping.

{% endnote %}

### message {#property_message}

```objectivec translate=no
@optional
@property (readonly, copy, nonatomic, nullable) NSString *message;
```

Arbitrary error description.

The maximum value length is 1000 characters. If the value exceeds the limit, AppMetrica truncates it.

### parameters {#property_parameters}

```objectivec translate=no
@optional
@property (readonly, copy, nonatomic, nullable) NSDictionary<NSString *, id> *parameters;
```

Additional error parameters.

Parameters are represented as key-value pairs, where the key and value are strings. If the key or value differs from the string type, AppMetrica calls the `description` method automatically.

The maximum number of parameters is 50. The maximum allowed parameter size is 100 characters for the key and 2000 characters for the value. If the value exceeds the limit, AppMetrica truncates it.

### backtrace {#property_backtrace}

```objectivec translate=no
@optional
@property (readonly, copy, nonatomic, nullable) NSArray<NSNumber *> *backtrace;
```

Custom error backtrace. You can get it using the `NSThread.callStackReturnAddresses` method.

The maximum number of stack frames is 200. If the value exceeds the limit, AppMetrica truncates it.

### underlyingError {#property_underlyingError}

```objectivec translate=no
@optional
@property (readonly, strong, nonatomic, nullable) id<AMAErrorRepresentable> underlyingError;
```

Error instance that matches the `AMAErrorRepresentable` protocol.

The maximum number of nested errors is 10. If the value exceeds the limit, AppMetrica truncates it.
