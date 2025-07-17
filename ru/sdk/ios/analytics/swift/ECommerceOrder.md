# Класс ECommerceOrder

Класс с информацией о заказе.

## Методы экземпляра {#instance_summary}

#|
|| [init(identifier:cartItems:)](#method_initWithIdentifier__cartItems) | Инициализирует экземпляр класса `ECommerceOrder` с информацией о заказе. ||
|| [init(identifier:cartItems:payload:)](#method_initWithIdentifier__cartItems__payload) | Инициализирует экземпляр класса `ECommerceOrder` с информацией о заказе. ||
|#

## Свойства {#property_summary}

#|
|| [identifier](#property_identifier) | Идентификатор заказа. Допустимый размер: до 100 символов. ||
|| [cartItems](#property_cartItems) | Список товаров в корзине. ||
|| [payload](#property_payload) | Дополнительная информация о заказе. ||
|#

## Описание методов {#method_detail}

### init(identifier:cartItems:) {#method_initWithIdentifier__cartItems}

```swift translate=no
init(identifier: String, cartItems: [ECommerceCartItem])
```

Инициализирует экземпляр класса `ECommerceOrder` с информацией о заказе.

**Параметры:**

#|
|| `identifier` | Идентификатор заказа. Допустимый размер: до 100 символов. ||
|| `cartItems` | Список товаров в корзине. ||
|#

**Возвращает:**

Объект класса `ECommerceOrder`.

### init(identifier:cartItems:payload:) {#method_initWithIdentifier__cartItems__payload}

```swift translate=no
init(identifier: String, cartItems: [ECommerceCartItem], payload: [String: String]?)
```

Инициализирует экземпляр класса `ECommerceOrder` с информацией о заказе.

**Параметры:**

#|
|| `identifier` | Идентификатор заказа. Допустимый размер: до 100 символов. ||
|| `cartItems` | Список товаров в корзине. ||
|| `payload` | Дополнительная информация о заказе. ||
|#

**Возвращает:**

Объект класса `ECommerceOrder`.

## Описание свойств {#property_detail}

### identifier {#property_identifier}

`var identifier: String { get }`

Идентификатор заказа. Допустимый размер: до 100 символов.

### cartItems {#property_cartItems}

`var cartItems: [ECommerceCartItem] { get }`

Список товаров в корзине.

### payload {#property_payload}

`var payload: [String: String]? { get }`

Дополнительная информация о заказе. Допустимые размеры:

- общий размер `payload`: до 20 КБ;
- размер `key`: до 100 символов;
- размер `value`: до 1000 символов.
