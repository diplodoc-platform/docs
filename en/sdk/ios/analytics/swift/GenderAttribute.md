# GenderAttribute protocol

The protocol defines methods for updating the gender of a user profile.

## Instance methods {#instance_summary}

#|
|| [withValue(_:)](#method_withValue) | Updates the attribute value with the specified value from the [GenderType](GenderType.md) enum. ||
|| [withValueReset()](#method_withValueReset) | Resets the attribute value. ||
|#

## Method descriptions {#method_detail}

### withValue(_:) {#method_withValue}

```swift translate=no
func withValue(_ value: GenderType) -> UserProfileUpdate
```

Updates the attribute value with the specified value from the [GenderType](GenderType.md) enum.

**Parameters:**

#|
|| `value` | The value from the [GenderType](GenderType.md) enum. ||
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
