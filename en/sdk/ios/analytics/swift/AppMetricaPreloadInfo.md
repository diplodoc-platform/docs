# AppMetricaPreloadInfo class

This class contains information for [tracking pre-installed apps](../../../../mobile-tracking/preinstalled-app-attr.md).

## Instance methods {#instance_summary}

#|
|| [init?(trackingIdentifier:)](#method_initWithTrackingIdentifier) | Initializes the instance of the `AppMetricaPreloadInfo` class with the specified `trackingID`. ||
|| [setAdditional(info:forKey:)](#method_setAdditionalInfo) | Sets additional parameters as <q>key-value</q> pairs that are used for [tracking pre-installed apps](../../../../mobile-tracking/preinstalled-app-attr.md). ||
|#

## Method descriptions {#method_detail}

### init?(trackingIdentifier:) {#method_initWithTrackingIdentifier}

```swift translate=no
init?(trackingIdentifier trackingID: String)
```

Initializes the instance of the `AppMetricaPreloadInfo` class with the specified `trackingID`.

**Parameters:**

#|
|| `trackingID` | Tracking ID for tracking pre-installed apps. ||
|#

**Returns:**

The `AppMetricaPreloadInfo` class instance.

### setAdditional(info:forKey:) {#method_setAdditionalInfo}

```swift translate=no
func setAdditional(info: String, forKey key: String)
```

Sets additional parameters as <q>key-value</q> pairs that are used for [tracking pre-installed apps](../../../../mobile-tracking/preinstalled-app-attr.md).

This method may be invoked repeatedly for setting multiple pairs of additional information

**Parameters:**

#|
|| `info` | Value of the additional parameter. Can't be `nil`. Pairs with the `nil` value are ignored. ||
|| `key` | Key for the additional parameter. Can't be `nil`. Pairs with the `nil` key are ignored. ||
|#
