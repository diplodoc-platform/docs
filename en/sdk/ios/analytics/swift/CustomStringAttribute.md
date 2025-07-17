# CustomStringAttribute protocol

The protocol defines methods for updating the value of a string attribute.

## Instance methods {#instance_summary}

#|
|| [withValue(_:)](#method_withValue) | Updates the attribute value. ||
|| [withValueIfUndefined(_:)](#method_withValueIfUndefined) | Updates the attribute value if it wasn't set earlier. ||
|| [withValueReset()](#method_withValueReset) | Resets the attribute value. ||
|#

## Method descriptions {#method_detail}

### withValue(_:) {#method_withValue}

```swift translate=no
func withValue(_ value: String?) -> UserProfileUpdate
```

Updates the attribute value.

**Parameters:**

#|
|| `value` | Attribute value as a string. The maximum value length is 200 characters. ||
|#

**Returns:**

The `UserProfileUpdate` class instance.

### withValueIfUndefined(_:) {#method_withValueIfUndefined}

```swift translate=no
func withValueIfUndefined(_ value: String?) -> UserProfileUpdate
```

Updates the attribute value if it wasn't set earlier.

**Parameters:**

#|
|| `value` | Attribute value as a string. The maximum value length is 200 characters. ||
|#

**Returns:**

The `UserProfileUpdate` class instance.

### withValueReset() {#method_withValueReset}

```swift translate=no
func withValueReset() -> UserProfileUpdate
```

Resets the attribute value.

**Returns:**

The `UserProfileUpdate` class instance.
