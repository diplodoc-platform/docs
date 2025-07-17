# AMACustomNumberAttribute protocol

The protocol defines methods for updating the value of a numeric attribute.

## Instance methods {#instance_summary}

#|
|| -[withValue:](#method_withValue) | Updates the attribute value. ||
|| -[withValueIfUndefined:](#method_withValueIfUndefined) | Updates the attribute value if it wasn't set earlier. ||
|| -[withValueReset](#method_withValueReset) | Resets the attribute value. ||
|#

## Method descriptions {#method_detail}

### -withValue: {#method_withValue}

```objectivec translate=no
- (AMAUserProfileUpdate *)withValue:(double)value
```

Updates the attribute value.

**Parameters:**

#|
|| `value` | The value of the numeric attribute. The data type is `double`. ||
|#

**Returns:**

The `AMAUserProfileUpdate` class instance.

### -withValueIfUndefined: {#method_withValueIfUndefined}

```objectivec translate=no
- (AMAUserProfileUpdate *)withValueIfUndefined:(double)value
```

Updates the attribute value if it wasn't set earlier.

**Parameters:**

#|
|| `value` | The value of the numeric attribute. The data type is `double`. ||
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
