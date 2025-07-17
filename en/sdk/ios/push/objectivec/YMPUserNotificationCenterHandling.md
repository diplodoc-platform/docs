# YMPUserNotificationCenterHandling protocol

A delegate for manual handling foreground push notifications on iOS 10 and higher.

Use this delegate if you implement the [UNUserNotificationCenterDelegate](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate?language=objc) protocol with custom logic. You should implement all methods of `UNUserNotificationCenterDelegate` and call proper methods in `YMPUserNotificationCenterHandling`.

The implementation of this delegate is called by the  `YMPYandexMetricaPush` [userNotificationCenterHandler](YMPYandexMetricaPush.md#method_userNotificationCenterHandler) method.

## Instance methods {#instance_summary}

#|
|| -[userNotificationCenterWillPresentNotification:](#method_userNotificationCenterWillPresentNotification) | You should call this method in your implementation of [userNotificationCenter:willPresentNotification:withCompletionHandler:](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/1649518-usernotificationcenter?language=objc). ||
|| -[userNotificationCenterDidReceiveNotificationResponse:](#method_userNotificationCenterDidReceiveNotificationResponse) | You should call this method in your implementation of [userNotificationCenter:didReceiveNotificationResponse:withCompletionHandler:](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/1649501-usernotificationcenter?language=objc). ||
|| -[userNotificationCenterOpenSettingsForNotification:](#method_userNotificationCenterOpenSettingsForNotification) | You should call this method in your implementation of [userNotificationCenter:openSettingsForNotification:](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/2981869-usernotificationcenter?language=objc). ||
|#

## Method descriptions {#method_detail}

### -userNotificationCenterWillPresentNotification: {#method_userNotificationCenterWillPresentNotification}

```objectivec translate=no
- (void)userNotificationCenterWillPresentNotification:(UNNotification *)notification
```

You should call this method in your implementation of [userNotificationCenter:willPresentNotification:withCompletionHandler:](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/1649518-usernotificationcenter?language=objc).

**Parameters:**

#|
|| `notification` | The instance of [UNNotification](https://developer.apple.com/documentation/usernotifications/unnotification). ||
|#

### -userNotificationCenterDidReceiveNotificationResponse: {#method_userNotificationCenterDidReceiveNotificationResponse}

```objectivec translate=no
- (void)userNotificationCenterDidReceiveNotificationResponse:(UNNotificationResponse *)response;
```

You should call this method in your implementation of [userNotificationCenter:didReceiveNotificationResponse:withCompletionHandler:](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/1649501-usernotificationcenter?language=objc).

**Parameters:**

#|
|| `notification` | The instance of [UNNotificationResponse](https://developer.apple.com/documentation/usernotifications/unnotificationresponse). ||
|#

### -userNotificationCenterOpenSettingsForNotification: {#method_userNotificationCenterOpenSettingsForNotification}

```objectivec translate=no
- (void)userNotificationCenterOpenSettingsForNotification:(nullable UNNotification *)notification API_AVAILABLE(ios(12.0));
```

You should call this method in your implementation of [userNotificationCenter:openSettingsForNotification:](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/2981869-usernotificationcenter?language=objc).

**Parameters:**

#|
|| `notification` | The instance of [UNNotification](https://developer.apple.com/documentation/usernotifications/unnotification). ||
|#
