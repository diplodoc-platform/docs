# Протокол AMABirthDateAttribute

Протокол определяет методы для обновления возраста или даты рождения пользовательского профиля.

## Методы экземпляра {#instance_summary}

#|
|| -[withAge:](#method_withAge) | Обновляет значение атрибута. ||
|| -[withYear:](#method_withYear) | Обновляет значение атрибута. ||
|| -[withYear:month:](#method_withYear_month) | Обновляет значение атрибута. ||
|| -[withYear:month:day:](#method_withYear_month_day) | Обновляет значение атрибута. ||
|| -[withDateComponents:](#method_withDateComponents) | Обновляет значение атрибута. ||
|| -[withValueReset](#method_withValueReset) | Сбрасывает значение атрибута. ||
|#

## Описание методов {#method_detail}

### -withAge: {#method_withAge}

```objectivec translate=no
- (AMAUserProfileUpdate *)withAge:(NSUInteger)value
```

Обновляет значение атрибута.

**Параметры:**

#|
|| `value` | Возраст. ||
|#

**Возвращает:**

Объект класса `AMAUserProfileUpdate`.

### -withYear: {#method_withYear}

```objectivec translate=no
- (AMAUserProfileUpdate *)withYear:(NSUInteger)year
```

Обновляет значение атрибута.

**Параметры:**

#|
|| `year` | Год рождения. ||
|#

**Возвращает:**

Объект класса `AMAUserProfileUpdate`.

### -withYear:month: {#method_withYear_month}

```objectivec translate=no
- (AMAUserProfileUpdate *)withYear:(NSUInteger)year month:(NSUInteger)month
```

Обновляет значение атрибута.

**Параметры:**

#|
|| `year` | Год рождения. ||
|| `month` | Месяц рождения. ||
|#

**Возвращает:**

Объект класса `AMAUserProfileUpdate`.

### -withYear:month:day: {#method_withYear_month_day}

```objectivec translate=no
- (AMAUserProfileUpdate *)withYear:(NSUInteger)year month:(NSUInteger)month day:(NSUInteger)day
```

Обновляет значение атрибута.

**Параметры:**

#|
|| `year` | Год рождения. ||
|| `month` | Месяц рождения. ||
|| `day` | День рождения. ||
|#

**Возвращает:**

Объект класса `AMAUserProfileUpdate`.

### -withDateComponents: {#method_withDateComponents}

```objectivec translate=no
- (AMAUserProfileUpdate *)withDateComponents:(NSDateComponents *)dateComponents
```

Обновляет значение атрибута.

**Параметры:**

#|
|| `dateComponents` | Объект класса [NSDateComponents](https://developer.apple.com/documentation/foundation/nsdatecomponents). ||
|#

**Возвращает:**

Объект класса `AMAUserProfileUpdate`.

### -withValueReset {#method_withValueReset}

```objectivec translate=no
- (AMAUserProfileUpdate *)withValueReset
```

Сбрасывает значение атрибута.

**Возвращает:**

Объект класса `AMAUserProfileUpdate`.
