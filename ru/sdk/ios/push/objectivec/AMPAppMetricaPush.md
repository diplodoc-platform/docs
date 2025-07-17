# Класс AMPAppMetricaPush

Основной класс для обработки Push-уведомлений.

## Методы экземпляра

#|
|| +[downloadAttachmentsForNotificationRequest:](#method_downloadAttachmentsForNotificationRequest) | Загружает прикрепленные файлы в push-уведомлениях. Метод доступен для iOS 10.0 и выше. ||
|| +[handleApplicationDidFinishLaunchingWithOptions:](#method_handleApplicationDidFinishLaunchingWithOptions) | Обрабатывает открытие push-уведомления из метода [application:didFinishLaunchingWithOptions:](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622921-application?language=objc). ||
||+[handleDidReceiveNotificationRequest:](#method_handleDidReceiveNotificationRequest) | Обрабатывает получение push-уведомления из расширения Notification Service Extension. ||
|| +[handleRemoteNotification:](#method_handleRemoteNotification) | Обрабатывает открытие push-уведомления из метода [application:didReceiveRemoteNotification:fetchCompletionHandler:](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1623013-application?language=objc). ||
|| +[handleSceneWillConnectToSession:](#method_handleSceneWillConnectToSession) | Обрабатывает открытие push-уведомления из метода [scene:willConnectToSession:options:](https://developer.apple.com/documentation/uikit/uiscenedelegate/3197914-scene?language=objc). ||
|| +[isNotificationRelatedToSDK:](#method_isNotificationRelatedToSDK) | Возвращает `YES`, если push-уведомление относится к AppMetrica. ||
|| +[setDeviceTokenFromData:](#method_setDeviceTokenFromData) | Регистрирует device token приложения с production-окружением. ||
|| +[setDeviceTokenFromData:pushEnvironment:](#method_setDeviceTokenFromData_pushEnvironment) | Регистрирует device token приложения с указанным окружением. ||
|| +[setExtensionAppGroup:](#method_setExtensionAppGroup) | Регистрирует общую группу App Groups приложения и Notification Service Extension. ||
|| +[userDataForNotification:](#method_userDataForNotification) | Возвращает произвольную строку данных, которая передается в push-уведомлении. ||
|#

## Свойства {#property_summary}

#|
|| [userNotificationCenterDelegate](#property_userNotificationCenterDelegate) | Возвращает делегат [AMPUserNotificationCenterDelegate](AMPUserNotificationCenterDelegate.md), который обрабатывает foreground push-уведомления на iOS 10 и выше. ||
|| [userNotificationCenterHandler](#property_userNotificationCenterHandler) | Возвращает делегат [AMPUserNotificationCenterHandling](AMPUserNotificationCenterHandling.md), который позволяет вручную обрабатывать foreground push-уведомления на iOS 10 и выше. ||
|#

## Описание методов {#method_detail}

### +downloadAttachmentsForNotificationRequest: {#method_downloadAttachmentsForNotificationRequest}

```objectivec translate=no
+ (void)downloadAttachmentsForNotificationRequest:(UNNotificationRequest *)request
                                         callback:(AMPAttachmentsDownloadCallback)callback);
```

Загружает прикрепленные файлы в push-уведомлениях. Метод доступен для iOS 10.0 и выше.

**Параметры:**

#|
|| `request` | Объект класса [UNNotificationRequest](https://developer.apple.com/documentation/usernotifications/unnotificationrequest). ||
|| `callback` | Callback-блок загрузки прикрепленных файлов. Формат:

```objectivec translate=no
typedef void (^AMPAttachmentsDownloadCallback) (NSArray<UNNotificationAttachment *> * _Nullable attachments, NSError * _Nullable error)
```
Включает в себя массив вложений `attachments` и ошибку `error`, если во время загрузки произошла ошибка. ||
|#

### +handleApplicationDidFinishLaunchingWithOptions: {#method_handleApplicationDidFinishLaunchingWithOptions}

```objectivec translate=no
+ (void)handleApplicationDidFinishLaunchingWithOptions:(nullable NSDictionary *)launchOptions
```

Обрабатывает открытие push-уведомления из метода [application:didFinishLaunchingWithOptions:](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622921-application?language=objc). Метод должен быть вызван после инициализации AppMetrica SDK.

**Параметры:**

#|
|| `launchOptions` | Параметры в виде пар «ключ-значение», которые содержат информацию о запуске приложения. ||
|#

### +handleDidReceiveNotificationRequest: {#method_handleDidReceiveNotificationRequest}

```objectivec translate=no
+ (void)handleDidReceiveNotificationRequest:(UNNotificationRequest *)request
```

Обрабатывает получение push-уведомления из расширения Notification Service Extension.

Метод должен быть вызван в реализации метода [didReceiveNotificationRequest:withContentHandler:](https://developer.apple.com/documentation/usernotifications/unnotificationserviceextension/1648229-didreceivenotificationrequest).

**Параметры:**

#|
|| `request` | Объект класса [UNNotificationRequest](https://developer.apple.com/documentation/usernotifications/unnotificationrequest?language=objc). ||
|#

### +handleRemoteNotification: {#method_handleRemoteNotification}

```objectivec translate=no
+ (void)handleRemoteNotification:(NSDictionary *)userInfo
```

Обрабатывает открытие push-уведомления из метода [application:didReceiveRemoteNotification:fetchCompletionHandler:](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1623013-application?language=objc). Метод должен быть вызван после инициализации AppMetrica SDK.

**Параметры:**

#|
|| `userInfo` | Параметры push-уведомлений в виде пар «ключ-значение», которые передаются системой. ||
|#

### +handleSceneWillConnectToSession: {#method_handleSceneWillConnectToSession}

```objectivec translate=no
+ (void)handleSceneWillConnectToSessionWithOptions:(UISceneConnectionOptions *)connectionOptions
```

Обрабатывает открытие push-уведомления из метода [scene:willConnectToSession:options:](https://developer.apple.com/documentation/uikit/uiscenedelegate/3197914-scene?language=objc). Метод должен быть вызван после инициализации AppMetrica SDK.

**Параметры:**

#|
|| `connectionOptions` | Объект класса [UISceneConnectionOptions](https://developer.apple.com/documentation/uikit/uisceneconnectionoptions?language=objc) с параметрами подключения, которые передаются системой. ||
|#

### +isNotificationRelatedToSDK: {#method_isNotificationRelatedToSDK}

```objectivec translate=no
+ (BOOL)isNotificationRelatedToSDK:(NSDictionary *)userInfo;
```

Возвращает `YES`, если push-уведомление относится к AppMetrica.

**Параметры:**

#|
|| `userInfo` | Параметры push-уведомлений в виде пар «ключ-значение», которые передаются системой. ||
|#

**Возвращает:**

- `YES` — если push-уведомление относится к AppMetrica.
- `NO` — если push-уведомление не относится к AppMetrica.

### +setDeviceTokenFromData: {#method_setDeviceTokenFromData}

```objectivec translate=no
+ (void)setDeviceTokenFromData:(nullable NSData *)data
```

Регистрирует device token приложения с production-окружением. Метод должен быть вызван после инициализации AppMetrica SDK.

**Параметры:**

#|
|| `data` | Device token приложения.

Если передается значение `nil`, предыдущий device token отзывается. ||
|#

### +setDeviceTokenFromData:pushEnvironment: {#method_setDeviceTokenFromData_pushEnvironment}

```objectivec translate=no
+ (void)setDeviceTokenFromData:(nullable NSData *)data
               pushEnvironment:(AMPAppMetricaPushEnvironment)pushEnvironment
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

### +setExtensionAppGroup: {#method_setExtensionAppGroup}

```objectivec translate=no
+ (void)setExtensionAppGroup:(NSString *)appGroup
```

Регистрирует общую группу App Groups приложения и Notification Service Extension.

Регистрация необходима для отслеживания доставки push-уведомлений. Подробнее в разделе [Настройка сбора статистики push-уведомлений](../ios-settings.md).

**Параметры:**

#|
|| `appGroup` | Название общей группы App Groups. ||
|#

### +userDataForNotification: {#method_userDataForNotification}

```objectivec translate=no
+ (nullable NSString *)userDataForNotification:(NSDictionary *)userInfo
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

### +userNotificationCenterDelegate {#property_userNotificationCenterDelegate}

```objectivec translate=no
@property (readonly, class) id<AMPUserNotificationCenterDelegate> userNotificationCenterDelegate;
```

Возвращает делегат [AMPUserNotificationCenterDelegate](AMPUserNotificationCenterDelegate.md), который обрабатывает foreground push-уведомления на iOS 10 и выше.

Для обработки foreground push-уведомлений, добавьте этот код в методе [application:didFinishLaunchingWithOptions:](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622921-application?language=objc):

```objectivec translate=no
[UNUserNotificationCenter currentNotificationCenter].delegate = [AMPAppMetricaPush userNotificationCenterDelegate];
```

Для ручной обработки push-уведомлений используйте [userNotificationCenterHandler](#property_userNotificationCenterHandler).

### +userNotificationCenterHandler {#property_userNotificationCenterHandler}

```objectivec translate=no
@property (readonly, class) id<AMPUserNotificationCenterHandling> userNotificationCenterHandler;
```

Возвращает делегат [AMPUserNotificationCenterHandling](AMPUserNotificationCenterHandling.md), который позволяет вручную обрабатывать foreground push-уведомления на iOS 10 и выше.

Используйте этот делегат, если вы реализуете протокол [UNUserNotificationCenterDelegate](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate?language=objc) с собственной логикой. При этом необходимо реализовать каждый метод из делегата `UNUserNotificationCenterDelegate` и вызывать соответствующие методы в `AMPUserNotificationCenterHandling`.

Для упрощенной обработки push-уведомлений используйте [userNotificationCenterDelegate](#property_userNotificationCenterDelegate).
