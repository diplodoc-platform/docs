# Класс ECommerceProduct

Класс с информацией о товаре.

## Методы экземпляра {#instance_summary}

#|
|| [init(sku:)](#method_initWithSKU) | Инициализирует экземпляр класса `ECommerceProduct` с указанным артикулом товара. ||
|| [init(sku:name:categoryComponents:payload:actualPrice:originalPrice:promoCodes:)](#method_initWithSKU__name__categoryComponents__payload__actualPrice__originalPrice__promoCodes) | Инициализирует экземпляр класса `ECommerceProduct` со всеми параметрами. ||
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

### init(sku:) {#method_initWithSKU}

```swift translate=no
init(sku: String)
```

Инициализирует экземпляр класса `ECommerceProduct` с указанным артикулом товара.

**Параметры:**

#|
|| `sku` | Артикул товара. Допустимый размер: до 100 символов. ||
|#

**Возвращает:**

Объект класса `ECommerceProduct`.

### init(sku:name:categoryComponents:payload:actualPrice:originalPrice:promoCodes:) {#method_initWithSKU__name__categoryComponents__payload__actualPrice__originalPrice__promoCodes}

```swift translate=no
init(sku: String, name: String?, categoryComponents: [String]?, payload: [String, String]?, actualPrice: ECommercePrice?, originalPrice: ECommercePrice?, promoCodes: [String]?)
```

Инициализирует экземпляр класса `ECommerceProduct` со всеми параметрами.

**Параметры:**

#|
|| `sku` | Артикул товара. Допустимый размер: до 100 символов. ||
|| `name` | Название товара. Допустимый размер: до 1000 символов. ||
|| `categoryComponents` | Путь к товару по категориям. ||
|| `payload` | Дополнительная информация о товаре. ||
|| `actualPrice` | Фактическая цена товара — цена после применения всех скидок и промокодов. ||
|| `originalPrice` | Первоначальная цена товара. ||
|| `promoCodes` | Список промокодов, которые применяются к товару. ||
|#

**Возвращает:**

Объект класса `ECommerceProduct`.

## Описание свойств {#property_detail}

### sku {#property_sku}

`var sku: String { get }`

Артикул товара. Допустимый размер: до 100 символов.

### name {#property_name}

`var name: String? { get }`

Название товара. Допустимый размер: до 1000 символов.

### categoryComponents {#property_categoryComponents}

`var categoryComponents: [String]? { get }`

Путь к товару по категориям. Допустимые размеры:

- до 10 элементов;
- размер одного элемента до 100 символов.

### payload {#property_payload}

`var payload: [String : String]? { get }`

Дополнительная информация о товаре. Допустимые размеры:

- общий размер `payload`: до 20 КБ;
- размер `key`: до 100 символов;
- размер `value`: до 1000 символов.

### actualPrice {#property_actualPrice}

`var actualPrice: ECommercePrice? { get }`

Фактическая цена товара — цена после применения всех скидок и промокодов.

### originalPrice {#property_originalPrice}

`var originalPrice: ECommercePrice? { get }`

Первоначальная цена товара.

### promoCodes {#property_promoCodes}

`var promoCodes: [String]? { get }`

Список промокодов, которые применяются к товару. Допустимые размеры:

- до 20 элементов;
- длина промокода до 100 символов.
