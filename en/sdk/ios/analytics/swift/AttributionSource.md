# AttributionSource

Provides attribution data from external systems.

## Structure {#struct_detail}

#|
|| `AttributionSource` | The attribution data source. Matches `Hashable`, `Equatable`, `RawRepresentable`, and `@unchecked Sendable`. ||
|#

## Initializers {#init_summary}

#|
|| [init(_:rawValue:)](#init_init) | Initializes a new instance with a given `rawValue`. ||
|| [init(rawValue:)](#init_rawValue) | Initializes a new instance with a given `rawValue`. ||
|#

## Properties {#property_summary}

#|
|| [adjust](#property_adjust) | Attribution data from Adjust. Returns the `AttributionSource`. ||
|| [airbridge](#property_airbridge) | Attribution data from Airbridge. Returns the `AttributionSource`. ||
|| [appsflyer](#property_appsflyer) | Attribution data from Appsflyer. Returns the `AttributionSource`. ||
|| [kochava](#property_kochava) | Attribution data from Kochava. Returns the `AttributionSource`. ||
|| [singular](#property_singular) | Attribution data from Singular. Returns the `AttributionSource`. ||
|| [tenjin](#property_tenjin) | Attribution data from Tenjin. Returns the `AttributionSource`. ||
|#

## Initializer descriptions {#init_detail}

### init (_:) {#init_init}

```swift translate=no
public init(_ rawValue: String)
```

Initializes a new instance with a given `rawValue`.

**Parameters:**

#|
|| `rawValue` | Raw value to be used for initializing a new instance. ||
|#

### init(rawValue:) {#init_rawValue}

```swift translate=no
public init(rawValue: String)
```

Initializes a new instance with a given `rawValue`.

**Parameters:**

#|
|| `rawValue` | Raw value to be used for initializing a new instance. ||
|#

## Property descriptions {#property_detail}

### adjust {#property_adjust}

```swift translate=no
public static let adjust: AttributionSource
```

Attribution data from Adjust. Returns the `AttributionSource`.

### airbridge {#property_airbridge}

```swift translate=no
public static let airbridge: AttributionSource
```

Attribution data from Airbridge. Returns the `AttributionSource`.

### appsflyer {#property_appsflyer}

```swift translate=no
public static let appsflyer: AttributionSource
```

Attribution data from Appsflyer. Returns the `AttributionSource`.

### kochava {#property_kochava}

```swift translate=no
public static let kochava: AttributionSource
```

Attribution data from Kochava. Returns the `AttributionSource`.

### singular {#property_singular}

```swift translate=no
public static let singular: AttributionSource
```

Attribution data from Singular. Returns the `AttributionSource`.

### tenjin {#property_tenjin}

```swift translate=no
public static let tenjin: AttributionSource
```

Attribution data from Tenjin. Returns the `AttributionSource`.
