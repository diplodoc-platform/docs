# Класс AMAECommerceOrder

Класс с информацией о заказе.

## Методы экземпляра {#instance_summary}

#|
|| [-initWithIdentifier:cartItems:](#method_initWithIdentifier__cartItems) | Инициализирует экземпляр класса `AMAECommerceOrder` с информацией о заказе. ||
|| [-initWithIdentifier:cartItems:payload:](#method_initWithIdentifier__cartItems__payload) | Инициализирует экземпляр класса `AMAECommerceOrder` с информацией о заказе. ||
|#

## Свойства {#property_summary}

#|
|| [identifier](#property_identifier) | Идентификатор заказа. Допустимый размер: до 100 символов. ||
|| [cartItems](#property_cartItems) | Список товаров в корзине. ||
|| [payload](#property_payload) | Дополнительная информация о заказе. ||
|#

## Описание методов {#method_detail}

### -initWithIdentifier:cartItems: {#method_initWithIdentifier__cartItems}

```objectivec translate=no
- (instancetype)initWithIdentifier:(NSString *)identifier
                         cartItems:(NSArray<AMAECommerceCartItem *> *)cartItems
```

Инициализирует экземпляр класса `AMAECommerceOrder` с информацией о заказе.

**Параметры:**

#|
|| `identifier` | Идентификатор заказа. Допустимый размер: до 100 символов. ||
|| `cartItems` | Список товаров в корзине. ||
|#

**Возвращает:**

Объект класса `AMAECommerceOrder`.

### -initWithIdentifier:cartItems:payload: {#method_initWithIdentifier__cartItems__payload}

```objectivec translate=no
- (instancetype)initWithIdentifier:(NSString *)identifier
                         cartItems:(NSArray<AMAECommerceCartItem *> *)cartItems
                           payload:(nullable NSDictionary<NSString *, NSString *> *)payload
```

Инициализирует экземпляр класса `AMAECommerceOrder` с информацией о заказе.

**Параметры:**

#|
|| `identifier` | Идентификатор заказа. Допустимый размер: до 100 символов. ||
|| `cartItems` | Список товаров в корзине. ||
|| `payload` | Дополнительная информация о заказе. ||
|#

**Возвращает:**

Объект класса `AMAECommerceOrder`.

## Описание свойств {#property_detail}

### identifier {#property_identifier}

`(nonatomic, copy, readonly) NSString *identifier`

Идентификатор заказа. Допустимый размер: до 100 символов.

### cartItems {#property_cartItems}

`(nonatomic, copy, readonly) NSArray<AMAECommerceCartItem *> *cartItems`

Список товаров в корзине.

### payload {#property_payload}

`(nonatomic, copy, readonly, nullable) nullable NSDictionary<NSString *, NSString *> *payload`

Дополнительная информация о заказе. Допустимые размеры:

- общий размер `payload`: до 20 КБ;
- размер `key`: до 100 символов;
- размер `value`: до 1000 символов.
