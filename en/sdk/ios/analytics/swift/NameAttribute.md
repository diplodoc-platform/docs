# NameAttribute protocol

The protocol defines methods for updating the name of a user profile.

## Instance methods {#instance_summary}

#|
|| [withValue(_:)](#method_withValue) | Updates the attribute value. ||
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
|| `value` | The name of the user profile. The maximum length of the user profile name is 100 characters. ||
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
