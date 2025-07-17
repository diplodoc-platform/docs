# MutableAdRevenueInfo class

The mutable version of the [AdRevenueInfo](AdRevenueInfo.md) class with information about advertising revenue.

The instance of the `MutableAdRevenueInfo` class should be passed to the AppMetrica server using the [reportAdRevenue](AppMetrica.md#reportadrevenueonfailure-method_reportadrevenue) method of the [AppMetrica](AppMetrica.md) class.

## Properties {#property_summary}

#|
|| [adType](#property_adType) | Ad type. See possible values in [AdType](AdType.md). ||
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

`var adType: AdType`

Ad type. See possible values in [AdType](AdType.md).

### adNetwork {#property_adNetwork}

`var adNetwork: String?`

Yandex Advertising Network. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### adUnitID {#property_adUnitID}

`var adUnitID: String?`

Ad unit ID. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### adUnitName {#property_adUnitName}

`var adUnitName: String?`

Ad unit name. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### adPlacementID {#property_adPlacementID}

`var adPlacementID: String?`

Ad placement ID. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### adPlacementName {#property_adPlacementName}

`var adPlacementName: String?`

Ad placement name. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### precision {#property_precision}

`var precision: String?`

Accuracy. For example, <q>publisher_defined</q> or <q>estimated</q>. The maximum length is 100 characters. If the value exceeds this limit, it will be truncated by AppMetrica.

### payload {#property_payload}

`var payload: [String: String]?`

Accuracy. For example, <q>publisher_defined</q> or <q>estimated</q>. Arbitrary payload: Additional information presented as key-value pairs. The maximum size is 30 KB. If the value exceeds this limit, it will be truncated by AppMetrica.
