# Протокол AMACustomCounterAttribute

Протокол определяет методы для обновления значения атрибута типа счетчик.

## Методы экземпляра {#instance_summary}

#|
|| -[withDelta:](#method_withDelta) | Обновляет значение атрибута, изменяя его на указанную дельту. ||
|#

## Описание методов {#method_detail}

### -withDelta: {#method_withDelta}

```objectivec translate=no
- (AMAUserProfileUpdate *)withDelta:(double)value
```

Обновляет значение атрибута, изменяя его на указанную дельту.

**Параметры:**

#|
|| `value` | Дельта, на которую необходимо изменить значение атрибута. ||
|#

**Возвращает:**

Объект класса `AMAUserProfileUpdate`.
