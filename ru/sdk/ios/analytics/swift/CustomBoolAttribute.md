# Протокол CustomBoolAttribute

Протокол определяет методы для обновления значения логического атрибута.

## Методы экземпляра {#instance_summary}

#|
|| [withValue(_:)](#method_withValue) | Обновляет значение атрибута. ||
|| [withValueIfUndefined(_:)](#method_withValueIfUndefined) | Обновляет значение атрибута, если оно не было установлено ранее. ||
|| [withValueReset()](#method_withValueReset) | Сбрасывает значение атрибута. ||
|#

## Описание методов {#method_detail}

### withValue(_:) {#method_withValue}

```swift translate=no
func withValue(_ value: Bool) -> UserProfileUpdate
```

Обновляет значение атрибута.

**Параметры:**

#|
|| `value` | Значение атрибута: `true` или `false`. ||
|#

**Возвращает:**

Объект класса `UserProfileUpdate`.

### withValueIfUndefined(_:) {#method_withValueIfUndefined}

```swift translate=no
func withValueIfUndefined(_ value: Bool) -> UserProfileUpdate
```

Обновляет значение атрибута, если оно не было установлено ранее.

**Параметры:**

#|
|| `value` | Значение атрибута: `true` или `false`. ||
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
