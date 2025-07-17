# YMPYandexMetricaPush class

The main class for push notifications handling.

## Instance methods

#|
|| +[downloadAttachmentsForNotificationRequest:](#method_downloadAttachmentsForNotificationRequest) | Uploads attached files in push notifications. The method is available for iOS 10.0 and higher. ||
|| +[handleApplicationDidFinishLaunchingWithOptions:](#method_handleApplicationDidFinishLaunchingWithOptions) | Handles push notification openings from the method [application:didFinishLaunchingWithOptions:](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622921-application?language=objc). ||
|| +[handleDidReceiveNotificationRequest:](#method_handleDidReceiveNotificationRequest) | Handles push notifications receiving from Notification Service Extension. ||
|| +[handleRemoteNotification:](#method_handleRemoteNotification) | Handles push notification openings from the method [application:didReceiveRemoteNotification:fetchCompletionHandler:](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1623013-application?language=objc). ||
|| +[handleSceneWillConnectToSession:](#method_handleSceneWillConnectToSession) | Handles opening push notifications from the method [scene:willConnectToSession:options:](https://developer.apple.com/documentation/uikit/uiscenedelegate/3197914-scene?language=objc). ||
|| +[isNotificationRelatedToSDK:](#method_isNotificationRelatedToSDK) | Returns `YES` if a push notification is related to AppMetrica. ||
|| +[setDeviceTokenFromData:](#method_setDeviceTokenFromData) | Registers the device token for an application with a production environment. ||
|| +[setDeviceTokenFromData:pushEnvironment:](#method_setDeviceTokenFromData_pushEnvironment) | Registers the device token of the application with the specified environment. ||
|| +[setExtensionAppGroup:](#method_setExtensionAppGroup) | Registers the App Groups shared group for the app and Notification Service Extension. ||
|| +[userDataForNotification:](#method_userDataForNotification) | Returns an arbitrary data string that is passed in the push notification. ||
|| +[userNotificationCenterDelegate:](#method_userNotificationCenterDelegate) | Returns a delegate [YMPUserNotificationCenterDelegate](YMPUserNotificationCenterDelegate.md), which handles foreground push notifications on iOS 10 and higher. ||
|| +[userNotificationCenterHandler:](#method_userNotificationCenterHandler) | Returns a delegate [YMPUserNotificationCenterHandling](YMPUserNotificationCenterHandling.md), which allows you to manually handle foreground push notifications on iOS 10 and higher. ||
|#

## Method descriptions {#method_detail}

### +downloadAttachmentsForNotificationRequest: {#method_downloadAttachmentsForNotificationRequest}

```objectivec translate=no
+ (void)downloadAttachmentsForNotificationRequest:(UNNotificationRequest *)request
                                         callback:(YMPAttachmentsDownloadCallback)callback);
```

Uploads attached files in push notifications. The method is available for iOS 10.0 and higher.

**Parameters:**

#|
|| `request` | The instance of [UNNotificationRequest](https://developer.apple.com/documentation/usernotifications/unnotificationrequest). ||
|| `callback` | The callback block for uploading attached files. Format:

```objectivec translate=no
typedef void (^YMPAttachmentsDownloadCallback) (NSArray<UNNotificationAttachment *> * _Nullable attachments, NSError * _Nullable error)
```
Includes an array of `attachments` and an `error` if an error occurs when uploading files. ||
|#

### +handleApplicationDidFinishLaunchingWithOptions: {#method_handleApplicationDidFinishLaunchingWithOptions}

```objectivec translate=no
+ (void)handleApplicationDidFinishLaunchingWithOptions:(nullable NSDictionary *)launchOptions
```

Handles push notification openings from the method [application:didFinishLaunchingWithOptions:](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622921-application?language=objc). Method should be invoked after AppMetrica SDK initialization.

**Parameters:**

#|
|| `launchOptions` | Parameters as «key-value» pairs that contain information about the application start. ||
|#

### +handleDidReceiveNotificationRequest: {#method_handleDidReceiveNotificationRequest}

```objectivec translate=no
+ (void)handleDidReceiveNotificationRequest:(UNNotificationRequest *)request
```

Handles push notifications receiving from Notification Service Extension.

You should call the method in the implementation of  [didReceiveNotificationRequest:withContentHandler:](https://developer.apple.com/documentation/usernotifications/unnotificationserviceextension/1648229-didreceivenotificationrequest).

**Parameters:**

#|
|| `request` | The instance of [UNNotificationRequest](https://developer.apple.com/documentation/usernotifications/unnotificationrequest?language=objc). ||
|#

### +handleRemoteNotification: {#method_handleRemoteNotification}

```objectivec translate=no
+ (void)handleRemoteNotification:(NSDictionary *)userInfo
```

Handles push notification openings from the method [application:didReceiveRemoteNotification:fetchCompletionHandler](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1623013-application?language=objc). Method should be invoked after AppMetrica SDK initialization.

**Parameters:**

#|
|| `userInfo` | Parameters of push notifications as «key-value» pairs that are transmitted by the system. ||
|#

### +handleSceneWillConnectToSession: {#method_handleSceneWillConnectToSession}

```objectivec translate=no
+ (void)handleSceneWillConnectToSessionWithOptions:(UISceneConnectionOptions *)connectionOptions
```

Handles opening push notifications from the method [scene:willConnectToSession:options:](https://developer.apple.com/documentation/uikit/uiscenedelegate/3197914-scene?language=objc). Method should be invoked after AppMetrica SDK initialization.

**Parameters:**

#|
|| `connectionOptions` | The [UISceneConnectionOptions](https://developer.apple.com/documentation/uikit/uisceneconnectionoptions?language=objc) class object with connection parameters that are transmitted by the system. ||
|#

### +isNotificationRelatedToSDK: {#method_isNotificationRelatedToSDK}

```objectivec translate=no
+ (BOOL)isNotificationRelatedToSDK:(NSDictionary *)userInfo;
```

Returns `YES` if a push notification is related to AppMetrica.

**Parameters:**

#|
|| `userInfo` | Parameters of push notifications as «key-value» pairs that are transmitted by the system. ||
|#

**Returns:**

- `YES` — If the push notification refers to AppMetrica.
- `NO` — If the push notification is not related to AppMetrica.

### +setDeviceTokenFromData: {#method_setDeviceTokenFromData}

```objectivec translate=no
+ (void)setDeviceTokenFromData:(nullable NSData *)data
```

Registers the device token for an application with a production environment. Method should be invoked after AppMetrica SDK initialization.

**Parameters:**

#|
|| `data` | Device token of the application.

If you pass the `nil` value, the previous device token is revoked. ||
|#

### +setDeviceTokenFromData:pushEnvironment: {#method_setDeviceTokenFromData_pushEnvironment}

```objectivec translate=no
+ (void)setDeviceTokenFromData:(nullable NSData *)data
               pushEnvironment:(YMPYandexMetricaPushEnvironment)pushEnvironment
```

Registers the device token of the application with the specified environment. Method should be invoked after AppMetrica SDK initialization.

{% note alert %}

AppMetrica allows you to send push notifications to Sandbox APNs. However, push notification processing may not work correctly if versions of the application with different environments were run on the device(_development_ and _production_). To avoid this issue, you can use a separate test API key for _development_ environment.

{% endnote %}

**Parameters:**

#|
|| `data` | Device token of the application.

If you pass the `nil` value, the previous device token is revoked. ||
|| `pushEnvironment` | APNs app environment. ||
|#

### +setExtensionAppGroup: {#method_setExtensionAppGroup}

```objectivec translate=no
+ (void)setExtensionAppGroup:(NSString *)appGroup
```

Registers the App Groups shared group for the app and Notification Service Extension.

Registration is necessary for tracking the delivery of push notifications. For more information, see [Configuring statistics collection for push notifications](../ios-settings.md).

**Parameters:**

#|
|| `appGroup` | The name of the shared App Groups group. ||
|#

### +userDataForNotification: {#method_userDataForNotification}

```objectivec translate=no
+ (nullable NSString *)userDataForNotification:(NSDictionary *)userInfo
```

Returns an arbitrary data string that is passed in the push notification:

- In the **Additional data** field when sending from the AppMetrica interface.
- In the `data` field when sending using the [Push API](../../../../mobile-api/push/about.md).

**Parameters:**

#|
|| `userInfo` | Parameters of push notifications as «key-value» pairs that are transmitted by the system. ||
|#

**Returns:**

An arbitrary data string.

### +userNotificationCenterDelegate {#method_userNotificationCenterDelegate}

```objectivec translate=no
+ (id<YMPUserNotificationCenterDelegate>)userNotificationCenterDelegate
```

Returns a delegate [YMPUserNotificationCenterDelegate](YMPUserNotificationCenterDelegate.md), which handles foreground push notifications on iOS 10 and higher.

To handle foreground push notifications, add this code to the [application: didFinishLaunchingWithOptions:](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622921-application?language=objc) method:

```objectivec translate=no
[UNUserNotificationCenter currentNotificationCenter].delegate = [YMPYandexMetricaPush userNotificationCenterDelegate];
```

For manual handling of push notifications, use [+userNotificationCenterHandler](#method_userNotificationCenterHandler).

**Returns:**

A delegate that implements the [YMPUserNotificationCenterDelegate](YMPUserNotificationCenterDelegate.md) protocol.

### +userNotificationCenterHandler {#method_userNotificationCenterHandler}

```objectivec translate=no
+ (id<YMPUserNotificationCenterHandling>)userNotificationCenterHandler
```

Returns a delegate [YMPUserNotificationCenterHandling](YMPUserNotificationCenterHandling.md), which allows you to manually handle foreground push notifications on iOS 10 and higher.

Use this delegate if you implement the [UNUserNotificationCenterDelegate](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate?language=objc) protocol with custom logic. In this case, you should implement all methods of the `UNUserNotificationCenterDelegate` delegate and call the corresponding methods in `YMPUserNotificationCenterHandling`.

For simplified push notification handling, use [+userNotificationCenterDelegate](#method_userNotificationCenterDelegate).

**Returns:**

A delegate that implements the `YMPUserNotificationCenterHandling` protocol.
