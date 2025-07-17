# ECommerceAmount class

This class contains cost information, such as quantity and units.

## Instance methods {#instance_summary}

#|
|| [init(unit:value:)](#method_initWithUnit__value) | Initializes the instance of the `ECommerceAmount` class for sending information about purchases. ||
|#

## Properties {#property_summary}

#|
|| [unit](#property_unit) | The unit. For example: USD or RUB. Acceptable value: Up to 20 characters. ||
|| [value](#property_value) | Quantity. ||
|#

## Method descriptions {#method_detail}

### init(unit:value:) {#method_initWithUnit__value}

```swift translate=no
init(unit: String, value: NSDecimalNumber)
```

Initializes the instance of the `ECommerceAmount` class for sending information about purchases.

**Parameters:**

#|
|| `unit` | The unit. For example: USD or RUB. Acceptable value: Up to 20 characters. ||
|| `value` | Quantity. ||
|#

**Returns:**

The `ECommerceAmount` class instance.

## Property descriptions {#property_detail}

### unit {#property_unit}

`var unit: String { get }`

The unit. For example: USD or RUB. Acceptable value: Up to 20 characters.

Use [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) format.

### value {#property_value}

`var value: NSDecimalNumber { get }`

Quantity.
