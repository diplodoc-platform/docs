# AMAGenderAttribute protocol

The protocol defines methods for updating the gender of a user profile.

## Instance methods {#instance_summary}

#|
|| [-withValue:](#method_withValue) | Updates the attribute value with the specified value from the [AMAGenderType](AMAGenderType.md) enum. ||
|| [-withValueReset](#method_withValueReset) | Resets the attribute value. ||
|#

## Method descriptions {#method_detail}

### -withValue: {#method_withValue}

```objectivec translate=no
- (AMAUserProfileUpdate *)withValue:(AMAGenderType)value
```

Updates the attribute value with the specified value from the [AMAGenderType](AMAGenderType.md) enum.

**Parameters:**

#|
|| `value` | The value from the [AMAGenderType](AMAGenderType.md) enum. ||
|#

**Returns:**

The `AMAUserProfileUpdate` class instance.

### -withValueReset {#method_withValueReset}

```objectivec translate=no
- (AMAUserProfileUpdate *)withValueReset
```

Resets the attribute value.

**Returns:**

The `AMAUserProfileUpdate` class instance.
