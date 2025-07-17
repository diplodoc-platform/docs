# Класс AMAECommerceScreen

Класс с информацией об экране.

## Методы экземпляра {#instance_summary}

#|
|| [-initWithName:](#method_initWithName) | Инициализирует экземпляр класса `AMAECommerceScreen` с указанным названием экрана. ||
|| [-initWithCategoryComponents:](#method_initWithCategoryComponents) | Инициализирует экземпляр класса `AMAECommerceScreen` с указанным путем к экрану. ||
|| [-initWithSearchQuery:](#method_initWithSearchQuery) | Инициализирует экземпляр класса `AMAECommerceScreen` с указанным поисковым запросом. ||
|| [-initWithPayload:](#method_initWithPayload) | Инициализирует экземпляр класса `AMAECommerceScreen` с указанной дополнительной информацией. ||
|| [-initWithName:categoryComponents:searchQuery:payload:](#method_initWithName__currency__categoryComponents__searchQuery__payload) | Инициализирует экземпляр класса `AMAECommerceScreen` со всеми параметрами. ||
|#

## Свойства {#property_summary}

#|
|| [name](#property_name) | Название экрана. Допустимые размеры: до 100 символов. ||
|| [categoryComponents](#property_categoryComponents) | Путь к экрану по категориям. ||
|| [searchQuery](#property_searchQuery) | Поисковый запрос. Допустимый размер: до 1000 символов. ||
|| [payload](#property_payload) | Дополнительная информация об экране. ||
|#

## Описание методов {#method_detail}

### -initWithName: {#method_initWithName}

```objectivec translate=no
- (instancetype)initWithName:(NSString *)name
```

Инициализирует экземпляр класса `AMAECommerceScreen` с указанным названием экрана.

**Параметры:**

#|
|| `name` | Название экрана. Допустимые размеры: до 100 символов. ||
|#

**Возвращает:**

Объект класса `AMAECommerceScreen`.

### -initWithCategoryComponents: {#method_initWithCategoryComponents}

```objectivec translate=no
(instancetype)initWithCategoryComponents:(NSArray<NSString *> *)categoryComponents
```

Инициализирует экземпляр класса `AMAECommerceScreen` с указанным путем к экрану.

**Параметры:**

#|
|| `categoryComponents` | Путь к экрану по категориям. Допустимые размеры:

- до 10 элементов;
- размер одного элемента до 100 символов. ||
|#

**Возвращает:**

Объект класса `AMAECommerceScreen`.

### -initWithSearchQuery: {#method_initWithSearchQuery}

```objectivec translate=no
- (instancetype)initWithSearchQuery:(NSString *)searchQuery
```

Инициализирует экземпляр класса `AMAECommerceScreen` с указанным поисковым запросом.

**Параметры:**

#|
|| `searchQuery` | Поисковый запрос. Допустимый размер: до 1000 символов. ||
|#

**Возвращает:**

Объект класса `AMAECommerceScreen`.

### -initWithPayload: {#method_initWithPayload}

```objectivec translate=no
- (instancetype)initWithPayload:(NSDictionary<NSString *, NSString *> *)payload;
```

Инициализирует экземпляр класса `AMAECommerceScreen` с указанной дополнительной информацией.

**Параметры:**

#|
|| `payload` | Дополнительная информация об экране. Допустимые размеры:

- общий размер `payload`: до 20 КБ;
- размер `key`: до 100 символов;
- размер `value`: до 1000 символов. ||
|#

**Возвращает:**

Объект класса `AMAECommerceScreen`.

### ‑initWithName:categoryComponents:searchQuery:payload: {#method_initWithName__currency__categoryComponents__searchQuery__payload}

```objectivec translate=no
- (instancetype)initWithName:(nullable NSString *)name
          categoryComponents:(nullable NSArray<NSString *> *)categoryComponents
                 searchQuery:(nullable NSString *)searchQuery
                     payload:(nullable NSDictionary<NSString *, NSString *> *)payload
```

Инициализирует экземпляр класса `AMAECommerceScreen` со всеми параметрами.

**Параметры:**

#|
|| `name` | Название экрана. Допустимые размеры: до 100 символов. ||
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

Объект класса `AMAECommerceScreen`.

## Описание свойств {#property_detail}

### name {#property_name}

`(nonatomic, copy, readonly, nullable) NSString *name`

Название экрана. Допустимые размеры: до 100 символов.

### categoryComponents {#property_categoryComponents}

`(nonatomic, copy, readonly, nullable) NSArray<NSString *> *categoryComponents`

Путь к экрану по категориям. Допустимые размеры:

- до 10 элементов;
- размер одного элемента до 100 символов.

### searchQuery {#property_searchQuery}

`(nonatomic, copy, readonly, nullable) NSString *searchQuery`

Поисковый запрос. Допустимый размер: до 1000 символов.

### payload {#property_payload}

`(nonatomic, copy, readonly, nullable) NSDictionary<NSString *, NSString *> *payload`

Дополнительная информация об экране. Допустимые размеры:

- общий размер `payload`: до 20 КБ;
- размер `key`: до 100 символов;
- размер `value`: до 1000 символов.
