# AMAECommerceOrder class

This class contains order information.

## Instance methods {#instance_summary}

#|
|| [-initWithIdentifier:cartItems:](#method_initWithIdentifier__cartItems) | Initializes the instance of the `AMAECommerceOrder` class with order information. ||
|| [-initWithIdentifier:cartItems:payload:](#method_initWithIdentifier__cartItems__payload) | Initializes the instance of the `AMAECommerceOrder` class with order information. ||
|#

## Properties {#property_summary}

#|
|| [identifier](#property_identifier) | Order ID. Allowed size: Up to 100 characters. ||
|| [cartItems](#property_cartItems) | A list of items in the cart. ||
|| [payload](#property_payload) | Additional information about the order. ||
|#

## Method descriptions {#method_detail}

### -initWithIdentifier:cartItems: {#method_initWithIdentifier__cartItems}

```objectivec translate=no
- (instancetype)initWithIdentifier:(NSString *)identifier
                         cartItems:(NSArray<AMAECommerceCartItem *> *)cartItems
```

Initializes the instance of the `AMAECommerceOrder` class with order information.

**Parameters:**

#|
|| `identifier` | Order ID. Allowed size: Up to 100 characters. ||
|| `cartItems` | A list of items in the cart. ||
|#

**Returns:**

The `AMAECommerceOrder` class instance.

### -initWithIdentifier:cartItems:payload: {#method_initWithIdentifier__cartItems__payload}

```objectivec translate=no
- (instancetype)initWithIdentifier:(NSString *)identifier
                         cartItems:(NSArray<AMAECommerceCartItem *> *)cartItems
                           payload:(nullable NSDictionary<NSString *, NSString *> *)payload
```

Initializes the instance of the `AMAECommerceOrder` class with order information.

**Parameters:**

#|
|| `identifier` | Order ID. Allowed size: Up to 100 characters. ||
|| `cartItems` | A list of items in the cart. ||
|| `payload` | Additional information about the order. ||
|#

**Returns:**

The `AMAECommerceOrder` class instance.

## Property descriptions {#property_detail}

### identifier {#property_identifier}

`(nonatomic, copy, readonly) NSString *identifier`

Order ID. Allowed size: Up to 100 characters.

### cartItems {#property_cartItems}

`(nonatomic, copy, readonly) NSArray<AMAECommerceCartItem *> *cartItems`

A list of items in the cart.

### payload {#property_payload}

`(nonatomic, copy, readonly, nullable) nullable NSDictionary<NSString *, NSString *> *payload`

Additional information about the order. Acceptable sizes:

- The total `payload` size: Up to 20 KB.
- The `key` size: Up to 100 characters.
- The `value` size: Up to 1000 characters.
