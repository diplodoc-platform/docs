# ECommercePrice class

This class contains the product price.

## Instance methods {#instance_summary}

#|
|| [init(fiat:)](#method_initWithFiat) | Initializes the instance of the `ECommercePrice` class. ||
|| [init(fiat:internalComponents:)](#method_initWithFiat__internalComponents) | Initializes the instance of the `ECommercePrice` class. ||
|#

## Properties {#property_summary}

#|
|| [fiat](#property_fiat) | The cost in fiat money. The `ECommerceAmount` class instance. ||
|| [internalComponents](#property_internalComponents) | The cost of internal components (the amounts in the internal currency). Allowed size: Up to 30 elements. ||
|#

## Method descriptions {#method_detail}

### init(fiat:) {#method_initWithFiat}

```swift translate=no
init(fiat: ECommerceAmount)
```

Initializes the instance of the `ECommercePrice` class.

**Parameters:**

#|
|| `fiat` | The cost in fiat money. The `ECommerceAmount` class instance. ||
|#

**Returns:**

The `ECommercePrice` class instance.

### init(fiat:internalComponents:) {#method_initWithFiat__internalComponents}

```swift translate=no
init(fiat: ECommerceAmount, internalComponents: [ECommerceAmount]?)
```

Initializes the instance of the `ECommercePrice` class.

**Parameters:**

#|
|| `fiat` | The cost in fiat money. The `ECommerceAmount` class instance. ||
|| `internalComponents` | The cost of internal components (the amounts in the internal currency). Allowed size: Up to 30 elements. ||
|#

**Returns:**

The `ECommercePrice` class instance.

## Property descriptions {#property_detail}

### fiat {#property_fiat}

`var fiat: ECommerceAmount { get }`

The cost in fiat money. The `ECommerceAmount` class instance.

### internalComponents {#property_internalComponents}

`var internalComponents: [ECommerceAmount]? { get }`

The cost of internal components (the amounts in the internal currency). Allowed size: Up to 30 elements.
