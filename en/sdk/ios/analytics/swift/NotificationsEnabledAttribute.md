# NotificationsEnabledAttribute protocol

The protocol defines methods for updating the notification status of a user profile.

It indicates whether the user has enabled notifications.

## Instance methods {#instance_summary}

#|
|| [withValue(_:)](#method_withValue) | Updates the attribute value. ||
|| [withValueReset()](#method_withValueReset) | Resets the attribute value. ||
|#

## Method descriptions {#method_detail}

### withValue(_:) {#method_withValue}

```swift translate=no
func withValue(_ value: Bool) -> UserProfileUpdate
```

Updates the attribute value.

**Parameters:**

#|
|| `value` | Attribute value: `true` or `false`. ||
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
