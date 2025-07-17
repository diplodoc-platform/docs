# ECommerceCartItem class

This class contains information about items added to the cart.

## Instance methods {#instance_summary}

#|
|| [init(product:quantity:revenue:referrer:)](#method_initWithProduct__referrer__quantity__revenue) | Initializes the instance of the `ECommerceCartItem` class with information about items added to the cart. ||
|#

## Properties {#property_summary}

#|
|| [product](#property_product) | Product. The `ECommerceProduct` class instance. ||
|| [quantity](#property_quantity) | Quantity. ||
|| [revenue](#property_revenue) | The total price of the product in the cart. This price factors in the quantity, discounts to be applied, and so on. The `ECommercePrice` class instance. ||
|| [referrer](#property_referrer) | The source of traffic to the cart. The `ECommerceReferrer` class instance. ||
|#

## Method descriptions {#method_detail}

### init(product:quantity:revenue:referrer:) {#method_initWithProduct__referrer__quantity__revenue}

```swift translate=no
init(product: ECommerceProduct, quantity: NSDecimalNumber, revenue: ECommercePrice, referrer: ECommerceReferrer?)
```

Initializes the instance of the `ECommerceCartItem` class with information about items added to the cart.

**Parameters:**

#|
|| `product` | Product. The `ECommerceProduct` class instance. ||
|| `quantity` | Quantity. ||
|| `revenue` | The total price of the product in the cart. This price factors in the quantity, discounts to be applied, and so on. The `ECommercePrice` class instance. ||
|| `referrer` | The source of traffic to the cart. The `ECommerceReferrer` class instance. ||
|#

**Returns:**

The `ECommerceCartItem` class instance.

## Property descriptions {#property_detail}

### product {#property_product}

`var product: ECommerceProduct { get }`

Product. The `ECommerceProduct` class instance.

### quantity {#property_quantity}

`var quantity: NSDecimalNumber { get }`

Quantity.

### revenue {#property_revenue}

`var revenue: ECommercePrice { get }`

The total price of the product in the cart. This price factors in the quantity, discounts to be applied, and so on. The `ECommercePrice` class instance.

### referrer {#property_referrer}

`var referrer: ECommerceReferrer? { get }`

The source of traffic to the cart. The `ECommerceReferrer` class instance.
