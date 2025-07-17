# AMABirthDateAttribute protocol

The protocol defines methods for updating the age or date of birth of a user profile.

## Instance methods {#instance_summary}

#|
|| -[withAge:](#method_withAge) | Updates the attribute value. ||
|| -[withYear:](#method_withYear) | Updates the attribute value. ||
|| -[withYear:month:](#method_withYear_month) | Updates the attribute value. ||
|| -[withYear:month:day:](#method_withYear_month_day) | Updates the attribute value. ||
|| -[withDateComponents:](#method_withDateComponents) | Updates the attribute value. ||
|| -[withValueReset](#method_withValueReset) | Resets the attribute value. ||
|#

## Method descriptions {#method_detail}

### -withAge: {#method_withAge}

```objectivec translate=no
- (AMAUserProfileUpdate *)withAge:(NSUInteger)value
```

Updates the attribute value.

**Parameters:**

#|
|| `value` | Age. ||
|#

**Returns:**

The `AMAUserProfileUpdate` class instance.

### -withYear: {#method_withYear}

```objectivec translate=no
- (AMAUserProfileUpdate *)withYear:(NSUInteger)year
```

Updates the attribute value.

**Parameters:**

#|
|| `year` | Year of birth. ||
|#

**Returns:**

The `AMAUserProfileUpdate` class instance.

### -withYear:month: {#method_withYear_month}

```objectivec translate=no
- (AMAUserProfileUpdate *)withYear:(NSUInteger)year month:(NSUInteger)month
```

Updates the attribute value.

**Parameters:**

#|
|| `year` | Year of birth. ||
|| `month` | Month of birth. ||
|#

**Returns:**

The `AMAUserProfileUpdate` class instance.

### -withYear:month:day: {#method_withYear_month_day}

```objectivec translate=no
- (AMAUserProfileUpdate *)withYear:(NSUInteger)year month:(NSUInteger)month day:(NSUInteger)day
```

Updates the attribute value.

**Parameters:**

#|
|| `year` | Year of birth. ||
|| `month` | Month of birth. ||
|| `day` | Day of birth. ||
|#

**Returns:**

The `AMAUserProfileUpdate` class instance.

### -withDateComponents: {#method_withDateComponents}

```objectivec translate=no
- (AMAUserProfileUpdate *)withDateComponents:(NSDateComponents *)dateComponents
```

Updates the attribute value.

**Parameters:**

#|
|| `dateComponents` | The [NSDateComponents](https://developer.apple.com/documentation/foundation/nsdatecomponents) class instance. ||
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
