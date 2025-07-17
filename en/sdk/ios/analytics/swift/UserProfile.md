# UserProfile class

Immutable class for storing the user profile.

Use the [MutableUserProfile](MutableUserProfile.md) class to change the user profile.

A user profile is a set of user attributes. User profile details are displayed in the AppMetrica report on user profiles.

The instance of the `UserProfile` class should be passed to the AppMetrica server using the [reportUserProfile](AppMetrica.md#reportuserprofile_onfailure-method_reportuserprofile) method of the [AppMetrica](AppMetrica.md) class. Use methods of the [ProfileAttribute](ProfileAttribute.md) class to create user attributes.

## Instance methods {#instance_summary}

#|
|| [init(updates:)](#method_initWithUpdates) | Initializes the user profile with the specified set of updates. ||
|#

## Properties {#property_summary}

#|
|| [updates](#property_updates) | Array that contains attribute updates. ||
|#

## Method descriptions {#method_detail}

### init(updates:) {#method_initWithUpdates}

```swift translate=no
init(updates: [UserProfileUpdate])
```

Initializes the user profile with the specified set of updates.

**Parameters:**

#|
|| `updates` | Array that contains attribute updates. ||
|#

**Returns:**

The `UserProfile` class instance.

## Property descriptions {#property_detail}

### updates {#property_updates}

`var updates: [UserProfileUpdate] { get }`

Array that contains attribute updates.
