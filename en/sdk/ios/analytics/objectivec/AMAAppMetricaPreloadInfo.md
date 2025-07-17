# AMAAppMetricaPreloadInfo class

This class contains information for tracking pre-installed apps.

## Instance methods

#|
|| [-initWithTrackingIdentifier:](#method_initWithTrackingIdentifier) | Initializes the instance of the `AMAAppMetricaPreloadInfo` class with the specified `trackingID`. ||
|| [-setAdditionalInfo:forKey:](#method_setAdditionalInfo) | Sets additional parameters as <q>key-value</q> pairs that are used for [tracking pre-installed apps](../../../../mobile-tracking/preinstalled-app-attr.md). ||
|#

## Method descriptions {#method_detail}

### -initWithTrackingIdentifier: {#method_initWithTrackingIdentifier}

```objectivec translate=no
- (instancetype)initWithTrackingIdentifier:(NSString *)trackingID
```

Initializes the instance of the `AMAAppMetricaPreloadInfo` class with the specified `trackingID`.

**Parameters:**

#|
|| `trackingID` | Tracking ID for tracking pre-installed apps. ||
|#

**Returns:**

The `AMAAppMetricaPreloadInfo` class instance.

### -setAdditionalInfo:key: {#method_setAdditionalInfo}

```objectivec translate=no
- (void)setAdditionalInfo:(NSString *)info forKey:(NSString *)key
```

Sets additional parameters as <q>key-value</q> pairs that are used for [tracking pre-installed apps](../../../../mobile-tracking/preinstalled-app-attr.md).

This method may be invoked repeatedly for setting multiple pairs of additional information

**Parameters:**

#|
|| `info` | Value of the additional parameter. Can't be `nil`. Pairs with the `nil` value are ignored. ||
|| `key` | Key for the additional parameter. Can't be `nil`. Pairs with the `nil` key are ignored. ||
|#
