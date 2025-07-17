# AMAECommerceCartItem class

This class contains information about items added to the cart.

## Instance methods {#instance_summary}

#|
|| [-initWithProduct:quantity:revenue:referrer:](#method_initWithProduct__referrer__quantity__revenue) | Initializes the instance of the `AMAECommerceCartItem` class with information about items added to the cart. ||
|#

## Properties {#property_summary}

#|
|| [product](#property_product) | Product. The `AMAECommerceProduct` class instance. ||
|| [quantity](#property_quantity) | Quantity. ||
|| [revenue](#property_revenue) | The total price of the product in the cart. This price factors in the quantity, discounts to be applied, and so on. The `AMAECommercePrice` class instance. ||
|| [referrer](#property_referrer) | The source of traffic to the cart. The `AMAECommerceReferrer` class instance. ||
|#

## Method descriptions {#method_detail}

### -initWithProduct:referrer:quantity:revenue: {#method_initWithProduct__referrer__quantity__revenue}

```objectivec translate=no
- (instancetype)initWithProduct:(AMAECommerceProduct *)product
                       quantity:(NSDecimalNumber *)quantity
                        revenue:(AMAECommercePrice *)revenue
                       referrer:(nullable AMAECommerceReferrer *)referrer;
```

Initializes the instance of the `AMAECommerceCartItem` class with information about items added to the cart.

**Parameters:**

#|
|| `product` | Product. The `AMAECommerceProduct` class instance. ||
|| `quantity` | Quantity. ||
|| `revenue` | The total price of the product in the cart. This price factors in the quantity, discounts to be applied, and so on. The `AMAECommercePrice` class instance. ||
|| `referrer` | The source of traffic to the cart. The `AMAECommerceReferrer` class instance. ||
|#

**Returns:**

The `AMAECommerceCartItem` class instance.

## Property descriptions {#property_detail}

### product {#property_product}

`(nonatomic, strong, readonly) AMAECommerceProduct *product`

Product. The `AMAECommerceProduct` class instance.

### quantity {#property_quantity}

`(nonatomic, strong, readonly) NSDecimalNumber *quantity`

Quantity.

### revenue {#property_revenue}

`(nonatomic, strong, readonly) AMAECommercePrice *revenue`

The total price of the product in the cart. This price factors in the quantity, discounts to be applied, and so on. The `AMAECommercePrice` class instance.

### referrer {#property_referrer}

`(nonatomic, strong, readonly, nullable) AMAECommerceReferrer *referrer`

The source of traffic to the cart. The `AMAECommerceReferrer` class instance.
