# Протокол UserNotificationCenterDelegate

Делегат для обработки foreground push-уведомления на iOS 10 и выше.

Для обработки foreground push-уведомлений, добавьте этот код в методе [application(_:didFinishLaunchingWithOptions:)](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622921-application?language=swift):

```swift translate=no
let delegate = AppMetricaPush.userNotificationCenterDelegate
UNUserNotificationCenter.current().delegate = delegate
```

## Свойства {#property_summary}

#|
|| [presentationOptions](#property_presentationOptions) | {{ presentationOptions }} ||
|| [nextDelegate](#property_nextDelegate) | {{ nextDelegate }} ||
|#

## Описание свойств {#property_detail}

### presentationOptions {#property_presentationOptions}

```swift translate=no
var presentationOptions: UNNotificationPresentationOptions
```

Параметры представления push-уведомлений. Они передаются в обработчик [userNotificationCenter(_:willPresent:withCompletionHandler:)](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/1649518-usernotificationcenter?language=swift).

Делегат вызывает обработчик, если свойство `nextDelegate` не установлено или если объект в `nextDelegate` не отвечает.

### nextDelegate {#property_nextDelegate}

```swift translate=no
var nextDelegate: id<UNUserNotificationCenterDelegate>
```

{{ nextDelegate }}
