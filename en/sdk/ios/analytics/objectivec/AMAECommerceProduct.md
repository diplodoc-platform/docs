# AMAECommerceProduct class

This class contains product information.

## Instance methods {#instance_summary}

#|
|| [-initWithSKU:](#method_initWithSKU) | Initializes the instance of the `AMAECommerceProduct` class with the specified item number. ||
|| [-initWithSKU:name:categoryComponents:payload:actualPrice:originalPrice:promoCodes:](#method_initWithSKU__name__categoryComponents__payload__actualPrice__originalPrice__promoCodes) | Initializes the instance of the `AMAECommerceProduct` class with all parameters. ||
|#

## Properties {#property_summary}

#|
|| [sku](#property_sku) | Item number. Allowed size: Up to 100 characters. ||
|| [name](#property_name) | Name of the product. Allowed size: Up to 1000 characters. ||
|| [categoryComponents](#property_categoryComponents) | The path to the product by category. |
|| [payload](#property_payload) | Additional information about the product. ||
|| [actualPrice](#property_actualPrice) | The actual product price, which is the price after applying all discounts and promo codes. ||
|| [originalPrice](#property_originalPrice) | The initial product price. ||
|| [promoCodes](#property_promoCodes) | A list of promo codes that are applied to the product. ||
|#

## Method descriptions {#method_detail}

### -initWithSKU: {#method_initWithSKU}

```objectivec translate=no
- (instancetype)initWithSKU:(NSString *)sku
```

Initializes the instance of the `AMAECommerceProduct` class with the specified item number.

**Parameters:**

#|
|| `sku` | Item number. Allowed size: Up to 100 characters. ||
|#

**Returns:**

The `AMAECommerceProduct` class instance.

### ‑initWithSKU:name:categoryComponents:payload:actualPrice:originalPrice:promoCodes: {#method_initWithSKU__name__categoryComponents__payload__actualPrice__originalPrice__promoCodes}

```objectivec translate=no
- (instancetype)initWithSKU:(NSString *)sku
                       name:(nullable NSString *)name
         categoryComponents:(nullable NSArray<NSString *> *)categoryComponents
                    payload:(nullable NSDictionary<NSString *, NSString *> *)payload
                actualPrice:(nullable AMAECommercePrice *)actualPrice
              originalPrice:(nullable AMAECommercePrice *)originalPrice
                 promoCodes:(nullable NSArray<NSString *> *)promoCodes;
```

Initializes the instance of the `AMAECommerceProduct` class with all parameters.

**Parameters:**

#|
|| `sku` | Item number. Allowed size: Up to 100 characters. ||
|| `name` | Name of the product. Allowed size: Up to 1000 characters. ||
|| `categoryComponents` | The path to the product by category. Acceptable sizes:

- Up to 10 elements.
- The size of a single element is up to 100 characters. |
   || `payload` | Additional information about the order. Acceptable sizes:

- The total `payload` size: Up to 20 KB.
- The `key` size: Up to 100 characters.
- The `value` size: Up to 1000 characters. ||
   || `actualPrice` | The actual product price, which is the price after applying all discounts and promo codes. ||
   || `originalPrice` | The initial product price. ||
   || `promoCodes` | A list of promo codes that are applied to the product. Acceptable sizes:

- Up to 20 elements.
- The promo code length is up to 100 characters. ||
   |#

**Returns:**

The `AMAECommerceProduct` class instance.

## Property descriptions {#property_detail}

### sku {#property_sku}

`(nonatomic, copy, readonly) NSString *sku`

Item number. Allowed size: Up to 100 characters.

### name {#property_name}

`(nonatomic, copy, readonly, nullable) NSString *name`

Name of the product. Allowed size: Up to 1000 characters.

### categoryComponents {#property_categoryComponents}

`(nonatomic, copy, readonly, nullable) NSArray<NSString *> *categoryComponents`

The path to the product by category. Acceptable sizes:

- Up to 10 elements.
- The size of a single element is up to 100 characters.

### payload {#property_payload}

`(nonatomic, copy, readonly, nullable) NSDictionary<NSString *, NSString *> *payload`

Additional information about the product. Acceptable sizes:

- The total `payload` size: Up to 20 KB.
- The `key` size: Up to 100 characters.
- The `value` size: Up to 1000 characters.

### actualPrice {#property_actualPrice}

`(nonatomic, strong, readonly, nullable) AMAECommercePrice *actualPrice`

The actual product price, which is the price after applying all discounts and promo codes.

### originalPrice {#property_originalPrice}

`(nonatomic, strong, readonly, nullable) AMAECommercePrice *originalPrice`

The initial product price.

### promoCodes {#property_promoCodes}

`(nonatomic, copy, readonly, nullable) NSArray<NSString *> *promoCodes`

A list of promo codes that are applied to the product. Acceptable sizes:

- Up to 20 elements.
- The promo code length is up to 100 characters.
