# BirthDateAttribute protocol

The protocol defines methods for updating the age or date of birth of a user profile.

## Instance methods {#instance_summary}

#|
|| -[withAge(_:)](#method_withAge) | Updates the attribute value. ||
|| -[withDate(year:)](#method_withYear) | Updates the attribute value. ||
|| -[withDate(year:month:)](#method_withYear_month) | Updates the attribute value. ||
|| -[withDate(year:month:day:)](#method_withYear_month_day) | Updates the attribute value. ||
|| -[withDate(dateComponents:)](#method_withDateComponents) | Updates the attribute value. ||
|| -[withValueReset()](#method_withValueReset) | Resets the attribute value. ||
|#

## Method descriptions {#method_detail}

### withAge(_:) {#method_withAge}

```swift translate=no
func withAge(_ value: UInt) -> UserProfileUpdate
```

Updates the attribute value.

**Parameters:**

#|
|| `value` | Age. ||
|#

**Returns:**

The `UserProfileUpdate` class instance.

### withDate(year:) {#method_withYear}

```swift translate=no
func withDate(year: UInt) -> UserProfileUpdate
```

Updates the attribute value.

**Parameters:**

#|
|| `year` | Year of birth. ||
|#

**Returns:**

The `UserProfileUpdate` class instance.

### withDate(year:month:) {#method_withYear_month}

```swift translate=no
func withDate(year: UInt, month: UInt) -> UserProfileUpdate
```

Updates the attribute value.

**Parameters:**

#|
|| `year` | Year of birth. ||
|| `month` | Month of birth. ||
|#

**Returns:**

The `UserProfileUpdate` class instance.

### withDate(year:month:day:) {#method_withYear_month_day}

```swift translate=no
func withDate(year: UInt, month: UInt, day: UInt) -> UserProfileUpdate
```

Updates the attribute value.

**Parameters:**

#|
|| `year` | Year of birth. ||
|| `month` | Month of birth. ||
|| `day` | Day of birth. ||
|#

**Returns:**

The `UserProfileUpdate` class instance.

### withDate(dateComponents:) {#method_withDateComponents}

```swift translate=no
func withDate(dateComponents: DateComponents) -> UserProfileUpdate
```

Updates the attribute value.

**Parameters:**

#|
|| `dateComponents` | The [DateComponents](https://developer.apple.com/documentation/foundation/datecomponents) class instance. ||
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
