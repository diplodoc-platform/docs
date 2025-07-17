# Класс AMARevenueInfo

Класс содержит неизменяемую информацию о доходах от покупок в приложении.

Чтобы изменить информацию о доходах, воспользуйтесь классом [AMAMutableRevenueInfo](AMAMutableRevenueInfo.md).

Объект `AMARevenueInfo` должен быть передан на сервер AppMetrica с помощью метода [reportRevenue](AMAAppMetrica.md#method_reportRevenue) класса [AMAAppMetrica](AMAAppMetrica.md).

## Методы экземпляра {#instance_summary}

#|
|| [-initWithPriceDecimal:currency:](#method_initWithPriceDecimal__currency) | Инициализирует экземпляр класса `AMARevenueInfo` для передачи информации о покупках. ||
|| [-initWithPriceDecimal:currency:quantity:productID:transactionID:receiptData:payload:](#method_initWithPriceDecimal__currency__quantity) | Инициализирует экземпляр класса `AMARevenueInfo` для передачи информации о покупках. ||
|#

## Свойства {#property_summary}

#|
|| [currency](#property_currency) | Код валюты покупки в формате [ISO 4217](https://ru.wikipedia.org/wiki/ISO_4217). ||
|| [payload](#property_payload) | Дополнительная информация о покупке. ||
|| [priceDecimal](#property_priceDecimal) | Стоимость, которая задается объектом [NSDecimalNumber](https://developer.apple.com/documentation/foundation/nsdecimalnumber). Может быть отрицательной (например, для возврата). ||
|| [productID](#property_productID) | Идентификатор покупки. Может содержать до 200 символов. ||
|| [quantity](#property_quantity) | Количество покупок (купленных товаров). ||
|| [receiptData](#property_receiptData) | Подробная информация о покупке в приложении из App Store. ||
|| [transactionID](#property_transactionID) | Информация о покупке в приложении из App Store. ||
|#

## Описание методов {#method_detail}

### -initWithPriceDecimal:currency: {#method_initWithPriceDecimal__currency}

```objectivec translate=no
- (instancetype)initWithPriceDecimal:(NSDecimalNumber *)priceDecimal currency:(NSString *)currency
```

Инициализирует экземпляр класса `AMARevenueInfo` для передачи информации о покупках.

**Параметры:**

#|
|| `priceDecimal` | Стоимость, которая задается объектом [NSDecimalNumber](https://developer.apple.com/documentation/foundation/nsdecimalnumber). Может быть отрицательной (например, для возврата). ||
|| `currency` | Код валюты покупки в формате [ISO 4217](https://ru.wikipedia.org/wiki/ISO_4217). Значение должно содержать 3 латинских буквы в верхнем регистре. Пример: `RUB`.

{% note info %}

Если значение не задано в формате ISO 4217 — покупка игнорируется.

{% endnote %}
||
|#

**Возвращает:**

Объект класса `AMARevenueInfo`.

### ‑initWithPriceDecimal:currency:quantity:productID:transactionID:receiptData:payload: {#method_initWithPriceDecimal__currency__quantity}

```objectivec translate=no
- (instancetype)initWithPriceDecimal:(NSDecimalNumber *)priceDecimal
                            currency:(NSString *)currency
                            quantity:(NSUInteger)quantity
                           productID:(NSString *)productID
                       transactionID:(NSString *)transactionID
                         receiptData:(NSData *)receiptData
                             payload:(NSDictionary *)payload
```

Инициализирует экземпляр класса `AMARevenueInfo` для передачи информации о покупках.

**Параметры:**

#|
|| `priceDecimal` | Стоимость, которая задается объектом [NSDecimalNumber](https://developer.apple.com/documentation/foundation/nsdecimalnumber). Может быть отрицательной (например, для возврата). ||
|| `currency` | Код валюты покупки в формате [ISO 4217](https://ru.wikipedia.org/wiki/ISO_4217). Значение должно содержать 3 латинских буквы в верхнем регистре. Пример: `RUB`.

{% note info %}

Если значение не задано в формате ISO 4217 — покупка игнорируется.

{% endnote %} ||
|| `quantity` | Количество покупок (купленных товаров). ||
|| `productID` | Идентификатор покупки. Может содержать до 200 символов. ||
|| `transactionID` | Информация о покупке в приложении из App Store. ||
|| `receiptData` | Подробная информация о покупке в приложении из App Store. ||
|| `payload` | Дополнительная информация о покупке. ||
|#

**Возвращает:**

Объект класса `AMARevenueInfo`.

## Описание свойств {#property_detail}

### currency {#property_currency}

`(nonatomic, copy, readonly) NSString *currency`

Код валюты покупки в формате [ISO 4217](https://ru.wikipedia.org/wiki/ISO_4217).

### payload {#property_payload}

`(nonatomic, copy, readonly) NSDictionary *payload`

Дополнительная информация о покупке.

### priceDecimal {#property_priceDecimal}

`(nonatomic, assign, readonly) NSDecimalNumber *priceDecimal`

Стоимость, которая задается объектом [NSDecimalNumber](https://developer.apple.com/documentation/foundation/nsdecimalnumber). Может быть отрицательной (например, для возврата).

### productID {#property_productID}

`(nonatomic, copy, readonly) NSString *productID`

Идентификатор покупки. Может содержать до 200 символов.

### quantity {#property_quantity}

`(nonatomic, assign, readonly) NSUInteger quantity`

Количество покупок (купленных товаров).

### receiptData {#property_receiptData}

`(nonatomic, copy, readonly) NSData *receiptData`

Подробная информация о покупке в приложении из App Store.

### transactionID {#property_transactionID}

`(nonatomic, copy, reaоdonly) NSString *transactionID`

Информация о покупке в приложении из App Store.
