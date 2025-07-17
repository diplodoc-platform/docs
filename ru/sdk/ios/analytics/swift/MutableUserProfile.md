# Класс MutableUserProfile

Изменяемая версия класса [UserProfile](UserProfile.md) для хранения профиля пользователя.

Профиль пользователя — это набор пользовательских атрибутов. Сведения о профиле пользователя отображаются в отчете о профилях пользователей AppMetrica.

Объект `MutableUserProfile` должен быть передан на сервер AppMetrica с помощью метода [reportUserProfile](AppMetrica.md#reportuserprofile_onfailure-method_reportuserprofile) класса [AppMetrica](AppMetrica.md). Используйте методы класса [ProfileAttribute](ProfileAttribute.md) для создания атрибутов.

## Методы экземпляра {#instance_summary}

#|
|| [apply(_:)](#method_apply) | Обновляет один атрибут пользовательского профиля. ||
|| [apply(from:)](#method_applyFromArray) | Обновляет несколько атрибутов пользовательского профиля. ||
|#

## Описание методов {#method_detail}

### apply(_:) {#method_apply}

```swift translate=no
func apply(_ update: UserProfileUpdate)
```

Обновляет один атрибут пользовательского профиля.

**Параметры:**

#|
|| `update` | Объект класса `UserProfileUpdate`. ||
|#

### apply(from:) {#method_applyFromArray}

```swift translate=no
func apply(from updatesArray: [UserProfileUpdate])
```

Обновляет несколько атрибутов пользовательского профиля.

**Параметры:**

#|
|| `updatesArray` | Массив объектов `UserProfileUpdate`. ||
|#
