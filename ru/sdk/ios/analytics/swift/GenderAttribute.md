# Протокол GenderAttribute

Протокол определяет методы для обновления пола пользовательского профиля.

## Методы экземпляра {#instance_summary}

#|
|| [withValue(_:)](#method_withValue) | Обновляет значение атрибута, используя указанное значение из перечисления [GenderType](GenderType.md). ||
|| [withValueReset()](#method_withValueReset) | Сбрасывает значение атрибута. ||
|#

## Описание методов {#method_detail}

### withValue(_:) {#method_withValue}

```swift translate=no
func withValue(_ value: GenderType) -> UserProfileUpdate
```

Обновляет значение атрибута, используя указанное значение из перечисления [GenderType](GenderType.md).

**Параметры:**

#|
|| `value` | Значение из перечисления [GenderType](GenderType.md). ||
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
