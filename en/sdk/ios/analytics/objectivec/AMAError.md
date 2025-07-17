# AMAError class

A simple implementation of the [AMAErrorRepresentable](AMAErrorRepresentable.md) protocol.

## Instance methods {#instance_summary}

#|
|| +[errorWithIdentifier:](#method_errorWithIdentifier) | Creates the `AMAError` instance with the specified ID. ||
|| +[errorWithIdentifier:message:parameters:](#method_method_errorWithIdentifier_message_params) | Creates the `AMAError` instance with the specified ID and other parameters. ||
|| +[errorWithIdentifier:message:parameters:backtrace:underlyingError:](#method_errorWithIdentifier_message_params_backtrace_underlyingError) | Creates the `AMAError` instance with the specified ID and other parameters. ||
|#

## Method descriptions {#method_detail}

### +errorWithIdentifier: {#method_errorWithIdentifier}

```objectivec translate=no
+ (nonnull instancetype)errorWithIdentifier:(nonnull NSString *)identifier;
```

Creates the `AMAError` instance with the specified ID.

**Parameters:**

#|
|| `identifier` | Error ID. AppMetrica uses it to group errors. ||
|#

**Returns:**

The `AMAError` class instance.

### +errorWithIdentifier:message:parameters: {#method_method_errorWithIdentifier_message_params}

```objectivec translate=no
+ (nonnull instancetype) errorWithIdentifier:(nonnull NSString *)identifier
                                     message:(nullable NSString *)message
                                  parameters:(nullable NSDictionary<NSString *, id> *)parameters;
```

Creates the `AMAError` instance with the specified ID and other parameters.

**Parameters:**

#|
|| `identifier` | Error ID. AppMetrica uses it to group errors. ||
|| `message` | Arbitrary error description. ||
|| `parameters` | Additional error parameters. ||
|#

**Returns:**

The `AMAError` class instance.

### +errorWithIdentifier:message:parameters:backtrace:underlyingError {#method_errorWithIdentifier_message_params_backtrace_underlyingError}

```objectivec translate=no
+ (nonnull instancetype) errorWithIdentifier:(nonnull NSString *)identifier
                                     message:(nullable NSString *)message
                                  parameters:(nullable NSDictionary<SString *, id> *)parameters
                                   backtrace:(nullable NSArray<NSNumber *> *)backtrace
                             underlyingError:(nullable id<AMAErrorRepresentable>)underlyingError;
```

Creates the `AMAError` instance with the specified ID and other parameters.

**Parameters:**

#|
|| `identifier` | Error ID. AppMetrica uses it to group errors. ||
|| `message` | Arbitrary error description. ||
|| `parameters` | Additional error parameters. ||
|| `backtrace` | Custom error backtrace. ||
|| `underlyingError` | Error instance that matches the [AMAErrorRepresentable](AMAErrorRepresentable.md) protocol. ||
|#

**Returns:**

The `AMAError` class instance.
