# RevenueInfo class

The class contains immutable information about the revenue from in-app purchases.

Use the [MutableRevenueInfo](MutableRevenueInfo.md) class to change information about revenue.

The instance of the `RevenueInfo` class should be sent to the AppMetrica server using the [reportRevenue](AppMetrica.md#reportrevenue_onfailure-method_reportrevenue) method of the [AppMetrica](AppMetrica.md) class.

## Instance methods {#instance_summary}

#|
|| [init(priceDecimal:currency:)](#method_initWithPriceDecimal__currency) | Initializes the instance of the `RevenueInfo` class for sending information about purchases. ||
|| [init(priceDecimal:currency:quantity:productID:transactionID:receiptData:payload:)](#method_initWithPriceDecimal__currency__quantity) | Initializes the instance of the `RevenueInfo` class for sending information about purchases. ||
|#

## Properties {#property_summary}

#|
|| [currency](#property_currency) | Currency code of the purchase in [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) format. ||
|| [payload](#property_payload) | Additional information to be passed about the purchase. ||
|| [price](#property_price) | Price. It can be negative, e.g. for refunds. ||
|| [priceDecimal](#property_priceDecimal) | The price that is set using the [NSDecimalNumber](https://developer.apple.com/documentation/foundation/nsdecimalnumber) object. It can be negative, e.g. for refunds. ||
|| [productID](#property_productID) | ID of the product purchased. The value can contain up to 200 characters. ||
|| [quantity](#property_quantity) | Quantity of products purchased. ||
|| [receiptData](#property_receiptData) | Details about the in-app purchase order from App Store. ||
|| [transactionID](#property_transactionID) | Details about the in-app purchase order from App Store. ||
|#

## Method descriptions {#method_detail}

### init(priceDecimal:currency:) {#method_initWithPriceDecimal__currency}

```swift translate=no
init(priceDecimal: NSDecimalNumber, currency: String)
```

Initializes the instance of the `RevenueInfo` class for sending information about purchases.

**Parameters:**

#|
|| `priceDecimal` | The price that is set using the [NSDecimalNumber](https://developer.apple.com/documentation/foundation/nsdecimalnumber) instance. It can be negative, e.g. for refunds. ||
|| `currency` | Currency code of the purchase in [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) format.

The value should contain 3 Latin letters in uppercase. Example: `RUB`.

{% note info %}

If the value is not in the ISO 4217 format, the purchase is ignored.

{% endnote %} ||
|#

**Returns:**

The `RevenueInfo` class instance.

### init(priceDecimal:currency:quantity:productID:transactionID:receiptData:payload:) {#method_initWithPriceDecimal__currency__quantity}

```swift translate=no
init(priceDecimal: NSDecimalNumber, currency: String, quantity: UInt, productID: String?, transactionID: String?, receiptData: Data?, payload: [AnyHashable : Any]?)
```

Initializes the instance of the `RevenueInfo` class for sending information about purchases.

**Parameters:**

#|
|| `priceDecimal` | The price that is set using the [NSDecimalNumber](https://developer.apple.com/documentation/foundation/nsdecimalnumber) instance. It can be negative, e.g. for refunds. ||
|| `currency` | Currency code of the purchase in [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) format. The value should contain 3 Latin letters in uppercase. Example: `RUB`.

{% note info %}

If the value is not in ISO 4217 format, the purchase is ignored.

{% endnote %}
||
|| `quantity` | Quantity of products purchased. ||
|| `productID` | ID of the product purchased. The value can contain up to 200 characters. ||
|| `transactionID` | Details about the in-app purchase order from App Store. ||
|| `receiptData` | Details about the in-app purchase order from App Store. ||
|| `payload` | Additional information to be passed about the purchase. For instance, it can be used for categorizing your products.

You must pass the `AnyHashable` object that can be converted to a valid JSON. The maximum size of the value is 30 KB. ||
|#

**Returns:**

The `RevenueInfo` class instance.

## Property descriptions {#property_detail}

### currency {#property_currency}

`var currency: String { get }`

Currency code of the purchase in [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) format. The value should contain 3 Latin letters in uppercase. Example: `RUB`.

{% note info %}

If the value is not in the ISO 4217 format, the purchase is ignored.

{% endnote %}

### payload {#property_payload}

`var payload: [AnyHashable : Any]? { get }`

Additional information to be passed about the purchase. For instance, it can be used for categorizing your products.

You must pass the `AnyHashable` object that can be converted to a valid JSON. The maximum size of the value is 30 KB.

### price {#property_price}

### priceDecimal {#property_priceDecimal}

`var priceDecimal: NSDecimalNumber? { get }`

The price that is set using the [NSDecimalNumber](https://developer.apple.com/documentation/foundation/nsdecimalnumber) instance. It can be negative, e.g. for refunds.

### productID {#property_productID}

`var productID: String? { get }`

ID of the product purchased. The value can contain up to 200 characters.

### quantity {#property_quantity}

`var quantity: UInt { get }`

Quantity of products purchased.

### receiptData {#property_receiptData}

`var receiptData: Data? { get }`

Details about the in-app purchase order from App Store.

### transactionID {#property_transactionID}

`var transactionID: String? { get }`

Details about the in-app purchase order from App Store.
