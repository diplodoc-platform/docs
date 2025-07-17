# AMACustomBoolAttribute protocol

The protocol defines methods for updating the value of a boolean attribute.

## Instance methods {#instance_summary}

#|
|| -[withValue:](#method_withValue) | Updates the attribute value. ||
|| -[withValueIfUndefined:](#method_withValueIfUndefined) | Updates the attribute value if it wasn't set earlier. ||
|| -[withValueReset](#method_withValueReset) | Resets the attribute value. ||
|#

## Method descriptions {#method_detail}

### -withValue: {#method_withValue}

```objectivec translate=no
- (AMAUserProfileUpdate *)withValue:(BOOL)value
```

Updates the attribute value.

**Parameters:**

#|
|| `value` | Attribute value: `YES` or `NO`. ||
|#

**Returns:**

The `AMAUserProfileUpdate` class instance.

### -withValueIfUndefined: {#method_withValueIfUndefined}

```objectivec translate=no
- (AMAUserProfileUpdate *)withValueIfUndefined:(BOOL)value
```

Updates the attribute value if it wasn't set earlier.

**Parameters:**

#|
|| `value` | Attribute value: `YES` or `NO`. ||
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
