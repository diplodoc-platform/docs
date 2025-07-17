# Протокол AMPUserNotificationCenterDelegate

Делегат для обработки foreground push-уведомления на iOS 10 и выше.

Для обработки foreground push-уведомлений, добавьте этот код в методе [application:didFinishLaunchingWithOptions:](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622921-application?language=objc):

```objectivec translate=no
[UNUserNotificationCenter currentNotificationCenter].delegate = [AMPAppMetricaPush userNotificationCenterDelegate];
```

## Свойства {#property_summary}

#|
|| [presentationOptions](#property_presentationOptions) | {{ presentationOptions }} ||
|| [nextDelegate](#property_nextDelegate) | {{ nextDelegate }} ||
|#

## Описание свойств {#property_detail}

### presentationOptions {#property_presentationOptions}

```objectivec translate=no
(nonatomic, assign) [UNNotificationPresentationOptions](https://developer.apple.com/documentation/usernotifications/unnotificationpresentationoptions) presentationOptions
```

Параметры представления push-уведомлений. Они передаются в обработчик [userNotificationCenter: willPresentNotification: withCompletionHandler:](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/1649518-usernotificationcenter?language=objc).

Делегат вызывает обработчик, если свойство `nextDelegate` не установлено или если объект в `nextDelegate` не отвечает.

### nextDelegate {#property_nextDelegate}

```objectivec translate=no
(nonatomic, weak, nullable) id<UNUserNotificationCenterDelegate> nextDelegate;
```

Делегат, в который передаются вызовы этого протокола.
