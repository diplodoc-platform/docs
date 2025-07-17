# Класс AMAMutableUserProfile

Изменяемая версия класса [AMAUserProfile](AMAUserProfile.md) для хранения профиля пользователя.

Профиль пользователя — это набор пользовательских атрибутов. Сведения о профиле пользователя отображаются в отчете о профилях пользователей AppMetrica.

Объект `AMAMutableUserProfile` должен быть передан на сервер AppMetrica с помощью метода [reportUserProfile](AMAAppMetrica.md#method_reportUserProfile) класса [AMAAppMetrica](AMAAppMetrica.md). Используйте методы класса [AMAProfileAttribute](AMAProfileAttribute.md) для создания атрибутов.

## Методы экземпляра {#instance_summary}

#|
|| -[apply:](#method_apply) | Обновляет один атрибут пользовательского профиля. ||
|| -[applyFromArray:](#method_applyFromArray) | Обновляет несколько атрибутов пользовательского профиля. ||
|#

## Описание методов {#method_detail}

### -apply: {#method_apply}

```objectivec translate=no
- (void)apply:(AMAUserProfileUpdate *)update
```

Обновляет один атрибут пользовательского профиля.

**Параметры:**

#|
|| `update` | Объект класса `AMAUserProfileUpdate`. ||
|#

### -applyFromArray: {#method_applyFromArray}

```objectivec translate=no
- (void)applyFromArray:(NSArray<AMAUserProfileUpdate *>*)updatesArray
```

Обновляет несколько атрибутов пользовательского профиля.

**Параметры:**

#|
|| `updatesArray` | Массив объектов `AMAUserProfileUpdate`. ||
|#
