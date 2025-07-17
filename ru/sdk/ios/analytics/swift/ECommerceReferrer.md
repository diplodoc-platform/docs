# Класс ECommerceReferrer

Класс с информацией об источнике перехода. Например, о ссылке на страницу или экране, на котором показана карточка товара.

## Методы экземпляра {#instance_summary}

#|
|| [init(type:identifier:screen:)](#method_initWithType__identifier__screen) | Инициализирует экземпляр класса `ECommerceReferrer` с информацией об источнике перехода. ||
|#

## Свойства {#property_summary}

#|
|| [type](#property_type) | Тип источника перехода — тип объекта, с которого выполняется переход. Например: <q>button</q>, <q>banner</q>, <q>href</q>. Допустимый размер: до 100 символов. ||
|| [identifier](#property_identifier) | Идентификатор источника перехода. Допустимый размер: до 2048 символов. ||
|| [screen](#property_screen) | Экран источника перехода — экран, с которого выполняется переход. ||
|#

## Описание методов {#method_detail}

### init(type:identifier:screen:) {#method_initWithType__identifier__screen}

```swift translate=no
init(type: String?, identifier: String?, screen: ECommerceScreen?)
```

Инициализирует экземпляр класса `ECommerceReferrer` с информацией об источнике перехода.

**Параметры:**

#|
|| `type` | Тип источника перехода — тип объекта, с которого выполняется переход. Например: <q>button</q>, <q>banner</q>, <q>href</q>. Допустимый размер: до 100 символов. ||
|| `identifier` | Идентификатор источника перехода. Допустимый размер: до 2048 символов. ||
|| `screen` | Экран источника перехода — экран, с которого выполняется переход. ||
|#

**Возвращает:**

Объект класса `ECommerceReferrer`.

## Описание свойств {#property_detail}

### type {#property_type}

`var type: String? { get }`

Тип источника перехода — тип объекта, с которого выполняется переход. Например: <q>button</q>, <q>banner</q>, <q>href</q>. Допустимый размер: до 100 символов.

### identifier {#property_identifier}

`var identifier: String? { get }`

Идентификатор источника перехода. Допустимый размер: до 2048 символов.

### screen {#property_screen}

`var screen: ECommerceScreen? { get }`

Экран источника перехода — экран, с которого выполняется переход.
