# Класс AMAECommerceProduct

Класс с информацией о товаре.

## Методы экземпляра {#instance_summary}

#|
|| [-initWithSKU:](#method_initWithSKU) | Инициализирует экземпляр класса `AMAECommerceProduct` с указанным артикулом товара. ||
|| [-initWithSKU:name:categoryComponents:payload:actualPrice:originalPrice:promoCodes:](#method_initWithSKU__name__categoryComponents__payload__actualPrice__originalPrice__promoCodes) | Инициализирует экземпляр класса `AMAECommerceProduct` со всеми параметрами. ||
|#

## Свойства {#property_summary}

#|
|| [sku](#property_sku) | Артикул товара. Допустимый размер: до 100 символов. ||
|| [name](#property_name) | Название товара. Допустимый размер: до 1000 символов. ||
|| [categoryComponents](#property_categoryComponents) | Путь к товару по категориям. ||
|| [payload](#property_payload) | Дополнительная информация о товаре. ||
|| [actualPrice](#property_actualPrice) | Фактическая цена товара — цена после применения всех скидок и промокодов. ||
|| [originalPrice](#property_originalPrice) | Первоначальная цена товара. ||
|| [promoCodes](#property_promoCodes) | Список промокодов, которые применяются к товару. ||
|#

## Описание методов {#method_detail}

### -initWithSKU: {#method_initWithSKU}

```objectivec translate=no
- (instancetype)initWithSKU:(NSString *)sku
```

Инициализирует экземпляр класса `AMAECommerceProduct` с указанным артикулом товара.

**Параметры:**

#|
|| `sku` | Артикул товара. Допустимый размер: до 100 символов. ||
|#

**Возвращает:**

Объект класса `AMAECommerceProduct`.

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

Инициализирует экземпляр класса `AMAECommerceProduct` со всеми параметрами.

**Параметры:**

#|
|| `sku` | Артикул товара. Допустимый размер: до 100 символов. ||
|| `name` | Название товара. Допустимый размер: до 1000 символов. ||
|| `categoryComponents` | Путь к товару по категориям. Допустимые размеры:

- до 10 элементов;
- размер одного элемента до 100 символов. ||
|| `payload` | Дополнительная информация о товаре. Допустимые размеры:

- общий размер `payload`: до 20 КБ;
- размер `key`: до 100 символов;
- размер `value`: до 1000 символов. ||
|| `actualPrice` | Фактическая цена товара — цена после применения всех скидок и промокодов. ||
|| `originalPrice` | Первоначальная цена товара. ||
|| `promoCodes` | Список промокодов, которые применяются к товару. Допустимые размеры:

- до 20 элементов;
- длина промокода до 100 символов. ||
|#

**Возвращает:**

Объект класса `AMAECommerceProduct`.

## Описание свойств {#property_detail}

### sku {#property_sku}

`(nonatomic, copy, readonly) NSString *sku`

Артикул товара. Допустимый размер: до 100 символов.

### name {#property_name}

`(nonatomic, copy, readonly, nullable) NSString *name`

Название товара. Допустимый размер: до 1000 символов.

### categoryComponents {#property_categoryComponents}

`(nonatomic, copy, readonly, nullable) NSArray<NSString *> *categoryComponents`

Путь к товару по категориям. Допустимые размеры:

- до 10 элементов;
- размер одного элемента до 100 символов.

### payload {#property_payload}

`(nonatomic, copy, readonly, nullable) NSDictionary<NSString *, NSString *> *payload`

Дополнительная информация о товаре. Допустимые размеры:

- общий размер `payload`: до 20 КБ;
- размер `key`: до 100 символов;
- размер `value`: до 1000 символов.

### actualPrice {#property_actualPrice}

`(nonatomic, strong, readonly, nullable) AMAECommercePrice *actualPrice`

Фактическая цена товара — цена после применения всех скидок и промокодов.

### originalPrice {#property_originalPrice}

`(nonatomic, strong, readonly, nullable) AMAECommercePrice *originalPrice`

Первоначальная цена товара.

### promoCodes {#property_promoCodes}

`(nonatomic, copy, readonly, nullable) NSArray<NSString *> *promoCodes`

Список промокодов, которые применяются к товару. Допустимые размеры:

- до 20 элементов;
- длина промокода до 100 символов.
