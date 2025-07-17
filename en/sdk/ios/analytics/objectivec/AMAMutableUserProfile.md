# AMAMutableUserProfile class

The mutable version of the [AMAUserProfile](AMAUserProfile.md) class for storing the user profile.

A user profile is a set of user attributes. User profile details are displayed in the AppMetrica report on user profiles.

The instance of the `AMAMutableUserProfile` class should be passed to the AppMetrica server using the [reportUserProfile](AMAAppMetrica.md#method_reportUserProfile) method of the [AMAAppMetrica](AMAAppMetrica.md) class. Use methods of the [AMAProfileAttribute](AMAProfileAttribute.md) class to create user attributes.

## Instance methods {#instance_summary}

#|
|| -[apply:](#method_apply) | Updates a single attribute of the user profile. ||
|| -[applyFromArray:](#method_applyFromArray) | Updates several attributes of the user profile. ||
|#

## Method descriptions {#method_detail}

### -apply: {#method_apply}

```objectivec translate=no
- (void)apply:(AMAUserProfileUpdate *)update
```

Updates a single attribute of the user profile.

**Parameters:**

#|
|| `update` | The `AMAUserProfileUpdate` class instance. ||
|#

### -applyFromArray: {#method_applyFromArray}

```objectivec translate=no
- (void)applyFromArray:(NSArray<AMAUserProfileUpdate *>*)updatesArray
```

Updates several attributes of the user profile.

**Parameters:**

#|
|| `updatesArray` | Array of `AMAUserProfileUpdate` instances. ||
|#
