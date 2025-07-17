# Класс AMAECommercePrice

Класс с информацией о цене товара.

## Методы экземпляра {#instance_summary}

#|
|| -[initWithFiat:](#method_initWithFiat) | Инициализирует экземпляр класса `AMAECommercePrice`. ||
|| -[initWithFiat:internalComponents:](#method_initWithFiat__internalComponents) | Инициализирует экземпляр класса `AMAECommercePrice`. ||
|#

## Свойства {#property_summary}

#|
|| [fiat](#property_fiat) | Стоимость в фиатных деньгах. Объект класса `AMAECommerceAmount`. ||
|| [internalComponents](#property_internalComponents) | Стоимость внутренних компонентов — суммы во внутренней валюте. Допустимый размер: до 30 элементов. ||
|#

## Описание методов {#method_detail}

### -initWithFiat: {#method_initWithFiat}

```objectivec translate=no
- (instancetype)initWithFiat:(AMAECommerceAmount *)fiat
```

Инициализирует экземпляр класса `AMAECommercePrice`.

**Параметры:**

#|
|| `fiat` | Стоимость в фиатных деньгах. Объект класса `AMAECommerceAmount`. ||
|#

**Возвращает:**

Объект класса `AMAECommercePrice`.

### -initWithFiat:internalComponents: {#method_initWithFiat__internalComponents}

```objectivec translate=no
- (instancetype)initWithFiat:(AMAECommerceAmount *)fiat
          internalComponents:(nullable NSArray<AMAECommerceAmount *> *)internalComponents;
```

Инициализирует экземпляр класса `AMAECommercePrice`.

**Параметры:**

#|
|| `fiat` | Стоимость в фиатных деньгах. Объект класса `AMAECommerceAmount`. ||
|| `internalComponents` | Стоимость внутренних компонентов — суммы во внутренней валюте. Допустимый размер: до 30 элементов. ||
|#

**Возвращает:**

Объект класса `AMAECommercePrice`.

## Описание свойств {#property_detail}

### fiat {#property_fiat}

```objectivec translate=no
(nonatomic, strong, readonly) AMAECommerceAmount *fiat;
```

Стоимость в фиатных деньгах. Объект класса `AMAECommerceAmount`.

### internalComponents {#property_internalComponents}

```objectivec translate=no
(nonatomic, copy, readonly, nullable) NSArray<AMAECommerceAmount *> *internalComponents
```

Стоимость внутренних компонентов — суммы во внутренней валюте. Допустимый размер: до 30 элементов.
