# AMAAdRevenueInfo class

The class contains immutable information about advertising revenue (Ad Revenue).

Use the [AMAMutableAdRevenueInfo](AMAMutableAdRevenueInfo.md) class to change information about advertising revenue.

The instance of the `YMMAdRevenueInfo` class should be sent to the AppMetrica server using the [reportAdRevenue](AMAAppMetrica.md#method_reportAdRevenue) method of the [AMAAppMetrica](AMAAppMetrica.md) class.

## Instance methods {#instance_summary}

#|
|| [-initWithAdRevenue:adRevenue:currency:](#method_initWithAdRevenue__adRevenue__currency) | Initializes the instance of the `AMAAdRevenueInfo` class for sending information about advertising revenue. ||
|#

## Properties {#property_summary}

#|
|| [adRevenue](#property_adRevenue) | The amount of money received from advertising revenue. Can't be negative. ||
|| [currency](#property_currency) | The currency in which `adRevenue` is represented. Must be in ISO-4217 format. ||
|| [adType](#property_adType) | Ad type. See possible values in [AMAAdType](AMAAdType.md). ||
|| [adNetwork](#property_adNetwork) | Advertising network. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica. ||
|| [adUnitID](#property_adUnitID) | Ad unit ID. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica. ||
|| [adUnitName](#property_adUnitName) | Ad unit name. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica. ||
|| [adPlacementID](#property_adPlacementID) | Ad placement ID. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica. ||
|| [adPlacementName](#property_adPlacementName) | Ad placement name. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica. ||
|| [precision](#property_precision) | Accuracy. For example, «publisher_defined» or «estimated». The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica. ||
|| [payload](#property_payload) | Accuracy. For example, «publisher_defined» or «estimated». Arbitrary payload: Additional information presented as key-value pairs. The maximum size is 30 KB. If the value exceeds this limit, it will be truncated by AppMetrica. ||
|#

## Method descriptions {#method_detail}

### -initWithAdRevenue:adRevenue:currency: {#method_initWithAdRevenue__adRevenue__currency}

```objectivec translate=no
- (instancetype)initWithAdRevenue:(NSDecimalNumber *)adRevenue currency:(NSString *)currency
```

Initializes the instance of the `AMAAdRevenueInfo` class for sending information about advertising revenue.

**Parameters:**

#|
|| `adRevenue` | The amount of money received from advertising revenue. Can't be negative. ||
|| `currency` | The currency in which `adRevenue` is represented. Must be in ISO-4217 format. ||
|#

**Returns:**

The `AMAAdRevenueInfo` class instance.

## Property descriptions {#property_detail}

### adRevenue {#property_adRevenue}

`(nonatomic, strong, readonly) NSDecimalNumber *adRevenue`

The amount of money received from advertising revenue. Can't be negative.

### currency {#property_currency}

`(nonatomic, copy, readonly) NSString *currency`

The currency in which `adRevenue` is represented. Must be in ISO-4217 format.

### adType {#property_adType}

`(nonatomic, assign, readonly) AMAAdType adType`

Ad type. See possible values in [AMAAdType](AMAAdType.md).

### adNetwork {#property_adNetwork}

`(nonatomic, copy, nullable, readonly) NSString *adNetwork`

Yandex Advertising Network. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### adUnitID {#property_adUnitID}

`(nonatomic, copy, nullable, readonly) NSString *adUnitID`

Ad unit ID. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### adUnitName {#property_adUnitName}

`(nonatomic, copy, nullable, readonly) NSString *adUnitName`

Ad unit name. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### adPlacementID {#property_adPlacementID}

`(nonatomic, copy, nullable, readonly) NSString *adPlacementID`

Ad placement ID. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### adPlacementName {#property_adPlacementName}

`(nonatomic, copy, nullable, readonly) NSString *adPlacementName`

Ad placement name. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### precision {#property_precision}

`(nonatomic, copy, nullable, readonly) NSString *precision`

Accuracy. For example, <q>publisher_defined</q> or <q>estimated</q>. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### payload {#property_payload}

`(nonatomic, copy, nullable, readonly) NSDictionary<NSString *, NSString *> *payload`

Accuracy. For example, <q>publisher_defined</q> or <q>estimated</q>. Arbitrary payload: Additional information presented as key-value pairs. The maximum size is 30 KB. If the value exceeds this limit, it will be truncated by AppMetrica.
