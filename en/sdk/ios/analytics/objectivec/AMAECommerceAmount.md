# AMAECommerceAmount class

This class contains cost information, such as quantity and units.

## Instance methods {#instance_summary}

#|
|| [-initWithUnit:value:](#method_initWithUnit__value) | Initializes the instance of the `AMAECommerceAmount` class for sending information about purchases. ||
|#

## Properties {#property_summary}

#|
|| [unit](#property_unit) | The unit. For example: USD or RUB. Acceptable value: Up to 20 characters. ||
|| [value](#property_value) | Quantity. ||
|#

## Method descriptions {#method_detail}

### -initWithUnit:value: {#method_initWithUnit__value}

```objectivec translate=no
- (instancetype)initWithUnit:(NSString *)unit value:(NSDecimalNumber *)value
```

Initializes the instance of the `AMAECommerceAmount` class for sending information about purchases.

**Parameters:**

#|
|| `unit` |  The unit. For example: USD or RUB. Acceptable value: Up to 20 characters.
{% note info %}

Use [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) format.

{% endnote %} ||
|| `value` | Quantity. ||
|#

**Returns:**

The `AMAECommerceAmount` class instance.

## Property descriptions {#property_detail}

### unit {#property_unit}

`(nonatomic, copy, readonly) NSString *unit`

The unit. For example: USD or RUB. Acceptable value: Up to 20 characters.

{% note info %}

Use [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) format.

{% endnote %}

### value {#property_value}

`(nonatomic, strong, readonly) NSDecimalNumber *value`

Quantity.
