# Класс AMAUserProfile

Неизменяемый класс для хранения профиля пользователя.

Чтобы изменить профиля пользователя, воспользуйтесь классом [AMAMutableUserProfile](AMAMutableUserProfile.md).

Профиль пользователя — это набор пользовательских атрибутов. Сведения о профиле пользователя отображаются в отчете о профилях пользователей AppMetrica.

Объект `AMAUserProfile` должен быть передан на сервер AppMetrica с помощью метода [reportUserProfile](AMAAppMetrica.md#method_reportUserProfile) класса [AMAAppMetrica](AMAAppMetrica.md). Используйте методы класса [AMAProfileAttribute](AMAProfileAttribute.md) для создания атрибутов.

## Методы экземпляра {#instance_summary}

#|
|| -[initWithUpdates:](#method_initWithUpdates) | Инициализирует профиль пользователя с заданным набором обновлений. ||
|#

## Свойства {#property_summary}

#|
|| [updates](#property_updates) | Массив, который содержит обновления атрибутов. ||
|#

## Описание методов {#method_detail}

### -initWithUpdates: {#method_initWithUpdates}

```objectivec translate=no
- (instancetype)initWithUpdates:(NSArray<AMAUserProfileUpdate *> *)updates
```

Инициализирует профиль пользователя с заданным набором обновлений.

**Параметры:**

#|
|| `updates` | Массив, который содержит обновления атрибутов. ||
|#

**Возвращает:**

Объект класса `AMAUserProfile`.

## Описание свойств {#property_detail}

### updates {#property_updates}

`(nonatomic, copy, readonly) NSArray<AMAUserProfileUpdate *> *updates`

Массив, который содержит обновления атрибутов.
