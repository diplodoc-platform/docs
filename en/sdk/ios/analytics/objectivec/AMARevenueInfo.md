# AMARevenueInfo class

The class contains immutable information about the revenue from in-app purchases.

Use the [AMAMutableRevenueInfo](AMAMutableRevenueInfo.md) class to change information about revenue.

The instance of the `AMARevenueInfo` class should be sent to the AppMetrica server using the [reportRevenue](AMAAppMetrica.md#method_reportRevenue) method of the [AMAAppMetrica](AMAAppMetrica.md) class.

## Instance methods {#instance_summary}

#|
|| [-initWithPriceDecimal:currency:](#method_initWithPriceDecimal__currency) | Initializes the instance of the `AMARevenueInfo` class for sending information about purchases. ||
|| [-initWithPriceDecimal:currency:quantity:productID:transactionID:receiptData:payload:](#method_initWithPriceDecimal__currency__quantity) | Initializes the instance of the `AMARevenueInfo` class for sending information about purchases. ||
|#

## Properties {#property_summary}

#|
|| [currency](#property_currency) | Currency code of the purchase in [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) format. ||
|| [payload](#property_payload) | Additional information to be passed about the purchase. ||
|| [priceDecimal](#property_priceDecimal) | The price that is set using the [NSDecimalNumber](https://developer.apple.com/documentation/foundation/nsdecimalnumber) instance. It can be negative, e.g. for refunds. ||
|| [productID](#property_productID) | ID of the product purchased. The value can contain up to 200 characters. ||
|| [quantity](#property_quantity) | Quantity of products purchased. ||
|| [receiptData](#property_receiptData) | Details about the in-app purchase order from App Store. ||
|| [transactionID](#property_transactionID) | Details about the in-app purchase order from App Store. ||
|#

## Method descriptions {#method_detail}

### -initWithPriceDecimal:currency: {#method_initWithPriceDecimal__currency}

```objectivec translate=no
- (instancetype)initWithPriceDecimal:(NSDecimalNumber *)priceDecimal currency:(NSString *)currency
```

Initializes the instance of the `AMARevenueInfo` class for sending information about purchases.

**Parameters:**

#|
|| `priceDecimal` | The price that is set using the [NSDecimalNumber](https://developer.apple.com/documentation/foundation/nsdecimalnumber) instance. It can be negative, e.g. for refunds. ||
|| `currency` | Currency code of the purchase in [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) format. The value should contain 3 Latin letters in uppercase. Example: `RUB`.

{% note info %}

If the value is not in the ISO 4217 format, the purchase is ignored.

{% endnote %}
||
|#

**Returns:**

The `AMARevenueInfo` class instance.

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

Initializes the instance of the `AMARevenueInfo` class for sending information about purchases.

**Parameters:**

#|
|| `priceDecimal` | The price that is set using the [NSDecimalNumber](https://developer.apple.com/documentation/foundation/nsdecimalnumber) instance. It can be negative, e.g. for refunds. ||
|| `currency` | Currency code of the purchase in [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) format. The value should contain 3 Latin letters in uppercase. Example: `RUB`.

{% note info %}

If the value is not in the ISO 4217 format, the purchase is ignored.

{% endnote %} ||
|| `quantity` | Quantity of products purchased. ||
|| `productID` | ID of the product purchased. The value can contain up to 200 characters. ||
|| `transactionID` | Details about the in-app purchase order from App Store. ||
|| `receiptData` | Details about the in-app purchase order from App Store. ||
|| `payload` | Additional information to be passed about the purchase. ||
|#

**Returns:**

The `AMARevenueInfo` class instance.

## Property descriptions {#property_detail}

### currency {#property_currency}

`(nonatomic, copy, readonly) NSString *currency`

Currency code of the purchase in [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) format.

### payload {#property_payload}

`(nonatomic, copy, readonly) NSDictionary *payload`

Additional information to be passed about the purchase.

### priceDecimal {#property_priceDecimal}

`(nonatomic, assign, readonly) NSDecimalNumber *priceDecimal`

The price that is set using the [NSDecimalNumber](https://developer.apple.com/documentation/foundation/nsdecimalnumber) instance. It can be negative, e.g. for refunds.

### productID {#property_productID}

`(nonatomic, copy, readonly) NSString *productID`

ID of the product purchased. The value can contain up to 200 characters.

### quantity {#property_quantity}

`(nonatomic, assign, readonly) NSUInteger quantity`

Quantity of products purchased.

### receiptData {#property_receiptData}

`(nonatomic, copy, readonly) NSData *receiptData`

Details about the in-app purchase order from App Store.

### transactionID {#property_transactionID}

`(nonatomic, copy, reaоdonly) NSString *transactionID`

Details about the in-app purchase order from App Store.
