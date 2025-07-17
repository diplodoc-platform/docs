# ProfileAttribute class

Methods of the class create predefined and custom profile attributes.

AppMetrica lets you create up to 100 custom attributes.

## Instance methods {#instance_summary}

#|
|| [birthDate()](#method_birthDate) | Creates a birth date attribute. ||
|| [customBool(_:)](#method_customBool) | Creates a custom attribute with the `bool` type. ||
|| [customCounter(_:)](#method_customCounter) | Creates a custom attribute with the tag type. ||
|| [customNumber(_:)](#method_customNumber) | Creates a custom attribute with the `double` type. ||
|| [customString(_:)](#method_customString) | Creates a custom attribute with the `string` type. ||
|| [gender()](#method_gender) | Creates a gender attribute. ||
|| [name()](#method_name) | Creates a name attribute. ||
|| [notificationsEnabled()](#method_notificationsEnabled) | Creates a notification status attribute. ||
|#

## Method descriptions {#method_detail}

### birthDate() {#method_birthDate}

```swift translate=no
class func birthDate() -> BirthDateAttribute
```

Creates a birth date attribute.

{% note alert %}

AppMetrica doesn't display [predefined attributes](../../../../data-collection/profile-attributes.md#pre-defined) in the web interface if `ProfieId` sending isn't configured.

{% endnote %}

**Returns:**

The instance that implements the [BirthDateAttribute](BirthDateAttribute.md) protocol.

### customBool(_:) {#method_customBool}

```swift translate=no
class func customBool(_ name: String) -> CustomBoolAttribute
```

Creates a custom attribute with the `bool` type.

**Parameters:**

#|
|| `name` | Attribute name. The value can contain up to 200 characters. ||
|#

**Returns:**

The instance that implements the [CustomBoolAttribute](CustomBoolAttribute.md) protocol.

### customCounter(_:) {#method_customCounter}

```swift translate=no
class func customCounter(_ name: String) -> CustomCounterAttribute
```

Creates a custom attribute of the counter type.

**Parameters:**

#|
|| `name` | Attribute name. The value can contain up to 200 characters. ||
|#

**Returns:**

The instance that implements the [CustomCounterAttribute](CustomCounterAttribute.md) protocol.

### customNumber(_:) {#method_customNumber}

```swift translate=no
class func customNumber(_ name: String) -> CustomNumberAttribute
```

Creates a custom attribute with the `double` type.

**Parameters:**

#|
|| `name` | Attribute name. The value can contain up to 200 characters. ||
|#

**Returns:**

The instance that implements the [CustomNumberAttribute](CustomNumberAttribute.md) protocol.

### customString(_:) {#method_customString}

```swift translate=no
class func customString(_ name: String) -> CustomStringAttribute
```

Creates a custom attribute with the `string` type.

**Parameters:**

#|
|| `name` | Attribute name. The value can contain up to 200 characters. ||
|#

**Returns:**

The instance that implements the [CustomStringAttribute](CustomStringAttribute.md) protocol.

### gender() {#method_gender}

```swift translate=no
class func gender() -> GenderAttribute
```

Creates a gender attribute.

{% note alert %}

AppMetrica doesn't display [predefined attributes](../../../../data-collection/profile-attributes.md#pre-defined) in the web interface if `ProfieId` sending isn't configured.

{% endnote %}

**Returns:**

The instance that implements the [GenderAttribute](GenderAttribute.md) protocol.

### name() {#method_name}

```swift translate=no
class func name() -> NameAttribute
```

Creates a name attribute.

{% note alert %}

AppMetrica doesn't display [predefined attributes](../../../../data-collection/profile-attributes.md#pre-defined) in the web interface if `ProfieId` sending isn't configured.

{% endnote %}

**Returns:**

The instance that implements the [NameAttribute](NameAttribute.md) protocol.

### notificationsEnabled() {#method_notificationsEnabled}

```swift translate=no
class func notificationsEnabled() -> NotificationsEnabledAttribute
```

Creates a NotificationsEnabled attribute.

{% note alert %}

AppMetrica doesn't display [predefined attributes](../../../../data-collection/profile-attributes.md#pre-defined) in the web interface if `ProfieId` sending isn't configured.

{% endnote %}

**Returns:**

The instance that implements the [NotificationsEnabledAttribute](NotificationsEnabledAttribute.md) protocol.
