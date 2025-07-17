# ECommerceScreen class

This class contains screen information.

## Instance methods {#instance_summary}

#|
|| [init(name:)](#method_initWithName) | Initializes the instance of the `ECommerceScreen` class with the specified screen name. ||
|| [init(categoryComponents:)](#method_initWithCategoryComponents) | Initializes the instance of the `ECommerceScreen` class with the specified path to the screen. ||
|| [init(searchQuery:)](#method_initWithSearchQuery) | Initializes the instance of the `ECommerceScreen` class with the specified search query. ||
|| [init(payload:)](#method_initWithPayload) | Initializes the instance of the `ECommerceScreen` class with the specified additional information. ||
|| [init(name:categoryComponents:searchQuery:payload:)](#method_initWithName__currency__categoryComponents__searchQuery__payload) | Initializes the instance of the `ECommerceScreen` class with all parameters. ||
|#

## Properties {#property_summary}

#|
|| [name](#property_name) | Screen name. Allowed size: Up to 100 characters.||
|| [categoryComponents](#property_categoryComponents) | The path to the screen by category. ||
|| [searchQuery](#property_searchQuery) | Search query. Allowed size: Up to 1000 characters. ||
|| [payload](#property_payload) | Additional information about the screen. ||
|#

## Method descriptions {#method_detail}

### init(name:) {#method_initWithName}

```swift translate=no
init(name: String)
```

Initializes the instance of the `ECommerceScreen` class with the specified screen name.

**Parameters:**

#|
|| `name` | Screen name. Allowed size: Up to 100 characters. ||
|#

**Returns:**

The `ECommerceScreen` class instance.

### init(categoryComponents:) {#method_initWithCategoryComponents}

```swift translate=no
init(categoryComponents: [String])
```

Initializes the instance of the `ECommerceScreen` class with the specified path to the screen.

**Parameters:**

#|
|| `categoryComponents` | The path to the screen by category. Acceptable sizes:

- Up to 10 elements.
- The size of a single element is up to 100 characters. ||
   |#

**Returns:**

The `ECommerceScreen` class instance.

### init(searchQuery:) {#method_initWithSearchQuery}

```swift translate=no
init(searchQuery: String)
```

Initializes the instance of the `ECommerceScreen` class with the specified search query.

**Parameters:**

#|
|| `searchQuery` | Search query. Allowed size: Up to 1000 characters. ||
|#

**Returns:**

The `ECommerceScreen` class instance.

### init(payload:) {#method_initWithPayload}

```swift translate=no
init(payload: [String: String])
```

Initializes the instance of the `ECommerceScreen` class with the specified additional information.

**Parameters:**

#|
|| `payload` | Additional information about the screen. Acceptable sizes:

- The total `payload` size: Up to 20 KB.
- The `key` size: Up to 100 characters.
- The `value` size: Up to 1000 characters. ||
   |#

**Returns:**

The `ECommerceScreen` class instance.

### init(name:categoryComponents:searchQuery:payload:) {#method_initWithName__currency__categoryComponents__searchQuery__payload}

```swift translate=no
init(name: String?, categoryComponents: [String]?, searchQuery: String?, payload: [String: String]?)
```

Initializes the instance of the `ECommerceScreen` class with all parameters.

**Parameters:**

#|
|| `name` | Screen name. Allowed size: Up to 100 characters. ||
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

The `ECommerceScreen` class instance.

## Property descriptions {#property_detail}

### name {#property_name}

`var name: String? { get }`

Screen name. Allowed size: Up to 100 characters.

### categoryComponents {#property_categoryComponents}

`var categoryComponents: [String]? { get }`

The path to the screen by category. Acceptable sizes:

- Up to 10 elements.
- The size of a single element is up to 100 characters.

### searchQuery {#property_searchQuery}

`var searchQuery: String? { get }`

Search query. Allowed size: Up to 1000 characters.

### payload {#property_payload}

`var payload: [String: String]? { get }`

Additional information about the screen. Acceptable sizes:

- The total `payload` size: Up to 20 KB.
- The `key` size: Up to 100 characters.
- The `value` size: Up to 1000 characters.
