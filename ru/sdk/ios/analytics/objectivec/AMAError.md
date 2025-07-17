# Класс AMAError

Простая реализация протокола [AMAErrorRepresentable](AMAErrorRepresentable.md).

## Методы экземпляра {#instance_summary}

#|
|| +[errorWithIdentifier:](#method_errorWithIdentifier) | Создает объект `AMAError` с заданным идентификатором. ||
|| +[errorWithIdentifier:message:parameters:](#method_method_errorWithIdentifier_message_params) | Создает объект `AMAError` с заданным идентификатором и другими параметрами. ||
|| +[errorWithIdentifier:message:parameters:backtrace:underlyingError:](#method_errorWithIdentifier_message_params_backtrace_underlyingError) | Создает объект `AMAError` с заданным идентификатором и другими параметрами. ||
|#

## Описание методов {#method_detail}

### +errorWithIdentifier: {#method_errorWithIdentifier}

```objectivec translate=no
+ (nonnull instancetype)errorWithIdentifier:(nonnull NSString *)identifier;
```

Создает объект `AMAError` с заданным идентификатором.

**Параметры:**

#|
|| `identifier` | Идентификатор ошибки. Используется AppMetrica для группировки ошибок. ||
|#

**Возвращает:**

Объект класса `AMAError`.

### +errorWithIdentifier:message:parameters: {#method_method_errorWithIdentifier_message_params}

```objectivec translate=no
+ (nonnull instancetype) errorWithIdentifier:(nonnull NSString *)identifier
                                     message:(nullable NSString *)message
                                  parameters:(nullable NSDictionary<NSString *, id> *)parameters;
```

Создает объект `AMAError` с заданным идентификатором и другими параметрами.

**Параметры:**

#|
|| `identifier` | Идентификатор ошибки. Используется AppMetrica для группировки ошибок. ||
|| `message` | Произвольное описание ошибки. ||
|| `parameters` | Дополнительные параметры ошибки. ||
|#

**Возвращает:**

Объект класса `AMAError`.

### +errorWithIdentifier:message:parameters:backtrace:underlyingError {#method_errorWithIdentifier_message_params_backtrace_underlyingError}

```objectivec translate=no
+ (nonnull instancetype) errorWithIdentifier:(nonnull NSString *)identifier
                                     message:(nullable NSString *)message
                                  parameters:(nullable NSDictionary<SString *, id> *)parameters
                                   backtrace:(nullable NSArray<NSNumber *> *)backtrace
                             underlyingError:(nullable id<AMAErrorRepresentable>)underlyingError;
```

Создает объект `AMAError` с заданным идентификатором и другими параметрами.

**Параметры:**

#|
|| `identifier` | Идентификатор ошибки. Используется AppMetrica для группировки ошибок. ||
|| `message` | Произвольное описание ошибки. ||
|| `parameters` | Дополнительные параметры ошибки. ||
|| `backtrace` | Кастомный бэктрейс ошибки. ||
|| `underlyingError` | Объект ошибки, который соответствует протоколу [AMAErrorRepresentable](AMAErrorRepresentable.md). ||
|#

**Возвращает:**

Объект класса `AMAError`.
