# Протокол AMANameAttribute

Протокол определяет методы для обновления имени пользовательского профиля.

## Методы экземпляра {#instance_summary}

#|
|| -[withValue:](#method_withValue) | Обновляет значение атрибута. ||
|| -[withValueReset](#method_withValueReset) | Сбрасывает значение атрибута. ||
|#

## Описание методов {#method_detail}

### -withValue: {#method_withValue}

```objectivec translate=no
- (AMAUserProfileUpdate *)withValue:(nullable NSString *)value
```

Обновляет значение атрибута.

**Параметры:**

#|
|| `value` | Имя пользовательского профиля. Максимальная длина имени — 100 символов. ||
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
