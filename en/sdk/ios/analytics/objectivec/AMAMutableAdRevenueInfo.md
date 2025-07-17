# AMAMutableAdRevenueInfo class

The mutable version of the [AMAAdRevenueInfo](AMAAdRevenueInfo.md) class with information about advertising revenue.

The `AMAMutableAdRevenueInfo` instance should be passed to the AppMetrica server using the [reportAdRevenue](AMAAppMetrica.md#method_reportAdRevenue) method of the [AMAAppMetrica](AMAAppMetrica.md) class.

## Properties {#property_summary}

#|
|| [adType](#property_adType) | Ad type. See possible values in [AMAAdType](AMAAdType.md). ||
|| [adNetwork](#property_adNetwork) | Advertising network. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica. ||
|| [adUnitID](#property_adUnitID) | Ad unit ID. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica. ||
|| [adUnitName](#property_adUnitName) | Ad unit name. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica. ||
|| [adPlacementID](#property_adPlacementID) | Ad placement ID. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica. ||
|| [adPlacementName](#property_adPlacementName) | Ad placement name. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica. ||
|| [precision](#property_precision) | Accuracy. For example, <q>publisher_defined</q> or <q>estimated</q>. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica. ||
|| [payload](#property_payload) | Accuracy. For example, <q>publisher_defined</q> or <q>estimated</q>. Arbitrary payload: Additional information presented as key-value pairs. The maximum size is 30 KB. If the value exceeds this limit, it will be truncated by AppMetrica. ||
|#

## Property descriptions {#property_detail}

### adType {#property_adType}

`(nonatomic, assign) AMAAdType adType`

Ad type. See possible values in [AMAAdType](AMAAdType.md).

### adNetwork {#property_adNetwork}

`(nonatomic, copy, nullable) NSString *adNetwork`

Yandex Advertising Network. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### adUnitID {#property_adUnitID}

`(nonatomic, copy, nullable) NSString *adUnitID`

Ad unit ID. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### adUnitName {#property_adUnitName}

`(nonatomic, copy, nullable) NSString *adUnitName`

Ad unit name. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### adPlacementID {#property_adPlacementID}

`(nonatomic, copy, nullable) NSString *adPlacementID`

Ad placement ID. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### adPlacementName {#property_adPlacementName}

`(nonatomic, copy, nullable) NSString *adPlacementName`

Ad placement name. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### precision {#property_precision}

`(nonatomic, copy, nullable) NSString *precision`

Accuracy. For example, <q>publisher_defined</q> or <q>estimated</q>. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### payload {##property_payload}

`(nonatomic, copy, nullable) NSDictionary<NSString *, NSString *> *payload`

Accuracy. For example, <q>publisher_defined</q> or <q>estimated</q>. Arbitrary payload: Additional information presented as key-value pairs. The maximum size is 30 KB. If the value exceeds this limit, it will be truncated by AppMetrica.
