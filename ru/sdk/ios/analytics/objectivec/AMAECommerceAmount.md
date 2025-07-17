# Класс AMAECommerceAmount

Класс с информацией о стоимости: количестве и единицах измерения.

## Методы экземпляра {#instance_summary}

#|
|| [-initWithUnit:value:](#method_initWithUnit__value) | Инициализирует экземпляр класса `AMAECommerceAmount` для передачи информации о покупках. ||
|#

## Свойства {#property_summary}

#|
|| [unit](#property_unit) | Единица измерения. Например: USD, RUB. Допустимое значение: до 20 символов. ||
|| [value](#property_value) | Количество. ||
|#

## Описание методов {#method_detail}

### -initWithUnit:value: {#method_initWithUnit__value}

```objectivec translate=no
- (instancetype)initWithUnit:(NSString *)unit value:(NSDecimalNumber *)value
```

Инициализирует экземпляр класса `AMAECommerceAmount` для передачи информации о покупках.

**Параметры:**

#|
|| `unit` |  Единица измерения. Например: USD, RUB. Допустимое значение: до 20 символов. 
{% note info %}

Используйте формат [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217).

{% endnote %} ||
|| `value` | Количество. ||
|#

**Возвращает:**

Объект класса `AMAECommerceAmount`.

## Описание свойств {#property_detail}

### unit {#property_unit}

`(nonatomic, copy, readonly) NSString *unit`

Единица измерения. Например: USD, RUB. Допустимое значение: до 20 символов.

{% note info %}

Используйте формат [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217).

{% endnote %}

### value {#property_value}

`(nonatomic, strong, readonly) NSDecimalNumber *value`

Количество.
