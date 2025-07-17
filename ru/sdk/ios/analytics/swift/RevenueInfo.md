# Класс RevenueInfo

Класс содержит неизменяемую информацию о доходах от покупок в приложении.

Чтобы изменить информацию о доходах, воспользуйтесь классом [MutableRevenueInfo](MutableRevenueInfo.md).

Объект `RevenueInfo` должен быть передан на сервер AppMetrica с помощью метода [reportRevenue](AppMetrica.md#reportrevenue_onfailure-method_reportrevenue) класса [AppMetrica](AppMetrica.md).

## Методы экземпляра {#instance_summary}

#|
|| [init(priceDecimal:currency:)](#method_initWithPriceDecimal__currency) | Инициализирует экземпляр класса `RevenueInfo` для передачи информации о покупках. ||
|| [init(priceDecimal:currency:quantity:productID:transactionID:receiptData:payload:)](#method_initWithPriceDecimal__currency__quantity) | Инициализирует экземпляр класса `RevenueInfo` для передачи информации о покупках. ||
|#

## Свойства {#property_summary}

#|
|| [currency](#property_currency) | Код валюты покупки в формате [ISO 4217](https://ru.wikipedia.org/wiki/ISO_4217). ||
|| [payload](#property_payload) | Дополнительная информация о покупке. ||
|| [price](#property_price) | Стоимость. Может быть отрицательной (например, для возврата). ||
|| [priceDecimal](#property_priceDecimal) | Стоимость, которая задается объектом [NSDecimalNumber](https://developer.apple.com/documentation/foundation/nsdecimalnumber). Может быть отрицательной (например, для возврата). ||
|| [productID](#property_productID) | Идентификатор покупки. Может содержать до 200 символов. ||
|| [quantity](#property_quantity) | Количество покупок (купленных товаров). ||
|| [receiptData](#property_receiptData) | Подробная информация о покупке в приложении из App Store. ||
|| [transactionID](#property_transactionID) | Информация о покупке в приложении из App Store. ||
|#

## Описание методов {#method_detail}

### init(priceDecimal:currency:) {#method_initWithPriceDecimal__currency}

```swift translate=no
init(priceDecimal: NSDecimalNumber, currency: String)
```

Инициализирует экземпляр класса `RevenueInfo` для передачи информации о покупках.

**Параметры:**

#|
|| `priceDecimal` | Стоимость, которая задается объектом [NSDecimalNumber](https://developer.apple.com/documentation/foundation/nsdecimalnumber). Может быть отрицательной (например, для возврата). ||
|| `currency` | Код валюты покупки в формате [ISO 4217](https://ru.wikipedia.org/wiki/ISO_4217).

Значение должно содержать 3 латинских буквы в верхнем регистре. Пример: `RUB`.

{% note info %}

Если значение не задано в формате ISO 4217 — покупка игнорируется.

{% endnote %} ||
|#

**Возвращает:**

Объект класса `RevenueInfo`.

### init(priceDecimal:currency:quantity:productID:transactionID:receiptData:payload:) {#method_initWithPriceDecimal__currency__quantity}

```swift translate=no
init(priceDecimal: NSDecimalNumber, currency: String, quantity: UInt, productID: String?, transactionID: String?, receiptData: Data?, payload: [AnyHashable : Any]?)
```

Инициализирует экземпляр класса `RevenueInfo` для передачи информации о покупках.

**Параметры:**

#|
|| `priceDecimal` | Стоимость, которая задается объектом [NSDecimalNumber](https://developer.apple.com/documentation/foundation/nsdecimalnumber). Может быть отрицательной (например, для возврата). ||
|| `currency` | Код валюты покупки в формате [ISO 4217](https://ru.wikipedia.org/wiki/ISO_4217). Значение должно содержать 3 латинских буквы в верхнем регистре. Пример: `RUB`.

{% note info %}

Если значение не задано в формате ISO 4217 — покупка игнорируется.

{% endnote %}
||
|| `quantity` | Количество покупок (купленных товаров). ||
|| `productID` | Идентификатор покупки. Может содержать до 200 символов. ||
|| `transactionID` | Информация о покупке в приложении из App Store. ||
|| `receiptData` | Подробная информация о покупке в приложении из App Store. ||
|| `payload` | Дополнительная информация о покупке. Например, можно использовать для категоризации ваших продуктов.

Необходимо передать объект `AnyHashable`, который может быть преобразован в валидный JSON. Максимальный размер значения — 30 КБ. ||
|#

**Возвращает:**

Объект класса `RevenueInfo`.

## Описание свойств {#property_detail}

### currency {#property_currency}

`var currency: String { get }`

Код валюты покупки в формате [ISO 4217](https://ru.wikipedia.org/wiki/ISO_4217). Значение должно содержать 3 латинских буквы в верхнем регистре. Пример: `RUB`.

{% note info %}

Если значение не задано в формате ISO 4217 — покупка игнорируется.

{% endnote %}

### payload {#property_payload}

`var payload: [AnyHashable : Any]? { get }`

Дополнительная информация о покупке. Например, можно использовать для категоризации ваших продуктов.

Необходимо передать объект `AnyHashable`, который может быть преобразован в валидный JSON. Максимальный размер значения — 30 КБ.

### price {#property_price}

### priceDecimal {#property_priceDecimal}

`var priceDecimal: NSDecimalNumber? { get }`

Стоимость, которая задается объектом [NSDecimalNumber](https://developer.apple.com/documentation/foundation/nsdecimalnumber). Может быть отрицательной (например, для возврата).

### productID {#property_productID}

`var productID: String? { get }`

Идентификатор покупки. Может содержать до 200 символов.

### quantity {#property_quantity}

`var quantity: UInt { get }`

Количество покупок (купленных товаров).

### receiptData {#property_receiptData}

`var receiptData: Data? { get }`

Подробная информация о покупке в приложении из App Store.

### transactionID {#property_transactionID}

`var transactionID: String? { get }`

Информация о покупке в приложении из App Store.
