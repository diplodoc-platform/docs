# Класс ECommerceCartItem

Класс с информацией о товаре в корзине.

## Методы экземпляра {#instance_summary}

#|
|| [init(product:quantity:revenue:referrer:)](#method_initWithProduct__referrer__quantity__revenue) | Инициализирует экземпляр класса `ECommerceCartItem` с информацией о товаре в корзине. ||
|#

## Свойства {#property_summary}

#|
|| [product](#property_product) | Товар. Объект класса `ECommerceProduct`. ||
|| [quantity](#property_quantity) | Количество. ||
|| [revenue](#property_revenue) | Общая цена товара в корзине. Она учитывает количество, применяемые скидки и т. д. Объект класса `ECommercePrice`. ||
|| [referrer](#property_referrer) | Источника перехода в корзину. Объект класса `ECommerceReferrer`. ||
|#

## Описание методов {#method_detail}

### init(product:quantity:revenue:referrer:) {#method_initWithProduct__referrer__quantity__revenue}

```swift translate=no
init(product: ECommerceProduct, quantity: NSDecimalNumber, revenue: ECommercePrice, referrer: ECommerceReferrer?)
```

Инициализирует экземпляр класса `ECommerceCartItem` с информацией о товаре в корзине.

**Параметры:**

#|
|| `product` | Товар. Объект класса `ECommerceProduct`. ||
|| `quantity` | Количество. ||
|| `revenue` | Общая цена товара в корзине. Она учитывает количество, применяемые скидки и т. д. Объект класса `ECommercePrice`. ||
|| `referrer` | Источника перехода в корзину. Объект класса `ECommerceReferrer`. ||
|#

**Возвращает:**

Объект класса `ECommerceCartItem`.

## Описание свойств {#property_detail}

### product {#property_product}

`var product: ECommerceProduct { get }`

Товар. Объект класса `ECommerceProduct`.

### quantity {#property_quantity}

`var quantity: NSDecimalNumber { get }`

Количество.

### revenue {#property_revenue}

`var revenue: ECommercePrice { get }`

Общая цена товара в корзине. Она учитывает количество, применяемые скидки и т. д. Объект класса `ECommercePrice`.

### referrer {#property_referrer}

`var referrer: ECommerceReferrer? { get }`

Источника перехода в корзину. Объект класса `ECommerceReferrer`.
