# ECommerceOrder class

This class contains order information.

## Instance methods {#instance_summary}

#|
|| [init(identifier:cartItems:)](#method_initWithIdentifier__cartItems) | Initializes the instance of the `ECommerceOrder` class with order information. ||
|| [init(identifier:cartItems:payload:)](#method_initWithIdentifier__cartItems__payload) | Initializes the instance of the `ECommerceOrder` class with order information. ||
|#

## Properties {#property_summary}

#|
|| [identifier](#property_identifier) | Order ID. Allowed size: Up to 100 characters. ||
|| [cartItems](#property_cartItems) | A list of items in the cart. ||
|| [payload](#property_payload) | Additional information about the order. ||
|#

## Method descriptions {#method_detail}

### init(identifier:cartItems:) {#method_initWithIdentifier__cartItems}

```swift translate=no
init(identifier: String, cartItems: [ECommerceCartItem])
```

Initializes the instance of the `ECommerceOrder` class with order information.

**Parameters:**

#|
|| `identifier` | Order ID. Allowed size: Up to 100 characters. ||
|| `cartItems` | A list of items in the cart. ||
|#

**Returns:**

The `ECommerceOrder` class instance.

### init(identifier:cartItems:payload:) {#method_initWithIdentifier__cartItems__payload}

```swift translate=no
init(identifier: String, cartItems: [ECommerceCartItem], payload: [String: String]?)
```

Initializes the instance of the `ECommerceOrder` class with order information.

**Parameters:**

#|
|| `identifier` | Order ID. Allowed size: Up to 100 characters. ||
|| `cartItems` | A list of items in the cart. ||
|| `payload` | Additional information about the order. ||
|#

**Returns:**

The `ECommerceOrder` class instance.

## Property descriptions {#property_detail}

### identifier {#property_identifier}

`var identifier: String { get }`

Order ID. Allowed size: Up to 100 characters.

### cartItems {#property_cartItems}

`var cartItems: [ECommerceCartItem] { get }`

A list of items in the cart.

### payload {#property_payload}

`var payload: [String: String]? { get }`

Additional information about the order. Acceptable sizes:

- The total `payload` size: Up to 20 KB.
- The `key` size: Up to 100 characters.
- The `value` size: Up to 1000 characters.
