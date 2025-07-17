# Протокол AMPUserNotificationCenterHandling

Делегат для ручной обработки foreground push-уведомлений на iOS 10 и выше.

Используйте этот делегат, если вы реализуете протокол [UNUserNotificationCenterDelegate](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate?language=objc) с собственной логикой. При этом необходимо реализовать каждый метод из делегата `UNUserNotificationCenterDelegate` и вызывать его аналогичные методы в `AMPUserNotificationCenterHandling`.

Реализация этого делегата вызывается методом класса `AMPAppMetricaPush` [userNotificationCenterHandler](AMPAppMetricaPush.md#method_userNotificationCenterHandler).

## Методы экземпляра {#instance_summary}

#|
|| -[userNotificationCenterWillPresentNotification:](#method_userNotificationCenterWillPresentNotification) | Метод необходимо вызывать в вашей реализации [userNotificationCenter:willPresentNotification:withCompletionHandler:](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/1649518-usernotificationcenter?language=objc). ||
|| -[userNotificationCenterDidReceiveNotificationResponse:](#method_userNotificationCenterDidReceiveNotificationResponse) | Метод необходимо вызывать в вашей реализации [userNotificationCenter:didReceiveNotificationResponse:withCompletionHandler:](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/1649501-usernotificationcenter?language=objc). ||
|| -[userNotificationCenterOpenSettingsForNotification:](#method_userNotificationCenterOpenSettingsForNotification) | Метод необходимо вызывать в вашей реализации [userNotificationCenter:openSettingsForNotification:](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/2981869-usernotificationcenter?language=objc). ||
|#

## Описание методов {#method_detail}

### -userNotificationCenterWillPresentNotification: {#method_userNotificationCenterWillPresentNotification}

```objectivec translate=no
- (void)userNotificationCenterWillPresentNotification:(UNNotification *)notification
```

Метод необходимо вызывать в вашей реализации [userNotificationCenter:willPresentNotification:withCompletionHandler:](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/1649518-usernotificationcenter?language=objc).

**Параметры:**

#|
|| `notification` | Объект класса [UNNotification](https://developer.apple.com/documentation/usernotifications/unnotification). ||
|#

### -userNotificationCenterDidReceiveNotificationResponse: {#method_userNotificationCenterDidReceiveNotificationResponse}

```objectivec translate=no
- (void)userNotificationCenterDidReceiveNotificationResponse:(UNNotificationResponse *)response;
```

Метод необходимо вызывать в вашей реализации [userNotificationCenter:didReceiveNotificationResponse:withCompletionHandler:](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/1649501-usernotificationcenter?language=objc).

**Параметры:**

#|
|| `notification` | Объект класса [UNNotificationResponse](https://developer.apple.com/documentation/usernotifications/unnotificationresponse). ||
|#

### -userNotificationCenterOpenSettingsForNotification: {#method_userNotificationCenterOpenSettingsForNotification}

```objectivec translate=no
- (void)userNotificationCenterOpenSettingsForNotification:(nullable UNNotification *)notification API_AVAILABLE(ios(12.0));
```

Метод необходимо вызывать в вашей реализации [userNotificationCenter:openSettingsForNotification:](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/2981869-usernotificationcenter?language=objc).

**Параметры:**

#|
|| `notification` | Объект класса [UNNotification](https://developer.apple.com/documentation/usernotifications/unnotification). ||
|#
