# Класс ProfileAttribute

Методы класса создают предопределенные и собственные атрибуты профиля.

AppMetrica позволяет создать до 100 собственных атрибутов.

## Методы экземпляра {#instance_summary}

#|
|| [birthDate()](#method_birthDate) | Создает предопределенный атрибут для даты рождения/возраста. ||
|| [customBool(_:)](#method_customBool) | Создает собственный атрибут типа `bool`. ||
|| [customCounter(_:)](#method_customCounter) | Создает собственный атрибут типа счетчик. ||
|| [customNumber(_:)](#method_customNumber) | Создает собственный атрибут типа `double`. ||
|| [customString(_:)](#method_customString) | Создает собственный атрибут типа `string`. ||
|| [gender()](#method_gender) | Создает предопределенный атрибут для пола. ||
|| [name()](#method_name) | Создает предопределенный атрибут для имени. ||
|| [notificationsEnabled()](#method_notificationsEnabled) | Создает предопределенный атрибут для статуса уведомлений. ||
|#

## Описание методов {#method_detail}

### birthDate() {#method_birthDate}

```swift translate=no
class func birthDate() -> BirthDateAttribute
```

Создает предопределенный атрибут для даты рождения/возраста.

{% note alert %}

Если отправка `ProfileId` не настроена, [предопределенные атрибуты](../../../../data-collection/profile-attributes.md#pre-defined) не отображаются в веб-интерфейсе.

{% endnote %}

**Возвращает:**

Объект, реализующий протокол [BirthDateAttribute](BirthDateAttribute.md).

### customBool(_:) {#method_customBool}

```swift translate=no
class func customBool(_ name: String) -> CustomBoolAttribute
```

Создает собственный атрибут типа `bool`.

**Параметры:**

#|
|| `name` | Название атрибута. Может содержать до 200 символов. ||
|#

**Возвращает:**

Объект, реализующий протокол [CustomBoolAttribute](CustomBoolAttribute.md).

### customCounter(_:) {#method_customCounter}

```swift translate=no
class func customCounter(_ name: String) -> CustomCounterAttribute
```

Создает собственный атрибут типа счетчик.

**Параметры:**

#|
|| `name` | Название атрибута. Может содержать до 200 символов. ||
|#

**Возвращает:**

Объект, реализующий протокол [CustomCounterAttribute](CustomCounterAttribute.md).

### customNumber(_:) {#method_customNumber}

```swift translate=no
class func customNumber(_ name: String) -> CustomNumberAttribute
```

Создает собственный атрибут типа `double`.

**Параметры:**

#|
|| `name` | Название атрибута. Может содержать до 200 символов. ||
|#

**Возвращает:**

Объект, реализующий протокол [CustomNumberAttribute](CustomNumberAttribute.md).

### customString(_:) {#method_customString}

```swift translate=no
class func customString(_ name: String) -> CustomStringAttribute
```

Создает собственный атрибут типа `string`.

**Параметры:**

#|
|| `name` | Название атрибута. Может содержать до 200 символов. ||
|#

**Возвращает:**

Объект, реализующий протокол [CustomStringAttribute](CustomStringAttribute.md).

### gender() {#method_gender}

```swift translate=no
class func gender() -> GenderAttribute
```

Создает предопределенный атрибут для пола.

{% note alert %}

Если отправка `ProfileId` не настроена, [предопределенные атрибуты](../../../../data-collection/profile-attributes.md#pre-defined) не отображаются в веб-интерфейсе.

{% endnote %}

**Возвращает:**

Объект, реализующий протокол [GenderAttribute](GenderAttribute.md).

### name() {#method_name}

```swift translate=no
class func name() -> NameAttribute
```

Создает предопределенный атрибут для имени.

{% note alert %}

Если отправка `ProfileId` не настроена, [предопределенные атрибуты](../../../../data-collection/profile-attributes.md#pre-defined) не отображаются в веб-интерфейсе.

{% endnote %}

**Возвращает:**

Объект, реализующий протокол [NameAttribute](NameAttribute.md).

### notificationsEnabled() {#method_notificationsEnabled}

```swift translate=no
class func notificationsEnabled() -> NotificationsEnabledAttribute
```

Создает предопределенный атрибут для статуса уведомлений.

{% note alert %}

Если отправка `ProfileId` не настроена, [предопределенные атрибуты](../../../../data-collection/profile-attributes.md#pre-defined) не отображаются в веб-интерфейсе.

{% endnote %}

**Возвращает:**

Объект, реализующий протокол [NotificationsEnabledAttribute](NotificationsEnabledAttribute.md).
