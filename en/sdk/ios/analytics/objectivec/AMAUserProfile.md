# AMAUserProfile class

Immutable class for storing the user profile.

Use the [AMAMutableUserProfile](AMAMutableUserProfile.md) class to change the user profile.

A user profile is a set of user attributes. User profile details are displayed in the AppMetrica report on user profiles.

The instance of the `AMAUserProfile` class should be passed to the AppMetrica server using the [reportUserProfile](AMAAppMetrica.md#method_reportUserProfile) method of the [AMAAppMetrica](AMAAppMetrica.md) class. Use methods of the [AMAProfileAttribute](AMAProfileAttribute.md) class to create user attributes.

## Instance methods {#instance_summary}

#|
|| -[initWithUpdates:](#method_initWithUpdates) | Initializes the user profile with the specified set of updates. ||
|#

## Properties {#property_summary}

#|
|| [updates](#property_updates) | Array that contains attribute updates. ||
|#

## Method descriptions {#method_detail}

### -initWithUpdates: {#method_initWithUpdates}

```objectivec translate=no
- (instancetype)initWithUpdates:(NSArray<AMAUserProfileUpdate *> *)updates
```

Initializes the user profile with the specified set of updates.

**Parameters:**

#|
|| `updates` | Array that contains attribute updates. ||
|#

**Returns:**

The `AMAUserProfile` class instance.

## Property descriptions {#property_detail}

### updates {#property_updates}

`(nonatomic, copy, readonly) NSArray<AMAUserProfileUpdate *> *updates`

Array that contains attribute updates.
