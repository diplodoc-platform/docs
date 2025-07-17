# AttributionSource

Представляет данные об атрибуции из внешних систем.

## Структура {#struct_detail}

#|
|| `AttributionSource` | Источник данных об атрибуции. Соответствует `Hashable`, `Equatable`, `RawRepresentable` и `@unchecked Sendable`. ||
|#

## Инициализаторы {#init_summary}

#|
|| [init(_:rawValue:)](#init_init) | Инициализирует новый экземпляр с указанным `rawValue`. ||
|| [init(rawValue:)](#init_rawValue) | Инициализирует новый экземпляр с указанным `rawValue`. ||
|#

## Свойства {#property_summary}

#|
|| [adjust](#property_adjust) | Данные об атрибуции из Adjust. Возвращает `AttributionSource`. ||
|| [airbridge](#property_airbridge) | Данные об атрибуции из Airbridge. Возвращает `AttributionSource`. ||
|| [appsflyer](#property_appsflyer) | Данные об атрибуции из Appsflyer. Возвращает `AttributionSource`. ||
|| [kochava](#property_kochava) | Данные об атрибуции из Kochava. Возвращает `AttributionSource`. ||
|| [singular](#property_singular) | Данные об атрибуции из Singular. Возвращает `AttributionSource`. ||
|| [tenjin](#property_tenjin) | Данные об атрибуции из Tenjin. Возвращает `AttributionSource`. ||
|#

## Описание инициализаторов {#init_detail}

### init (_:) {#init_init}

```swift translate=no
public init(_ rawValue: String)
```

Инициализирует новый экземпляр с указанным `rawValue`.

**Параметры:**

#|
|| `rawValue` | Исходное значение, которое будет использоваться для инициализации нового экземпляра. ||
|#

### init(rawValue:) {#init_rawValue}

```swift translate=no
public init(rawValue: String)
```

Инициализирует новый экземпляр с указанным `rawValue`.

**Параметры:**

#|
|| `rawValue` | Исходное значение, которое будет использоваться для инициализации нового экземпляра. ||
|#

## Описание свойств {#property_detail}

### adjust {#property_adjust}

```swift translate=no
public static let adjust: AttributionSource
```

Данные об атрибуции из Adjust. Возвращает `AttributionSource`.

### airbridge {#property_airbridge}

```swift translate=no
public static let airbridge: AttributionSource
```

Данные об атрибуции из Airbridge. Возвращает `AttributionSource`.

### appsflyer {#property_appsflyer}

```swift translate=no
public static let appsflyer: AttributionSource
```

Данные об атрибуции из Appsflyer. Возвращает `AttributionSource`.

### kochava {#property_kochava}

```swift translate=no
public static let kochava: AttributionSource
```

Данные об атрибуции из Kochava. Возвращает `AttributionSource`.

### singular {#property_singular}

```swift translate=no
public static let singular: AttributionSource
```

Данные об атрибуции из Singular. Возвращает `AttributionSource`.

### tenjin {#property_tenjin}

```swift translate=no
public static let tenjin: AttributionSource
```

Данные об атрибуции из Tenjin. Возвращает `AttributionSource`.
