# Класс AppMetricaError

Простая реализация протокола [ErrorRepresentable](ErrorRepresentable.md).

## Методы экземпляра {#instance_summary}

#|
|| [init(identifier:)](#method_errorWithIdentifier) | Создает объект `AppMetricaError` с заданным идентификатором. ||
|| [init(identifier:message:parameters:)](#method_errorWithIdentifier_message_params) | Создает объект `AppMetricaError` с заданным идентификатором и другими параметрами. ||
|| [init(identifier:message:parameters:backtrace:underlyingError:)](#method_errorWithIdentifier_message_params_backtrace_underlyingError) | Создает объект `AppMetricaError` пользователя с заданным идентификатором и другими параметрами. ||
|#

## Описание методов {#method_detail}

### init(identifier:) {#method_errorWithIdentifier}

```swift translate=no
convenience init(identifier: String)
```

Создает объект `AppMetricaError` с заданным идентификатором.

**Параметры:**

#|
|| `identifier` | Идентификатор ошибки. Используется AppMetrica для группировки ошибок. ||
|#

**Возвращает:**

Объект класса `AppMetricaError`.

### init(identifier:message:parameters:) {#method_errorWithIdentifier_message_params}

```swift translate=no
convenience init(identifier: String, message: String?, parameters: [String : Any]?)
```

Создает объект `AppMetricaError` с заданным идентификатором и другими параметрами.

**Параметры:**

#|
|| `identifier` | Идентификатор ошибки. Используется AppMetrica для группировки ошибок. ||
|| `message` | Произвольное описание ошибки. ||
|| `parameters` | Дополнительные параметры ошибки. ||
|#

**Возвращает:**

Объект класса `AppMetricaError`.

### init(identifier:message:parameters:backtrace:underlyingError:) {#method_errorWithIdentifier_message_params_backtrace_underlyingError}

```swift translate=no
convenience init(identifier: String, message: String?, parameters: [String : Any]?, backtrace: [NSNumber]?, underlyingError: ErrorRepresentable?)
```

Создает объект `AppMetricaError` пользователя с заданным идентификатором и другими параметрами.

**Параметры:**

#|
|| `identifier` | Идентификатор ошибки. Используется AppMetrica для группировки ошибок. ||
|| `message` | Произвольное описание ошибки. ||
|| `parameters` | Дополнительные параметры ошибки. ||
|| `backtrace` | Кастомный бэктрейс ошибки. ||
|| `underlyingError` | Объект ошибки, который соответствует протоколу [ErrorRepresentable](ErrorRepresentable.md). ||
|#

**Возвращает:**

Объект класса `AppMetricaError`.
