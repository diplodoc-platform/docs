# Протокол AMACustomStringAttribute

Протокол определяет методы для обновления значения строкового атрибута.

## Методы экземпляра {#instance_summary}

#|
|| -[withValue:](#method_withValue) | Обновляет значение атрибута. ||
|| -[withValueIfUndefined:](#method_withValueIfUndefined) | Обновляет значение атрибута, если оно не было установлено ранее. ||
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
|| `value` | Обновляет значение атрибута. ||
|#

**Возвращает:**

Объект класса `AMAUserProfileUpdate`.

### -withValueIfUndefined: {#method_withValueIfUndefined}

```objectivec translate=no
- (AMAUserProfileUpdate *)withValueIfUndefined:(nullable NSString *)value
```

Обновляет значение атрибута, если оно не было установлено ранее.

**Параметры:**

#|
|| `value` | Значение атрибута в виде строки. Максимальная длина значения — 200 символов. ||
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
