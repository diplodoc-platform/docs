# Протокол AMANotificationsEnabledAttribute

Протокол определяет методы для обновления статуса уведомлений пользовательского профиля.

Статус указывает, разрешил ли пользователь получать уведомления.

## Методы экземпляра {#instance_summary}

#|
|| -[withValue:](#method_withValue) | Обновляет значение атрибута. ||
|| -[withValueReset](#method_withValueReset) | Сбрасывает значение атрибута. ||
|#

## Описание методов {#method_detail}

### -withValue: {#method_withValue}

```objectivec translate=no
- (AMAUserProfileUpdate *)withValue:(BOOL)value
```

Обновляет значение атрибута.

**Параметры:**

#|
|| `value` | Значение атрибута: `YES` или `NO`. ||
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
