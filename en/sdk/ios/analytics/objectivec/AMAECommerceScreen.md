# AMAECommerceScreen class

This class contains screen information.

## Instance methods {#instance_summary}

#|
|| [-initWithName:](#method_initWithName) | Initializes the instance of the `AMAECommerceScreen` class with the specified screen name. ||
|| [-initWithCategoryComponents:](#method_initWithCategoryComponents) | Initializes the instance of the `AMAECommerceScreen` class with the specified path to the screen. ||
|| [-initWithSearchQuery:](#method_initWithSearchQuery) | Initializes the instance of the `AMAECommerceScreen` class with the specified search query. ||
|| [-initWithPayload:](#method_initWithPayload) | Initializes the instance of the `AMAECommerceScreen` class with the specified additional information. ||
|| [-initWithName:categoryComponents:searchQuery:payload:](#method_initWithName__currency__categoryComponents__searchQuery__payload) | Initializes the instance of the `AMAECommerceScreen` class with all parameters. ||
|#

## Properties {#property_summary}

#|
|| [name](#property_name) | Screen name. Acceptable sizes: Up to 100 characters. ||
|| [categoryComponents](#property_categoryComponents) | The path to the screen by category. ||
|| [searchQuery](#property_searchQuery) | Search query. Allowed size: Up to 1000 characters. ||
|| [payload](#property_payload) | Additional information about the screen. ||
|#

## Method descriptions {#method_detail}

### -initWithName: {#method_initWithName}

```objectivec translate=no
- (instancetype)initWithName:(NSString *)name
```

Initializes the instance of the `AMAECommerceScreen` class with the specified screen name.

**Parameters:**

#|
|| `name` | Screen name. Acceptable sizes: Up to 100 characters. ||
|#

**Returns:**

The `AMAECommerceScreen` class instance.

### -initWithCategoryComponents: {#method_initWithCategoryComponents}

```objectivec translate=no
(instancetype)initWithCategoryComponents:(NSArray<NSString *> *)categoryComponents
```

Initializes the instance of the `AMAECommerceScreen` class with the specified path to the screen.

**Parameters:**

#|
|| `categoryComponents` | The path to the screen by category. Acceptable sizes:

- Up to 10 elements.
- The size of a single element is up to 100 characters. ||
   |#

**Returns:**

The `AMAECommerceScreen` class instance.

### -initWithSearchQuery: {#method_initWithSearchQuery}

```objectivec translate=no
- (instancetype)initWithSearchQuery:(NSString *)searchQuery
```

Initializes the instance of the `AMAECommerceScreen` class with the specified search query.

**Parameters:**

#|
|| `searchQuery` | Search query. Allowed size: Up to 1000 characters. ||
|#

**Returns:**

The `AMAECommerceScreen` class instance.

### -initWithPayload: {#method_initWithPayload}

```objectivec translate=no
- (instancetype)initWithPayload:(NSDictionary<NSString *, NSString *> *)payload;
```

Initializes the instance of the `AMAECommerceScreen` class with the specified additional information.

**Parameters:**

#|
|| `payload` | Additional information about the screen. Acceptable sizes:

- The total `payload` size: Up to 20 KB.
- The `key` size: Up to 100 characters.
- The `value` size: Up to 1000 characters. ||
   |#

**Returns:**

The `AMAECommerceScreen` class instance.

### ‑initWithName:categoryComponents:searchQuery:payload: {#method_initWithName__currency__categoryComponents__searchQuery__payload}

```objectivec translate=no
- (instancetype)initWithName:(nullable NSString *)name
          categoryComponents:(nullable NSArray<NSString *> *)categoryComponents
                 searchQuery:(nullable NSString *)searchQuery
                     payload:(nullable NSDictionary<NSString *, NSString *> *)payload
```

Initializes the instance of the `AMAECommerceScreen` class with all parameters.

**Parameters:**

#|
|| `name` | Screen name. Acceptable sizes: Up to 100 characters. ||
|| `categoryComponents` | The path to the screen by category. Acceptable sizes:

- Up to 10 elements.
- The size of a single element is up to 100 characters. ||
   || `searchQuery` | Search query. Allowed size: Up to 1000 characters. ||
   || `payload` | Additional information about the screen. Acceptable sizes:

- The total `payload` size: Up to 20 KB.
- The `key` size: Up to 100 characters.
- The `value` size: Up to 1000 characters. ||
   |#

**Returns:**

The `AMAECommerceScreen` class instance.

## Property descriptions {#property_detail}

### name {#property_name}

`(nonatomic, copy, readonly, nullable) NSString *name`

Screen name. Acceptable sizes: Up to 100 characters.

### categoryComponents {#property_categoryComponents}

`(nonatomic, copy, readonly, nullable) NSArray<NSString *> *categoryComponents`

The path to the screen by category. Acceptable sizes:

- Up to 10 elements.
- The size of a single element is up to 100 characters.

### searchQuery {#property_searchQuery}

`(nonatomic, copy, readonly, nullable) NSString *searchQuery`

Search query. Allowed size: Up to 1000 characters.

### payload {#property_payload}

`(nonatomic, copy, readonly, nullable) NSDictionary<NSString *, NSString *> *payload`

Additional information about the screen. Acceptable sizes:

- The total `payload` size: Up to 20 KB.
- The `key` size: Up to 100 characters.
- The `value` size: Up to 1000 characters.
