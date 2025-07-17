# Протокол CustomCounterAttribute

Протокол определяет методы для обновления значения атрибута типа счетчик.

## Методы экземпляра {#instance_summary}

#|
|| [withDelta(_:)](#method_withDelta) | Обновляет значение атрибута, изменяя его на указанную дельту. ||
|#

## Описание методов {#method_detail}

### withDelta(_:) {#method_withDelta}

```swift translate=no
func withDelta(_ value: Double) -> UserProfileUpdate
```

Обновляет значение атрибута, изменяя его на указанную дельту.

**Параметры:**

#|
|| `value` | Дельта, на которую необходимо изменить значение атрибута. ||
|#

**Возвращает:**

Объект класса `UserProfileUpdate`.
