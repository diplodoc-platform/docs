# ECommerceProduct class

This class contains product information.

## Instance methods {#instance_summary}

#|
|| [init(sku:)](#method_initWithSKU) | Initializes the instance of the `ECommerceProduct` class with the specified item number. ||
|| [init(sku:name:categoryComponents:payload:actualPrice:originalPrice:promoCodes:)](#method_initWithSKU__name__categoryComponents__payload__actualPrice__originalPrice__promoCodes) | Initializes the instance of the `ECommerceProduct` class with all parameters. ||
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

### init(sku:) {#method_initWithSKU}

```swift translate=no
init(sku: String)
```

Initializes the instance of the `ECommerceProduct` class with the specified item number.

**Parameters:**

#|
|| `sku` | Item number. Allowed size: Up to 100 characters. ||
|#

**Returns:**

The `ECommerceProduct` class instance.

### init(sku:name:categoryComponents:payload:actualPrice:originalPrice:promoCodes:) {#method_initWithSKU__name__categoryComponents__payload__actualPrice__originalPrice__promoCodes}

```swift translate=no
init(sku: String, name: String?, categoryComponents: [String]?, payload: [String, String]?, actualPrice: ECommercePrice?, originalPrice: ECommercePrice?, promoCodes: [String]?)
```

Initializes the instance of the `ECommerceProduct` class with all parameters.

**Parameters:**

#|
|| `sku` | Item number. Allowed size: Up to 100 characters. ||
|| `name` | Name of the product. Allowed size: Up to 1000 characters. ||
|| `categoryComponents` | The path to the product by category. |
|| `payload` | Additional information about the product. ||
|| `actualPrice` | The actual product price, which is the price after applying all discounts and promo codes. ||
|| `originalPrice` | The initial product price. ||
|| `promoCodes` | A list of promo codes that are applied to the product. ||
|#

**Returns:**

The `ECommerceProduct` class instance.

## Property descriptions {#property_detail}

### sku {#property_sku}

`var sku: String { get }`

Item number. Allowed size: Up to 100 characters.

### name {#property_name}

`var name: String? { get }`

Name of the product. Allowed size: Up to 1000 characters.

### categoryComponents {#property_categoryComponents}

`var categoryComponents: [String]? { get }`

The path to the product by category. Acceptable sizes:

- Up to 10 elements.
- The size of a single element is up to 100 characters.

### payload {#property_payload}

`var payload: [String : String]? { get }`

Additional information about the product. Acceptable sizes:

- The total `payload` size: Up to 20 KB.
- The `key` size: Up to 100 characters.
- The `value` size: Up to 1000 characters.

### actualPrice {#property_actualPrice}

`var actualPrice: ECommercePrice? { get }`

The actual product price, which is the price after applying all discounts and promo codes.

### originalPrice {#property_originalPrice}

`var originalPrice: ECommercePrice? { get }`

The initial product price.

### promoCodes {#property_promoCodes}

`var promoCodes: [String]? { get }`

A list of promo codes that are applied to the product. Acceptable sizes:

- Up to 20 elements.
- The promo code length is up to 100 characters.
