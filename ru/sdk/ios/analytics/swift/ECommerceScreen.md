# Класс ECommerceScreen

Класс с информацией об экране.

## Методы экземпляра {#instance_summary}

#|
|| [init(name:)](#method_initWithName) | Инициализирует экземпляр класса `ECommerceScreen` с указанным названием экрана. ||
|| [init(categoryComponents:)](#method_initWithCategoryComponents) | Инициализирует экземпляр класса `ECommerceScreen` с указанным путем к экрану. ||
|| [init(searchQuery:)](#method_initWithSearchQuery) | Инициализирует экземпляр класса `ECommerceScreen` с указанным поисковым запросом. ||
|| [init(payload:)](#method_initWithPayload) | Инициализирует экземпляр класса `ECommerceScreen` с указанной дополнительной информацией. ||
|| [init(name:categoryComponents:searchQuery:payload:)](#method_initWithName__currency__categoryComponents__searchQuery__payload) | Инициализирует экземпляр класса `ECommerceScreen` со всеми параметрами. ||
|#

## Свойства {#property_summary}

#|
|| [name](#property_name) | Название экрана. Допустимый размер: до 100 символов.||
|| [categoryComponents](#property_categoryComponents) | Путь к экрану по категориям. ||
|| [searchQuery](#property_searchQuery) | Поисковый запрос. Допустимый размер: до 1000 символов. ||
|| [payload](#property_payload) | Дополнительная информация об экране. ||
|#

## Описание методов {#method_detail}

### init(name:) {#method_initWithName}

```swift translate=no
init(name: String)
```

Инициализирует экземпляр класса `ECommerceScreen` с указанным названием экрана.

**Параметры:**

#|
|| `name` | Название экрана. Допустимый размер: до 100 символов. ||
|#

**Возвращает:**

Объект класса `ECommerceScreen`.

### init(categoryComponents:) {#method_initWithCategoryComponents}

```swift translate=no
init(categoryComponents: [String])
```

Инициализирует экземпляр класса `ECommerceScreen` с указанным путем к экрану.

**Параметры:**

#|
|| `categoryComponents` | Путь к экрану по категориям. Допустимые размеры:

- до 10 элементов;
- размер одного элемента до 100 символов. ||
|#

**Возвращает:**

Объект класса `ECommerceScreen`.

### init(searchQuery:) {#method_initWithSearchQuery}

```swift translate=no
init(searchQuery: String)
```

Инициализирует экземпляр класса `ECommerceScreen` с указанным поисковым запросом.

**Параметры:**

#|
|| `searchQuery` | Поисковый запрос. Допустимый размер: до 1000 символов. ||
|#

**Возвращает:**

Объект класса `ECommerceScreen`.

### init(payload:) {#method_initWithPayload}

```swift translate=no
init(payload: [String: String])
```

Инициализирует экземпляр класса `ECommerceScreen` с указанной дополнительной информацией.

**Параметры:**

#|
|| `payload` | Дополнительная информация об экране. Допустимые размеры:

- общий размер `payload`: до 20 КБ;
- размер `key`: до 100 символов;
- размер `value`: до 1000 символов. ||
|#

**Возвращает:**

Объект класса `ECommerceScreen`.

### init(name:categoryComponents:searchQuery:payload:) {#method_initWithName__currency__categoryComponents__searchQuery__payload}

```swift translate=no
init(name: String?, categoryComponents: [String]?, searchQuery: String?, payload: [String: String]?)
```

Инициализирует экземпляр класса `ECommerceScreen` со всеми параметрами.

**Параметры:**

#|
|| `name` | Название экрана. Допустимый размер: до 100 символов. ||
|| `categoryComponents` | Путь к экрану по категориям. Допустимые размеры:

- до 10 элементов;
- размер одного элемента до 100 символов. ||
|| `searchQuery` | Поисковый запрос. Допустимый размер: до 1000 символов. ||
|| `payload` | Дополнительная информация об экране. Допустимые размеры:

- общий размер `payload`: до 20 КБ;
- размер `key`: до 100 символов;
- размер `value`: до 1000 символов. ||
|#

**Возвращает:**

Объект класса `ECommerceScreen`.

## Описание свойств {#property_detail}

### name {#property_name}

`var name: String? { get }`

Название экрана. Допустимый размер: до 100 символов.

### categoryComponents {#property_categoryComponents}

`var categoryComponents: [String]? { get }`

Путь к экрану по категориям. Допустимые размеры:

- до 10 элементов;
- размер одного элемента до 100 символов.

### searchQuery {#property_searchQuery}

`var searchQuery: String? { get }`

Поисковый запрос. Допустимый размер: до 1000 символов.

### payload {#property_payload}

`var payload: [String: String]? { get }`

Дополнительная информация об экране. Допустимые размеры:

- общий размер `payload`: до 20 КБ;
- размер `key`: до 100 символов;
- размер `value`: до 1000 символов.
