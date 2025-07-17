# AMANotificationsEnabledAttribute protocol

The protocol defines methods for updating the notification status of a user profile.

It indicates whether the user has enabled notifications.

## Instance methods {#instance_summary}

#|
|| -[withValue:](#method_withValue) | Updates the attribute value. ||
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

### -withValueReset {#method_withValueReset}

```objectivec translate=no
- (AMAUserProfileUpdate *)withValueReset
```

Resets the attribute value.

**Returns:**

The `AMAUserProfileUpdate` class instance.
