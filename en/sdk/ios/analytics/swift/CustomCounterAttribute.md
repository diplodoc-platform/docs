# CustomCounterAttribute protocol

The protocol defines methods for updating the value of the tag type attribute.

## Instance methods {#instance_summary}

#|
|| [withDelta(_:)](#method_withDelta) | Updates the attribute value with the specified delta value. ||
|#

## Method descriptions {#method_detail}

### withDelta(_:) {#method_withDelta}

```swift translate=no
func withDelta(_ value: Double) -> UserProfileUpdate
```

Updates the attribute value with the specified delta value.

**Parameters:**

#|
|| `value` | The delta value to change the attribute value to. ||
|#

**Returns:**

The `UserProfileUpdate` class instance.
