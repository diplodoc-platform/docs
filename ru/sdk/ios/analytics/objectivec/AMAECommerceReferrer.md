# Класс AMAECommerceReferrer

Класс с информацией об источнике перехода. Например, о ссылке на страницу или экране, на котором показана карточка товара.

## Методы экземпляра {#instance_summary}

#|
|| [-initWithType:identifier:screen:](#method_initWithType__identifier__screen) | Инициализирует экземпляр класса `AMAECommerceReferrer` с информацией об источнике перехода. ||
|#

## Свойства {#property_summary}

#|
|| [type](#property_type) | Тип источника перехода — тип объекта, с которого выполняется переход. Например: <q>button</q>, <q>banner</q>, <q>href</q>. Допустимый размер: до 100 символов. ||
|| [identifier](#property_identifier) | Идентификатор источника перехода. Допустимый размер: до 2048 символов. ||
|| [screen](#property_screen) | Экран источника перехода — экран, с которого выполняется переход. ||
|#

## Описание методов {#method_detail}

### -initWithType:identifier:screen: {#method_initWithType__identifier__screen}

```objectivec translate=no
- (instancetype)initWithType:(nullable NSString *)type
                  identifier:(nullable NSString *)identifier
                      screen:(nullable AMAECommerceScreen *)screen
```

Инициализирует экземпляр класса `AMAECommerceReferrer` с информацией об источнике перехода.

**Параметры:**

#|
|| `type` | Тип источника перехода — тип объекта, с которого выполняется переход. Например: <q>button</q>, <q>banner</q>, <q>href</q>. Допустимый размер: до 100 символов. ||
|| `identifier` | Идентификатор источника перехода. Допустимый размер: до 2048 символов. ||
|| `screen` | Экран источника перехода — экран, с которого выполняется переход. ||
|#

**Возвращает:**

Объект класса `AMAECommerceReferrer`.

## Описание свойств {#property_detail}

### type {#property_type}

`(nonatomic, copy, readonly, nullable) NSString *type`

Тип источника перехода — тип объекта, с которого выполняется переход. Например: <q>button</q>, <q>banner</q>, <q>href</q>. Допустимый размер: до 100 символов.

### identifier {#property_identifier}

`(nonatomic, copy, readonly, nullable) NSString *identifier`

Идентификатор источника перехода. Допустимый размер: до 2048 символов.

### screen {#property_screen}

`(nonatomic, strong, readonly, nullable) AMAECommerceScreen *screen`

Экран источника перехода — экран, с которого выполняется переход.
