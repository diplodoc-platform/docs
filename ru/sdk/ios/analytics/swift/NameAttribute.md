# Протокол NameAttribute

Протокол определяет методы для обновления имени пользовательского профиля.

## Методы экземпляра {#instance_summary}

#|
|| [withValue(_:)](#method_withValue) | Обновляет значение атрибута. ||
|| [withValueReset()](#method_withValueReset) | Сбрасывает значение атрибута. ||
|#

## Описание методов {#method_detail}

### withValue(_:) {#method_withValue}

```swift translate=no
func withValue(_ value: String?) -> UserProfileUpdate
```

Обновляет значение атрибута.

**Параметры:**

#|
|| `value` | Имя пользовательского профиля. Максимальная длина имени — 100 символов. ||
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
