# AMAECommercePrice class

This class contains the product price.

## Instance methods {#instance_summary}

#|
|| -[initWithFiat:](#method_initWithFiat) | Initializes the instance of the `AMAECommercePrice` class. ||
|| -[initWithFiat:internalComponents:](#method_initWithFiat__internalComponents) | Initializes the instance of the `AMAECommercePrice` class. ||
|#

## Properties {#property_summary}

#|
|| [fiat](#property_fiat) | The cost in fiat money. The `AMAECommerceAmount` class instance. ||
|| [internalComponents](#property_internalComponents) | The cost of internal components (the amounts in the internal currency). Allowed size: Up to 30 elements. ||
|#

## Method descriptions {#method_detail}

### -initWithFiat: {#method_initWithFiat}

```objectivec translate=no
- (instancetype)initWithFiat:(AMAECommerceAmount *)fiat
```

Initializes the instance of the `AMAECommercePrice` class.

**Parameters:**

#|
|| `fiat` | The cost in fiat money. The `AMAECommerceAmount` class instance. ||
|#

**Returns:**

The `AMAECommercePrice` class instance.

### -initWithFiat:internalComponents: {#method_initWithFiat__internalComponents}

```objectivec translate=no
- (instancetype)initWithFiat:(AMAECommerceAmount *)fiat
          internalComponents:(nullable NSArray<AMAECommerceAmount *> *)internalComponents;
```

Initializes the instance of the `AMAECommercePrice` class.

**Parameters:**

#|
|| `fiat` | The cost in fiat money. The `AMAECommerceAmount` class instance. ||
|| `internalComponents` | The cost of internal components (the amounts in the internal currency). Allowed size: Up to 30 elements. ||
|#

**Returns:**

The `AMAECommercePrice` class instance.

## Property descriptions {#property_detail}

### fiat {#property_fiat}

```objectivec translate=no
(nonatomic, strong, readonly) AMAECommerceAmount *fiat;
```

The cost in fiat money. The `AMAECommerceAmount` class instance.

### internalComponents {#property_internalComponents}

```objectivec translate=no
(nonatomic, copy, readonly, nullable) NSArray<AMAECommerceAmount *> *internalComponents
```

The cost of internal components (the amounts in the internal currency). Allowed size: Up to 30 elements.
