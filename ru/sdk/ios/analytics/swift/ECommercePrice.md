# Класс ECommercePrice

Класс с информацией о цене товара.

## Методы экземпляра {#instance_summary}

#|
|| [init(fiat:)](#method_initWithFiat) | Инициализирует экземпляр класса `ECommercePrice`. ||
|| [init(fiat:internalComponents:)](#method_initWithFiat__internalComponents) | Инициализирует экземпляр класса `ECommercePrice`. ||
|#

## Свойства {#property_summary}

#|
|| [fiat](#property_fiat) | Стоимость в фиатных деньгах. Объект класса `ECommerceAmount`. ||
|| [internalComponents](#property_internalComponents) | Стоимость внутренних компонентов — суммы во внутренней валюте. Допустимый размер: до 30 элементов. ||
|#

## Описание методов {#method_detail}

### init(fiat:) {#method_initWithFiat}

```swift translate=no
init(fiat: ECommerceAmount)
```

Инициализирует экземпляр класса `ECommercePrice`.

**Параметры:**

#|
|| `fiat` | Стоимость в фиатных деньгах. Объект класса `ECommerceAmount`. ||
|#

**Возвращает:**

Объект класса `ECommercePrice`.

### init(fiat:internalComponents:) {#method_initWithFiat__internalComponents}

```swift translate=no
init(fiat: ECommerceAmount, internalComponents: [ECommerceAmount]?)
```

Инициализирует экземпляр класса `ECommercePrice`.

**Параметры:**

#|
|| `fiat` | Стоимость в фиатных деньгах. Объект класса `ECommerceAmount`. ||
|| `internalComponents` | Стоимость внутренних компонентов — суммы во внутренней валюте. Допустимый размер: до 30 элементов. ||
|#

**Возвращает:**

Объект класса `ECommercePrice`.

## Описание свойств {#property_detail}

### fiat {#property_fiat}

`var fiat: ECommerceAmount { get }`

Стоимость в фиатных деньгах. Объект класса `ECommerceAmount`.

### internalComponents {#property_internalComponents}

`var internalComponents: [ECommerceAmount]? { get }`

Стоимость внутренних компонентов — суммы во внутренней валюте. Допустимый размер: до 30 элементов.
