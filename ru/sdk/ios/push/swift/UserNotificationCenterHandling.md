# Протокол UserNotificationCenterHandling

Делегат для ручной обработки foreground push-уведомлений на iOS 10 и выше.

Используйте этот делегат, если вы реализуете протокол [UNUserNotificationCenterDelegate](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate?language=swift) с собственной логикой. Вы должны реализовать каждый метод из делегата `UNUserNotificationCenterDelegate` и вызывать его аналогичные методы в `UserNotificationCenterHandling`.

Реализация этого делегата предоставляется методом класса `AppMetricaPush` [userNotificationCenterDelegate](AppMetricaPush.md#method_userNotificationCenterHandler).

## Методы экземпляра {#instance_summary}

#|
|| [userNotificationCenterWillPresent(_:)](#method_userNotificationCenterWillPresentNotification) | Метод необходимо вызывать в вашей реализации [userNotificationCenter(_:willPresent:withCompletionHandler:)](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/1649518-usernotificationcenter?language=swift). ||
|| [userNotificationCenterDidReceive(_:)](#method_userNotificationCenterDidReceiveNotificationResponse) | Метод необходимо вызывать в вашей реализации [userNotificationCenter(_:didReceive:withCompletionHandler:)](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/1649501-usernotificationcenter?language=swift). ||
|| [userNotificationCenterOpenSettings(_:)](#method_userNotificationCenterOpenSettingsForNotification) | Метод необходимо вызывать в вашей реализации [userNotificationCenter(_:openSettingsFor:)](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/2981869-usernotificationcenter?language=swift). ||
|#

## Описание методов {#method_detail}

### userNotificationCenterWillPresent(_:) {#method_userNotificationCenterWillPresentNotification}

```swift translate=no
func userNotificationCenterWillPresent(_ notification: UNNotification?)
```

Метод необходимо вызывать в вашей реализации [userNotificationCenter(_:willPresent:withCompletionHandler:)](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/1649518-usernotificationcenter?language=swift).

**Параметры:**

#|
|| `notification` | Объект класса [UNNotification](https://developer.apple.com/documentation/usernotifications/unnotification?language=swift). ||
|#

### userNotificationCenterDidReceive(_:) {#method_userNotificationCenterDidReceiveNotificationResponse}

```swift translate=no
func userNotificationCenterDidReceive(_ response: UNNotificationResponse?)
```

Метод необходимо вызывать в вашей реализации [userNotificationCenter(_:didReceive:withCompletionHandler:)](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/1649501-usernotificationcenter?language=swift).

**Параметры:**

#|
|| `notification` | Объект класса [UNNotificationResponse](https://developer.apple.com/documentation/usernotifications/unnotificationresponse). ||
|#

### userNotificationCenterOpenSettings(_:) {#method_userNotificationCenterOpenSettingsForNotification}

```swift translate=no
func userNotificationCenterOpenSettings(for notification: UNNotification?)
```

Метод необходимо вызывать в вашей реализации [userNotificationCenter(_:openSettingsFor:)](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/2981869-usernotificationcenter?language=swift).

**Параметры:**

#|
|| `notification` | Объект класса [UNNotification](https://developer.apple.com/documentation/usernotifications/unnotification). ||
|#
