# AdRevenueInfo class

The class contains immutable information about advertising revenue.

Use the [MutableAdRevenueInfo](MutableAdRevenueInfo.md) class to change information about revenue.

The instance of the `AdRevenueInfo` class should be passed to the AppMetrica server using the [reportAdRevenue](AppMetrica.md#method_reportAdRevenue) method of the [AppMetrica](AppMetrica.md) class.

## Instance methods {#instance_summary}

#|
|| [init(adRevenue:currency:)](#method_init__adRevenue__currency) | Initializes the instance of the `AdRevenueInfo` class for sending information about advertising revenue. ||
|#

## Properties {#property_summary}

#|
|| [adRevenue](#property_adRevenue) | The amount of money received from advertising revenue. Can't be negative. ||
|| [currency](#property_currency) | The currency in which `adRevenue` is represented. Must be in ISO-4217 format. ||
|| [adType](#property_adType) | Ad type. See possible values in [AdType](AdType.md). ||
|| [adNetwork](#property_adNetwork) | Advertising network. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica. ||
|| [adUnitID](#property_adUnitID) | Ad unit ID. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica. ||
|| [adUnitName](#property_adUnitName) | Ad unit name. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica. ||
|| [adPlacementID](#property_adPlacementID) | Ad placement ID. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica. ||
|| [adPlacementName](#property_adPlacementName) | Ad placement name. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica. ||
|| [precision](#property_precision) | Accuracy. For example, «publisher_defined» or «estimated». The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica. ||
|| [payload](#property_payload) | Accuracy. For example, «publisher_defined» or «estimated». Arbitrary payload: Additional information presented as key-value pairs. The maximum size is 30 KB. If the value exceeds this limit, it will be truncated by AppMetrica. ||
|#

## Method descriptions {#method_detail}

### init(adRevenue:currency:) {#method_init__adRevenue__currency}

```swift translate=no
init(adRevenue: NSDecimalNumber, currency: String)
```

Initializes the instance of the `AdRevenueInfo` class for sending information about advertising revenue.

**Parameters:**

#|
|| `adRevenue` | The amount of money received from advertising revenue. Can't be negative. ||
|| `currency` | The currency in which `adRevenue` is represented. Must be in ISO-4217 format. ||
|#

**Returns:**

The `AdRevenueInfo` class instance.

## Property descriptions {#property_detail}

### adRevenue {#property_adRevenue}

`var adRevenue: NSDecimalNumber { get }`

The amount of money received from advertising revenue. Can't be negative.

### currency {#property_currency}

`var currency: String { get }`

The currency in which `adRevenue` is represented. Must be in ISO-4217 format.

### adType {#property_adType}

`var adType: AdType { get }`

Ad type. See possible values in [AdType](AdType.md).

### adNetwork {#property_adNetwork}

`var adNetwork: String? { get }`

Yandex Advertising Network. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### adUnitID {#property_adUnitID}

`var adUnitID: String? { get }`

Ad block ID. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### adUnitName {#property_adUnitName}

`var adUnitName: String? { get }`

Ad unit name. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### adPlacementID {#property_adPlacementID}

`var adPlacementID: String? { get }`

Ad placement ID. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### adPlacementName {#property_adPlacementName}

`var adPlacementName: String? { get }`

Ad placement name. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### precision {#property_precision}

`var precision: String? { get }`

Accuracy. For example, <q>publisher_defined</q> or <q>estimated</q>. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### payload {#property_payload}

`var payload: [String: String]? { get }`

Accuracy. For example, <q>publisher_defined</q> or <q>estimated</q>. Arbitrary payload: Additional information presented as key-value pairs. The maximum size is 30 KB. If the value exceeds this limit, it will be truncated by AppMetrica.
