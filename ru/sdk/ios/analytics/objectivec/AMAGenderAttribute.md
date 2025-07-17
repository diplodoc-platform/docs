# Протокол AMAGenderAttribute

Протокол определяет методы для обновления пола пользовательского профиля.

## Методы экземпляра {#instance_summary}

#|
|| [-withValue:](#method_withValue) | Обновляет значение атрибута, используя указанное значение из перечисления [AMAGenderType](AMAGenderType.md). ||
|| [-withValueReset](#method_withValueReset) | Сбрасывает значение атрибута. ||
|#

## Описание методов {#method_detail}

### -withValue: {#method_withValue}

```objectivec translate=no
- (AMAUserProfileUpdate *)withValue:(AMAGenderType)value
```

Обновляет значение атрибута, используя указанное значение из перечисления [AMAGenderType](AMAGenderType.md).

**Параметры:**

#|
|| `value` | Значение из перечисления [AMAGenderType](AMAGenderType.md). ||
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
