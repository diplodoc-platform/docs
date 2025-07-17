# Класс UserProfile

Неизменяемый класс для хранения профиля пользователя.

Чтобы изменить профиля пользователя, воспользуйтесь классом [MutableUserProfile](MutableUserProfile.md).

Профиль пользователя — это набор пользовательских атрибутов. Сведения о профиле пользователя отображаются в отчете о профилях пользователей AppMetrica.

Объект `UserProfile` должен быть передан на сервер AppMetrica с помощью метода [reportUserProfile](AppMetrica.md#reportuserprofile_onfailure-method_reportuserprofile) класса [AppMetrica](AppMetrica.md). Используйте методы класса [ProfileAttribute](ProfileAttribute.md) для создания атрибутов.

## Методы экземпляра {#instance_summary}

#|
|| [init(updates:)](#method_initWithUpdates) | Инициализирует профиль пользователя с заданным набором обновлений. ||
|#

## Свойства {#property_summary}

#|
|| [updates](#property_updates) | Массив, который содержит обновления атрибутов. ||
|#

## Описание методов {#method_detail}

### init(updates:) {#method_initWithUpdates}

```swift translate=no
init(updates: [UserProfileUpdate])
```

Инициализирует профиль пользователя с заданным набором обновлений.

**Параметры:**

#|
|| `updates` | Массив, который содержит обновления атрибутов. ||
|#

**Возвращает:**

Объект класса `UserProfile`.

## Описание свойств {#property_detail}

### updates {#property_updates}

`var updates: [UserProfileUpdate] { get }`

Массив, который содержит обновления атрибутов.
