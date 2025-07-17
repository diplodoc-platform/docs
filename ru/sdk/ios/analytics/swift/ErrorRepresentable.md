# Протокол ErrorRepresentable

Протокол для ошибок, которые можно отправлять в AppMetrica.

Каждый объект класса, который реализует протокол, должен иметь идентификатор. AppMetrica использует идентификаторы, чтобы группировать ошибки.

Вся отправленная информация об ошибках доступна в отчетах AppMetrica.

Вы можете реализовать этот протокол, чтобы отправлять собственные ошибки. Также вы можете воспользоваться дефолтной реализацией [AppMetricaError](AppMetricaError.md).

## Свойства {#property_summary}

#|
|| [identifier](#property_identifier) | Идентификатор ошибки. Используется AppMetrica для группировки ошибок. ||
|| [message](#property_message) | Произвольное описание ошибки. ||
|| [parameters](#property_parameters) | Дополнительные параметры ошибки. ||
|| [backtrace](#property_backtrace) | Кастомный бэктрейс ошибки. Вы можете получить его с помощью метода `Thread.callStackReturnAddresses`. ||
|| [underlyingError](#property_underlyingError) | Объект ошибки, который соответствует протоколу `ErrorRepresentable`. ||
|#

## Описание свойств {#property_detail}

### identifier {#property_identifier}

```swift translate=no
var identifier: String { get }
```

Идентификатор ошибки. Используется AppMetrica для группировки ошибок.

Максимальная длина значения — 300 символов. Если значение превышает ограничение, AppMetrica обрезает его.

{% note info %}

AppMetrica не использует идентификаторы вложенных ошибок (underlyingError) для группировки.

{% endnote %}

### message {#property_message}

```swift translate=no
optional var message: String? { get }
```

Произвольное описание ошибки.

Максимальная длина значения — 1000 символов. Если значение превышает ограничение, AppMetrica обрезает его.

### parameters {#property_parameters}

```swift translate=no
optional var parameters: [String : Any]? { get }
```

Дополнительные параметры ошибки.

Параметры приводятся к парам ключ-значение, где ключ и значение являются строками. Если ключ или значение отличаются от типа строка, AppMetrica автоматически вызывает метод `description`.

Максимальное количество параметров — 50. Максимальные значения параметров — 100 символов для ключа, 2 000 для значения. Если значение превышает ограничение, AppMetrica обрезает его.

### backtrace {#property_backtrace}

```swift translate=no
optional var backtrace: [NSNumber]? { get }
```

Кастомный бэктрейс ошибки. Вы можете получить его с помощью метода `Thread.callStackReturnAddresses`.

Максимальное количество фреймов стека — 200. Если значение превышает ограничение, AppMetrica обрезает его.

### underlyingError {#property_underlyingError}

```swift translate=no
optional var underlyingError: ErrorRepresentable? { get }
```

Объект ошибки, который соответствует протоколу `ErrorRepresentable`.

Максимальное количество вложенных ошибок — 10. Если значение превышает ограничение, AppMetrica обрезает его.
