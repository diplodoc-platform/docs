# Класс AMAECommerceCartItem

Класс с информацией о товаре в корзине.

## Методы экземпляра {#instance_summary}

#|
|| [-initWithProduct:quantity:revenue:referrer:](#method_initWithProduct__referrer__quantity__revenue) | Инициализирует экземпляр класса `AMAECommerceCartItem` с информацией о товаре в корзине. ||
|#

## Свойства {#property_summary}

#|
|| [product](#property_product) | Товар. Объект класса `AMAECommerceProduct`. ||
|| [quantity](#property_quantity) | Количество. ||
|| [revenue](#property_revenue) | Общая цена товара в корзине. Она учитывает количество, применяемые скидки и т. д. Объект класса `AMAECommercePrice`. ||
|| [referrer](#property_referrer) | Источник перехода в корзину. Объект класса `AMAECommerceReferrer`. ||
|#

## Описание методов {#method_detail}

### -initWithProduct:referrer:quantity:revenue: {#method_initWithProduct__referrer__quantity__revenue}

```objectivec translate=no
- (instancetype)initWithProduct:(AMAECommerceProduct *)product
                       quantity:(NSDecimalNumber *)quantity
                        revenue:(AMAECommercePrice *)revenue
                       referrer:(nullable AMAECommerceReferrer *)referrer;
```

Инициализирует экземпляр класса `AMAECommerceCartItem` с информацией о товаре в корзине.

**Параметры:**

#|
|| `product` | Товар. Объект класса `AMAECommerceProduct`. ||
|| `quantity` | Количество. ||
|| `revenue` | Общая цена товара в корзине. Она учитывает количество, применяемые скидки и т. д. Объект класса `AMAECommercePrice`. ||
|| `referrer` | Источник перехода в корзину. Объект класса `AMAECommerceReferrer`. ||
|#

**Возвращает:**

Объект класса `AMAECommerceCartItem`.

## Описание свойств {#property_detail}

### product {#property_product}

`(nonatomic, strong, readonly) AMAECommerceProduct *product`

Товар. Объект класса `AMAECommerceProduct`.

### quantity {#property_quantity}

`(nonatomic, strong, readonly) NSDecimalNumber *quantity`

Количество.

### revenue {#property_revenue}

`(nonatomic, strong, readonly) AMAECommercePrice *revenue`

Общая цена товара в корзине. Она учитывает количество, применяемые скидки и т. д. Объект класса `AMAECommercePrice`.

### referrer {#property_referrer}

`(nonatomic, strong, readonly, nullable) AMAECommerceReferrer *referrer`

Источник перехода в корзину. Объект класса `AMAECommerceReferrer`.
