# YMPUserNotificationCenterHandling protocol

A delegate for manual handling foreground push notifications on iOS 10 and higher.

Use this delegate if you implement the [UNUserNotificationCenterDelegate](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate?language=swift) protocol with custom logic. You should implement all methods of `UNUserNotificationCenterDelegate` and call proper methods in `YMPUserNotificationCenterHandling`.

The implementation of this delegate is called by the `YMPYandexMetricaPush` [userNotificationCenterDelegate](YMPYandexMetricaPush.md#method_userNotificationCenterHandler) method.

## Instance methods {#instance_summary}

#|
|| [userNotificationCenterWillPresent(_:)](#method_userNotificationCenterWillPresentNotification) | You should call this method in your implementation of [userNotificationCenter(_:willPresent:withCompletionHandler:)](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/1649518-usernotificationcenter?language=swift). ||
|| [userNotificationCenterDidReceive(_:)](#method_userNotificationCenterDidReceiveNotificationResponse) | You should call this method in your implementation of [userNotificationCenter(_:didReceive:withCompletionHandler:)](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/1649501-usernotificationcenter?language=swift). ||
|| [userNotificationCenterOpenSettings(_:)](#method_userNotificationCenterOpenSettingsForNotification) | You should call this method in your implementation of [userNotificationCenter(_:openSettingsFor:)](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/2981869-usernotificationcenter?language=swift). ||
|#

## Method descriptions {#method_detail}

### userNotificationCenterWillPresent(_:) {#method_userNotificationCenterWillPresentNotification}

```swift translate=no
func userNotificationCenterWillPresent(_ notification: UNNotification?)
```

You should call this method in your implementation of [userNotificationCenter (_: willPresent:withCompletionHandler:)](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/1649518-usernotificationcenter?language=swift).

**Parameters:**

#|
|| `notification` | The instance of [UNNotification](https://developer.apple.com/documentation/usernotifications/unnotification?language=swift). ||
|#

### userNotificationCenterDidReceive(_:) {#method_userNotificationCenterDidReceiveNotificationResponse}

```swift translate=no
func userNotificationCenterDidReceive(_ response: UNNotificationResponse?)
```

You should call this method in your implementation of [userNotificationCenter (_: didReceive:withCompletionHandler:)](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/1649501-usernotificationcenter?language=swift).

**Parameters:**

#|
|| `notification` | The instance of [UNNotificationResponse](https://developer.apple.com/documentation/usernotifications/unnotificationresponse). ||
|#

### userNotificationCenterOpenSettings(_:) {#method_userNotificationCenterOpenSettingsForNotification}

```swift translate=no
func userNotificationCenterOpenSettings(for notification: UNNotification?)
```

You should call this method in your implementation of [userNotificationCenter (_: openSettingsFor:)](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/2981869-usernotificationcenter?language=swift).

**Parameters:**

#|
|| `notification` | The instance of [UNNotification](https://developer.apple.com/documentation/usernotifications/unnotification). ||
|#
