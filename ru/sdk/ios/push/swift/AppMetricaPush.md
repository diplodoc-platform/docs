# Класс AppMetricaPush

Основной класс для обработки Push-уведомлений.

## Методы экземпляра

#|
|| +[downloadAttachmentsForNotificationRequest:](#method_downloadAttachmentsForNotificationRequest) | Загружает прикрепленные файлы в push-уведомлениях. Метод доступен для iOS 10.0 и выше. ||
|| +[handleApplicationDidFinishLaunchingWithOptions:](#method_handleApplicationDidFinishLaunchingWithOptions) | Обрабатывает открытие push-уведомления из метода [application(_:didFinishLaunchingWithOptions:)](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622921-application?language=swift). ||
|| +[handleDidReceiveNotificationRequest:](#method_handleDidReceiveNotificationRequest) | Обрабатывает получение push-уведомления из расширения Notification Service Extension. ||
|| +[handleRemoteNotification:](#method_handleRemoteNotification) | Обрабатывает открытие push-уведомления из метода [application(_:didReceiveRemoteNotification:fetchCompletionHandler:)](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1623013-application?language=swift). ||
|| +[handleSceneWillConnectToSession:](#method_handleSceneWillConnectToSession) | Обрабатывает открытие push-уведомления из метода [scene(_:willConnectTo:options:)](https://developer.apple.com/documentation/uikit/uiscenedelegate/3197914-scene). ||
|| +[isNotificationRelatedToSDK:](#method_isNotificationRelatedToSDK) | Возвращает `YES`, если push-уведомление относится к AppMetrica. ||
|| +[setDeviceTokenFromData:](#method_setDeviceTokenFromData) | Регистрирует device token приложения с production-окружением. ||
|| +[setDeviceTokenFromData:pushEnvironment:](#method_setDeviceTokenFromData_pushEnvironment) | Регистрирует device token приложения с указанным окружением. ||
|| +[setExtensionAppGroup:](#method_setExtensionAppGroup) | Регистрирует общую группу App Groups приложения и Notification Service Extension. ||
|| +[userDataForNotification:](#method_userDataForNotification) | Возвращает произвольную строку данных, которая передается в push-уведомлении. ||
|#

## Свойства {#property_summary}

#|
|| [userNotificationCenterDelegate](#property_userNotificationCenterDelegate) | Возвращает делегат [UserNotificationCenterDelegate](UserNotificationCenterDelegate.md), который обрабатывает foreground push-уведомления на iOS 10 и выше. ||
|| [userNotificationCenterHandler](#property_userNotificationCenterHandler) | Возвращает делегат [UserNotificationCenterHandling](UserNotificationCenterHandling.md), который позволяет вручную обрабатывать foreground push-уведомления на iOS 10 и выше. ||
|#

## Описание методов

### downloadAttachmentsForNotificationRequest: {#method_downloadAttachmentsForNotificationRequest}

```swift translate=no
class func downloadAttachments(request: UNNotificationRequest, callback: AttachmentsDownloadCallback)
```

Загружает прикрепленные файлы в push-уведомлениях. Метод доступен для iOS 10.0 и выше.

**Параметры:**

#|
|| `request` | Объект класса [UNNotificationRequest](https://developer.apple.com/documentation/usernotifications/unnotificationrequest). ||
|| `callback` | Callback-блок загрузки содержимого уведомлений. Формат:
```swift translate=no
public typealias AttachmentsDownloadCallback = ([UNNotificationAttachment]?, Error?) -> Void`
```
Включает в себя массив вложений `attachments` и ошибку `error`, если во время загрузки произошла ошибка. ||
|#

### handleApplicationDidFinishLaunching(withOptions:) {#method_handleApplicationDidFinishLaunchingWithOptions}

```swift translate=no
class func handleApplicationDidFinishLaunching(withOptions launchOptions: [AnyHashable : Any]?)
```

Обрабатывает открытие push-уведомления из метода [application(_:didFinishLaunchingWithOptions:)](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622921-application?language=swift). Метод должен быть вызван после инициализации AppMetrica SDK.

**Параметры:**

#|
|| `launchOptions` | Параметры в виде пар «ключ-значение», которые содержат информацию о запуске приложения. ||
|#

### handleDidReceive(_:) {#method_handleDidReceiveNotificationRequest}

```swift translate=no
class func handleDidReceive(_ request: UNNotificationRequest?)
```

Обрабатывает получение push-уведомления из расширения Notification Service Extension.

Метод должен быть вызван в реализации метода [didReceive(_:withContentHandler:)](https://developer.apple.com/documentation/usernotifications/unnotificationserviceextension/1648229-didreceive).

**Параметры:**

#|
|| `request` | Объект класса [UNNotificationRequest](https://developer.apple.com/documentation/usernotifications/unnotificationrequest?language=swift). ||
|#

### handleRemoteNotification(_:) {#method_handleRemoteNotification}

```swift translate=no
class func handleRemoteNotification(_ userInfo: [AnyHashable : Any]?)
```

Обрабатывает открытие push-уведомления из метода [application(_:didReceiveRemoteNotification:fetchCompletionHandler:)](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1623013-application?language=swift). Метод должен быть вызван после инициализации AppMetrica SDK.

**Параметры:**

#|
|| `userInfo` | Параметры push-уведомлений в виде пар «ключ-значение», которые передаются системой. ||
|#

### handleSceneWillConnectToSession(with: connectionOptions) {#method_handleSceneWillConnectToSession}

```swift translate=no
class func handleSceneWillConnectToSession(with: connectionOptions)
```

Обрабатывает открытие push-уведомления из метода [scene(_:willConnectTo:options:)](https://developer.apple.com/documentation/uikit/uiscenedelegate/3197914-scene). Метод должен быть вызван после инициализации AppMetrica SDK.

**Параметры:**

#|
|| `connectionOptions` | Объект класса [UIScene.ConnectionOptions](https://developer.apple.com/documentation/uikit/uiscene/connectionoptions) с параметрами подключения, которые передаются системой. ||
|#

### isNotificationRelated(toSDK:) {#method_isNotificationRelatedToSDK}

```swift translate=no
class func isNotificationRelated(toSDK userInfo: [AnyHashable : Any]?) -> Bool
```

Возвращает `YES`, если push-уведомление относится к AppMetrica.

**Параметры:**

#|
|| `userInfo` | Параметры push-уведомлений в виде пар «ключ-значение», которые передаются системой. ||
|#

**Возвращает:**

- `YES` — если push-уведомление относится к AppMetrica.
- `NO` — если push-уведомление не относится к AppMetrica.

### setDeviceTokenFrom(_:) {#method_setDeviceTokenFromData}

```swift translate=no
class func setDeviceTokenFrom(_ data: Data?)
```

Регистрирует device token приложения с production-окружением. Метод должен быть вызван после инициализации AppMetrica SDK.

**Параметры:**

#|
|| `data` | Device token приложения.

Если передается значение `nil`, предыдущий device token отзывается. ||
|#

### setDeviceTokenFrom(_:pushEnvironment:) {#method_setDeviceTokenFromData_pushEnvironment}

```swift translate=no
class func setDeviceTokenFrom(_ data: Data?, pushEnvironment: AppMetricaPushEnvironment)
```

Регистрирует device token приложения с указанным окружением. Метод должен быть вызван после инициализации AppMetrica SDK.

{% note alert %}

AppMetrica позволяет отправлять push-уведомления в Sandbox APNs. Но обработка push-уведомлений может работать некорректно, если на устройстве запускались версии приложения с разным окружением (_development_ и _production_). Чтобы избежать этого, можно использовать отдельный тестовый API key для _development_ окружения.

{% endnote %}

**Параметры:**

#|
|| `data` | Device token приложения.

Если передается значение `nil`, предыдущий device token отзывается. ||
|| `pushEnvironment` | APNs окружение приложения. ||
|#

### setExtensionAppGroup(_:) {#method_setExtensionAppGroup}

```swift translate=no
class func setExtensionAppGroup(_ appGroup: String?)
```

Регистрирует общую группу App Groups приложения и Notification Service Extension.

Регистрация необходима для отслеживания доставки push-уведомлений. Подробнее в разделе [Настройка сбора статистики push-уведомлений](../ios-settings.md).

**Параметры:**

#|
|| `appGroup` | Название общей группы App Groups. ||
|#

### userData(forNotification:) {#method_userDataForNotification}

```swift translate=no
class func userData(forNotification userInfo: [AnyHashable : Any]?) -> String?
```

Возвращает произвольную строку данных, которая передается в push-уведомлении:

- В поле **Дополнительные данные** при отправке из интерфейса AppMetrica.
- В поле `data` при отправке с помощью [Push API](../../../../mobile-api/push/about.md).

**Параметры:**

#|
|| `userInfo` | Параметры push-уведомлений в виде пар «ключ-значение», которые передаются системой. ||
|#

**Возвращает:**

Произвольная строка данных.

## Описание свойств {#property_detail}

### userNotificationCenterDelegate {#property_userNotificationCenterDelegate}

```swift translate=no
var userNotificationCenterDelegate: UserNotificationCenterDelegate? { get }
```

Возвращает делегат [UserNotificationCenterDelegate](UserNotificationCenterDelegate.md), который обрабатывает foreground push-уведомления на iOS 10 и выше.

Для обработки foreground push-уведомлений, добавьте этот код в методе [application(_:didFinishLaunchingWithOptions:)](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622921-application?language=swift):

```swift translate=no
let delegate = AppMetricaPush.userNotificationCenterDelegate
UNUserNotificationCenter.current().delegate = delegate
```

Для ручной обработки push-уведомлений используйте [userNotificationCenterHandler](#property_userNotificationCenterHandler).

### userNotificationCenterHandler {#property_userNotificationCenterHandler}

```swift translate=no
var userNotificationCenterHandler: UserNotificationCenterHandling? { get }
```

Возвращает делегат [UserNotificationCenterHandling](UserNotificationCenterHandling.md), который позволяет вручную обрабатывать foreground push-уведомления на iOS 10 и выше.

Используйте этот делегат, если вы реализуете протокол [UNUserNotificationCenterDelegate](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate?language=objc) с собственной логикой. При этом необходимо реализовать каждый метод из делегата `UNUserNotificationCenterDelegate` и вызывать соответствующие методы в `UserNotificationCenterHandling`.

Для упрощенной обработки push-уведомлений используйте [userNotificationCenterDelegate](#property_userNotificationCenterDelegate).
