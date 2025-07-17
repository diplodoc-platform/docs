# AMAProfileAttribute class

Methods of the class create predefined and custom profile attributes.

AppMetrica lets you create up to 100 custom attributes.

# Instance methods {#instance_summary}

#|
|| +[birthDate](#method_birthDate) | Creates a predefined birth date / age attribute. ||
|| +[customBool:](#method_customBool) | Creates a custom attribute with the `bool` type. ||
|| +[customCounter:](#method_customCounter) | Creates a custom attribute with the tag type. ||
|| +[customNumber:](#method_customNumber) | Creates a custom attribute with the `double` type. ||
|| +[customString:](#method_customString) | Creates a custom attribute with the `string` type. ||
|| +[gender](#method_gender) | Creates a predefined gender attribute. ||
|| +[name](#method_name) | Creates a predefined name attribute. ||
|| +[notificationsEnabled](#method_notificationsEnabled) | Creates a predefined notification status attribute. ||
|#

## Method descriptions {#method_detail}

### +birthDate {#method_birthDate}

```objectivec translate=no
+ (id<AMABirthDateAttribute>)birthDate
```

Creates a birth date attribute.

{% note alert %}

AppMetrica doesn't display [predefined attributes](../../../../data-collection/profile-attributes.md#pre-defined) in the web interface if `ProfieId` sending isn't configured.

{% endnote %}

**Returns:**

The instance that implements the [AMABirthDateAttribute](AMABirthDateAttribute.md) protocol.

### +customBool: {#method_customBool}

```objectivec translate=no
+ (id<AMACustomBoolAttribute>)customBool:(NSString *)name
```

Creates a custom attribute with the `bool` type.

**Parameters:**

#|
|| `name` | Attribute name. The value can contain up to 200 characters. ||
|#

**Returns:**

The instance that implements the [AMACustomBoolAttribute](AMACustomBoolAttribute.md) protocol.

### +customCounter: {#method_customCounter}

```objectivec translate=no
+ (id<AMACustomCounterAttribute>)customCounter:(NSString *)name
```

Creates a custom attribute of the tag type.

**Parameters:**

#|
|| `name` | Creates a custom attribute with the tag type. ||
|#

**Returns:**

The instance that implements the [AMACustomCounterAttribute](AMACustomCounterAttribute.md) protocol.

### +customNumber: {#method_customNumber}

```objectivec translate=no
+ (id<AMACustomNumberAttribute>)customNumber:(NSString *)name
```

Creates a custom attribute with the `double` type.

**Parameters:**

#|
|| `name` | Creates a custom attribute with the tag type. ||
|#

**Returns:**

The instance that implements the [AMACustomNumberAttribute](AMACustomNumberAttribute.md) protocol.

### +customString: {#method_customString}

```objectivec translate=no
+ (id<AMACustomStringAttribute>)customString:(NSString *)name
```

Creates a custom attribute with the `string` type.

**Parameters:**

#|
|| `name` | Attribute name. The value can contain up to 200 characters. ||
|#

**Returns:**

The instance that implements the [AMACustomStringAttribute](AMACustomStringAttribute.md) protocol.

### +gender {#method_gender}

```objectivec translate=no
+ (id<AMAGenderAttribute>)gender
```

Creates a gender attribute.

{% note alert %}

AppMetrica doesn't display [predefined attributes](../../../../data-collection/profile-attributes.md#pre-defined) in the web interface if `ProfieId` sending isn't configured.

{% endnote %}

**Returns:**

The instance that implements the [AMAGenderAttribute](AMAGenderAttribute.md) protocol.

### +name {#method_name}

```objectivec translate=no
+ (id<AMANameAttribute>)name
```

Creates a name attribute.

{% note alert %}

AppMetrica doesn't display [predefined attributes](../../../../data-collection/profile-attributes.md#pre-defined) in the web interface if `ProfieId` sending isn't configured.

{% endnote %}

**Returns:**

The instance that implements the [AMANameAttribute](AMANameAttribute.md) protocol.

### +notificationsEnabled {#method_notificationsEnabled}

```objectivec translate=no
+ (id<AMANotificationsEnabledAttribute>)notificationsEnabled
```

Creates a predefined notification status attribute.

{% note alert %}

AppMetrica doesn't display [predefined attributes](../../../../data-collection/profile-attributes.md#pre-defined) in the web interface if `ProfieId` sending isn't configured.

{% endnote %}

**Returns:**

The instance that implements the [AMANotificationsEnabledAttribute](AMANotificationsEnabledAttribute.md) protocol.
