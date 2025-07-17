# Класс ECommerceAmount

Класс с информацией о стоимости: количестве и единицах измерения.

## Методы экземпляра {#instance_summary}

#|
|| [init(unit:value:)](#method_initWithUnit__value) | Инициализирует экземпляр класса `ECommerceAmount` для передачи информации о покупках. ||
|#

## Свойства {#property_summary}

#|
|| [unit](#property_unit) | Единица измерения. Например: USD, RUB. Допустимое значение: до 20 символов. ||
|| [value](#property_value) | Количество. ||
|#

## Описание методов {#method_detail}

### init(unit:value:) {#method_initWithUnit__value}

```swift translate=no
init(unit: String, value: NSDecimalNumber)
```

Инициализирует экземпляр класса `ECommerceAmount` для передачи информации о покупках.

**Параметры:**

#|
|| `unit` | Единица измерения. Например: USD, RUB. Допустимое значение: до 20 символов. ||
|| `value` | Количество. ||
|#

**Возвращает:**

Объект класса `ECommerceAmount`.

## Описание свойств {#property_detail}

### unit {#property_unit}

`var unit: String { get }`

Единица измерения. Например: USD, RUB. Допустимое значение: до 20 символов.

Используйте формат [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217).

### value {#property_value}

`var value: NSDecimalNumber { get }`

Количество.
