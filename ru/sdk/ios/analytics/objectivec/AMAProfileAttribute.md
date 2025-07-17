# Класс AMAProfileAttribute

Методы класса создают предопределенные и собственные атрибуты профиля.

AppMetrica позволяет создать до 100 собственных атрибутов.

# Методы экземпляра {#instance_summary}

#|
|| +[birthDate](#method_birthDate) | Создает предопределенный атрибут для даты рождения/возраста. ||
|| +[customBool:](#method_customBool) | Создает собственный атрибут типа `bool`. ||
|| +[customCounter:](#method_customCounter) | Создает собственный атрибут типа счетчик. ||
|| +[customNumber:](#method_customNumber) | Создает собственный атрибут типа `double`. ||
|| +[customString:](#method_customString) | Создает собственный атрибут типа `string`. ||
|| +[gender](#method_gender) | Создает предопределенный атрибут для пола. ||
|| +[name](#method_name) | Создает предопределенный атрибут для имени. ||
|| +[notificationsEnabled](#method_notificationsEnabled) | Создает предопределенный атрибут для статуса уведомлений. ||
|#

## Описание методов {#method_detail}

### +birthDate {#method_birthDate}

```objectivec translate=no
+ (id<AMABirthDateAttribute>)birthDate
```

Создает предопределенный атрибут для даты рождения/возраста.

{% note alert %}

Если отправка `ProfileId` не настроена, [предопределенные атрибуты](../../../../data-collection/profile-attributes.md#pre-defined) не отображаются в веб-интерфейсе.

{% endnote %}

**Возвращает:**

Объект, реализующий протокол [AMABirthDateAttribute](AMABirthDateAttribute.md).

### +customBool: {#method_customBool}

```objectivec translate=no
+ (id<AMACustomBoolAttribute>)customBool:(NSString *)name
```

Создает собственный атрибут типа `bool`.

**Параметры:**

#|
|| `name` | Название атрибута. Может содержать до 200 символов. ||
|#

**Возвращает:**

Объект, реализующий протокол [AMACustomBoolAttribute](AMACustomBoolAttribute.md).

### +customCounter: {#method_customCounter}

```objectivec translate=no
+ (id<AMACustomCounterAttribute>)customCounter:(NSString *)name
```

Создает собственный атрибут типа счетчик.

**Параметры:**

#|
|| `name` | Создает собственный атрибут типа счетчик. ||
|#

**Возвращает:**

Объект, реализующий протокол [AMACustomCounterAttribute](AMACustomCounterAttribute.md).

### +customNumber: {#method_customNumber}

```objectivec translate=no
+ (id<AMACustomNumberAttribute>)customNumber:(NSString *)name
```

Создает собственный атрибут типа `double`.

**Параметры:**

#|
|| `name` | Создает собственный атрибут типа счетчик. ||
|#

**Возвращает:**

Объект, реализующий протокол [AMACustomNumberAttribute](AMACustomNumberAttribute.md).

### +customString: {#method_customString}

```objectivec translate=no
+ (id<AMACustomStringAttribute>)customString:(NSString *)name
```

Создает собственный атрибут типа `string`.

**Параметры:**

#|
|| `name` | Название атрибута. Может содержать до 200 символов. ||
|#

**Возвращает:**

Объект, реализующий протокол [AMACustomStringAttribute](AMACustomStringAttribute.md).

### +gender {#method_gender}

```objectivec translate=no
+ (id<AMAGenderAttribute>)gender
```

Создает предопределенный атрибут для пола.

{% note alert %}

Если отправка `ProfileId` не настроена, [предопределенные атрибуты](../../../../data-collection/profile-attributes.md#pre-defined) не отображаются в веб-интерфейсе.

{% endnote %}

**Возвращает:**

Объект, реализующий протокол [AMAGenderAttribute](AMAGenderAttribute.md).

### +name {#method_name}

```objectivec translate=no
+ (id<AMANameAttribute>)name
```

Создает предопределенный атрибут для имени.

{% note alert %}

Если отправка `ProfileId` не настроена, [предопределенные атрибуты](../../../../data-collection/profile-attributes.md#pre-defined) не отображаются в веб-интерфейсе.

{% endnote %}

**Возвращает:**

Объект, реализующий протокол [AMANameAttribute](AMANameAttribute.md).

### +notificationsEnabled {#method_notificationsEnabled}

```objectivec translate=no
+ (id<AMANotificationsEnabledAttribute>)notificationsEnabled
```

Создает предопределенный атрибут для статуса уведомлений.

{% note alert %}

Если отправка `ProfileId` не настроена, [предопределенные атрибуты](../../../../data-collection/profile-attributes.md#pre-defined) не отображаются в веб-интерфейсе.

{% endnote %}

**Возвращает:**

Объект, реализующий протокол [AMANotificationsEnabledAttribute](AMANotificationsEnabledAttribute.md).
