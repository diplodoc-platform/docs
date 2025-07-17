# AMANameAttribute protocol

The protocol defines methods for updating the name of a user profile.

## Instance methods {#instance_summary}

#|
|| -[withValue:](#method_withValue) | Updates the attribute value. ||
|| -[withValueReset](#method_withValueReset) | Resets the attribute value. ||
|#

## Method descriptions {#method_detail}

### -withValue: {#method_withValue}

```objectivec translate=no
- (AMAUserProfileUpdate *)withValue:(nullable NSString *)value
```

Updates the attribute value.

**Parameters:**

#|
|| `value` | The name of the user profile. The maximum length of the user profile name is 100 characters. ||
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
