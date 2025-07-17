# Протокол BirthDateAttribute

Протокол определяет методы для обновления возраста или даты рождения пользовательского профиля.

## Методы экземпляра {#instance_summary}

#|
|| -[withAge(_:)](#method_withAge) | Обновляет значение атрибута. ||
|| -[withDate(year:)](#method_withYear) | Обновляет значение атрибута. ||
|| -[withDate(year:month:)](#method_withYear_month) | Обновляет значение атрибута. ||
|| -[withDate(year:month:day:)](#method_withYear_month_day) | Обновляет значение атрибута. ||
|| -[withDate(dateComponents:)](#method_withDateComponents) | Обновляет значение атрибута. ||
|| -[withValueReset()](#method_withValueReset) | Сбрасывает значение атрибута. ||
|#

## Описание методов {#method_detail}

### withAge(_:) {#method_withAge}

```swift translate=no
func withAge(_ value: UInt) -> UserProfileUpdate
```

Обновляет значение атрибута.

**Параметры:**

#|
|| `value` | Возраст. ||
|#

**Возвращает:**

Объект класса `UserProfileUpdate`.

### withDate(year:) {#method_withYear}

```swift translate=no
func withDate(year: UInt) -> UserProfileUpdate
```

Обновляет значение атрибута.

**Параметры:**

#|
|| `year` | Год рождения. ||
|#

**Возвращает:**

Объект класса `UserProfileUpdate`.

### withDate(year:month:) {#method_withYear_month}

```swift translate=no
func withDate(year: UInt, month: UInt) -> UserProfileUpdate
```

Обновляет значение атрибута.

**Параметры:**

#|
|| `year` | Год рождения. ||
|| `month` | Месяц рождения. ||
|#

**Возвращает:**

Объект класса `UserProfileUpdate`.

### withDate(year:month:day:) {#method_withYear_month_day}

```swift translate=no
func withDate(year: UInt, month: UInt, day: UInt) -> UserProfileUpdate
```

Обновляет значение атрибута.

**Параметры:**

#|
|| `year` | Год рождения. ||
|| `month` | Месяц рождения. ||
|| `day` | День рождения. ||
|#

**Возвращает:**

Объект класса `UserProfileUpdate`.

### withDate(dateComponents:) {#method_withDateComponents}

```swift translate=no
func withDate(dateComponents: DateComponents) -> UserProfileUpdate
```

Обновляет значение атрибута.

**Параметры:**

#|
|| `dateComponents` | Объект класса [DateComponents](https://developer.apple.com/documentation/foundation/datecomponents). ||
|#

**Возвращает:**

Объект класса `UserProfileUpdate`.

### withValueReset() {#method_withValueReset}

```swift translate=no
func withValueReset() -> UserProfileUpdate
```

Сбрасывает значение атрибута.

**Возвращает:**

Объект класса `UserProfileUpdate`.
