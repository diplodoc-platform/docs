# MutableUserProfile class

The mutable version of the [UserProfile](UserProfile.md) class for storing the user profile.

A user profile is a set of user attributes. User profile details are displayed in the AppMetrica report on user profiles.

The instance of the `MutableUserProfile` class should be passed to the AppMetrica server using the [reportUserProfile](AppMetrica.md#reportuserprofile_onfailure-method_reportuserprofile) method of the [AppMetrica](AppMetrica.md) class. Use methods of the [ProfileAttribute](ProfileAttribute.md) class to create user attributes.

## Instance methods {#instance_summary}

#|
|| [apply(_:)](#method_apply) | Updates a single attribute of the user profile. ||
|| [apply(from:)](#method_applyFromArray) | Updates several attributes of the user profile. ||
|#

## Method descriptions {#method_detail}

### apply(_:) {#method_apply}

```swift translate=no
func apply(_ update: UserProfileUpdate)
```

Updates a single attribute of the user profile.

**Parameters:**

#|
|| `update` | The `UserProfileUpdate` class instance. ||
|#

### apply(from:) {#method_applyFromArray}

```swift translate=no
func apply(from updatesArray: [UserProfileUpdate])
```

Updates several attributes of the user profile.

**Parameters:**

#|
|| `updatesArray` | Array of `UserProfileUpdate` instances. ||
|#
