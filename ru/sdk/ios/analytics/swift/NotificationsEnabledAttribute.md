# Протокол NotificationsEnabledAttribute

Протокол определяет методы для обновления статуса уведомлений пользовательского профиля.

Статус указывает, разрешил ли пользователь получать уведомления.

## Методы экземпляра {#instance_summary}

#|
|| [withValue(_:)](#method_withValue) | Обновляет значение атрибута. ||
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

### withValueReset() {#method_withValueReset}

```swift translate=no
func withValueReset() -> UserProfileUpdate
```

Сбрасывает значение атрибута.

**Возвращает:**

Объект класса `UserProfileUpdate`.
