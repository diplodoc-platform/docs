# AppMetricaPush class

The main class for push notifications handling.

## Instance methods

#|
|| +[downloadAttachmentsForNotificationRequest:](#method_downloadAttachmentsForNotificationRequest) | Uploads attached files in push notifications. The method is available for iOS 10.0 and higher. ||
|| +[handleApplicationDidFinishLaunchingWithOptions:](#method_handleApplicationDidFinishLaunchingWithOptions) | Handles push notification openings from the method [application(_:didFinishLaunchingWithOptions:)](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622921-application?language=swift). ||
|| +[handleDidReceiveNotificationRequest:](#method_handleDidReceiveNotificationRequest) | Handles push notifications receiving from Notification Service Extension. ||
|| +[handleRemoteNotification:](#method_handleRemoteNotification) | Handles push notification openings from the method [application(_:didReceiveRemoteNotification:fetchCompletionHandler:)](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1623013-application?language=swift). ||
|| +[handleSceneWillConnectToSession:](#method_handleSceneWillConnectToSession) | Handles push notification openings from the method [scene(_:willConnectTo:options:)](https://developer.apple.com/documentation/uikit/uiscenedelegate/3197914-scene). ||
|| +[isNotificationRelatedToSDK:](#method_isNotificationRelatedToSDK) | Returns `YES` if a push notification is related to AppMetrica. ||
|| +[setDeviceTokenFromData:](#method_setDeviceTokenFromData) | Registers the device token for an application with a production environment. ||
|| +[setDeviceTokenFromData:pushEnvironment:](#method_setDeviceTokenFromData_pushEnvironment) | Registers the device token of the application with the specified environment. ||
|| +[setExtensionAppGroup:](#method_setExtensionAppGroup) | Registers the App Groups shared group for the app and Notification Service Extension. ||
|| +[userDataForNotification:](#method_userDataForNotification) | Returns an arbitrary data string that is passed in the push notification. ||
|#

## Properties {#property_summary}

#|
|| [userNotificationCenterDelegate](#property_userNotificationCenterDelegate) | Returns a delegate [UserNotificationCenterDelegate](UserNotificationCenterDelegate.md) which handles foreground push notifications in iOS 10 and higher. ||
|| [userNotificationCenterHandler](#property_userNotificationCenterHandler) | Returns a delegate [UserNotificationCenterHandling](UserNotificationCenterHandling.md) to manually handle foreground push notifications in iOS 10 and higher. ||
|#

## Method descriptions

### downloadAttachmentsForNotificationRequest: {#method_downloadAttachmentsForNotificationRequest}

```swift translate=no
class func downloadAttachments(request: UNNotificationRequest, callback: AttachmentsDownloadCallback)
```

Uploads attached files in push notifications. The method is available for iOS 10.0 and higher.

**Parameters:**

#|
|| `request` | The instance of [UNNotificationRequest](https://developer.apple.com/documentation/usernotifications/unnotificationrequest). ||
|| `callback` | The callback block for uploading notification contents. Format:
```swift translate=no
public typealias AttachmentsDownloadCallback = ([UNNotificationAttachment]?, Error?) -> Void`
```
Includes an array of `attachments` and an `error` if an error occurs when uploading files. ||
|#

### handleApplicationDidFinishLaunching(withOptions:) {#method_handleApplicationDidFinishLaunchingWithOptions}

```swift translate=no
class func handleApplicationDidFinishLaunching(withOptions launchOptions: [AnyHashable : Any]?)
```

Handles push notification openings from the method [application (_: didFinishLaunchingWithOptions:)](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622921-application?language=swift). Method should be invoked after AppMetrica SDK initialization.

**Parameters:**

#|
|| `launchOptions` | Parameters as «key-value» pairs that contain information about the application start. ||
|#

### handleDidReceive(_:) {#method_handleDidReceiveNotificationRequest}

```swift translate=no
class func handleDidReceive(_ request: UNNotificationRequest?)
```

Handles push notifications receiving from Notification Service Extension.

You should call the method in the implementation of [didReceive (_: withContentHandler:)](https://developer.apple.com/documentation/usernotifications/unnotificationserviceextension/1648229-didreceive).

**Parameters:**

#|
|| `request` | The instance of [UNNotificationRequest](https://developer.apple.com/documentation/usernotifications/unnotificationrequest?language=swift). ||
|#

### handleRemoteNotification(_:) {#method_handleRemoteNotification}

```swift translate=no
class func handleRemoteNotification(_ userInfo: [AnyHashable : Any]?)
```

Handles push notification openings from the method [application(_:didReceiveRemoteNotification:fetchCompletionHandler:)](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1623013-application?language=swift) Method should be invoked after AppMetrica SDK initialization.

**Parameters:**

#|
|| `userInfo` | Parameters of push notifications as «key-value» pairs that are transmitted by the system. ||
|#

### handleSceneWillConnectToSession(with: connectionOptions) {#method_handleSceneWillConnectToSession}

```swift translate=no
class func handleSceneWillConnectToSession(with: connectionOptions)
```

Handles push notification openings from the method [scene(_:willConnectTo:options:)](https://developer.apple.com/documentation/uikit/uiscenedelegate/3197914-scene). Method should be invoked after AppMetrica SDK initialization.

**Parameters:**

#|
|| `connectionOptions` | The [UIScene.ConnectionOptions](https://developer.apple.com/documentation/uikit/uiscene/connectionoptions) class object with connection parameters that are transmitted by the system. ||
|#

### isNotificationRelated(toSDK:) {#method_isNotificationRelatedToSDK}

```swift translate=no
class func isNotificationRelated(toSDK userInfo: [AnyHashable : Any]?) -> Bool
```

Returns `YES` if a push notification is related to AppMetrica.

**Parameters:**

#|
|| `userInfo` | Parameters of push notifications as «key-value» pairs that are transmitted by the system. ||
|#

**Returns:**

- `YES` — If the push notification refers to AppMetrica.
- `NO` — If the push notification is not related to AppMetrica.

### setDeviceTokenFrom(_:) {#method_setDeviceTokenFromData}

```swift translate=no
class func setDeviceTokenFrom(_ data: Data?)
```

Registers the device token for an application with a production environment. Method should be invoked after AppMetrica SDK initialization.

**Parameters:**

#|
|| `data` | Device token of the application.

If you pass the `nil` value, the previous device token is revoked. ||
|#

### setDeviceTokenFrom(_:pushEnvironment:) {#method_setDeviceTokenFromData_pushEnvironment}

```swift translate=no
class func setDeviceTokenFrom(_ data: Data?, pushEnvironment: AppMetricaPushEnvironment)
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

### setExtensionAppGroup(_:) {#method_setExtensionAppGroup}

```swift translate=no
class func setExtensionAppGroup(_ appGroup: String?)
```

Registers the App Groups shared group for the app and Notification Service Extension.

Registration is necessary for tracking the delivery of push notifications. For more information, see [Configuring statistics collection for push notifications](../ios-settings.md).

**Parameters:**

#|
|| `appGroup` | The name of the shared App Groups group. ||
|#

### userData(forNotification:) {#method_userDataForNotification}

```swift translate=no
class func userData(forNotification userInfo: [AnyHashable : Any]?) -> String?
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

## Property descriptions {#property_detail}

### userNotificationCenterDelegate {#property_userNotificationCenterDelegate}

```swift translate=no
var userNotificationCenterDelegate: UserNotificationCenterDelegate? { get }
```

Returns a delegate [UserNotificationCenterDelegate](UserNotificationCenterDelegate.md) which handles foreground push notifications in iOS 10 and higher.

To handle foreground push notifications, add this code to the [application(_:didFinishLaunchingWithOptions:)](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622921-application?language=swift) method:

```swift translate=no
let delegate = AppMetricaPush.userNotificationCenterDelegate
UNUserNotificationCenter.current().delegate = delegate
```

To manually handle push notifications, use [userNotificationCenterHandler](#property_userNotificationCenterHandler).

### userNotificationCenterHandler {#property_userNotificationCenterHandler}

```swift translate=no
var userNotificationCenterHandler: UserNotificationCenterHandling? { get }
```

Returns a delegate [UserNotificationCenterHandling](UserNotificationCenterHandling.md) which allows you to manually handle foreground push notifications in iOS 10 and higher.

Use this delegate if you implement the [UNUserNotificationCenterDelegate](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate?language=objc) protocol with custom logic. In this case, you should implement all methods of the `UNUserNotificationCenterDelegate` delegate and call the corresponding methods in `UserNotificationCenterHandling`.

For simplified push notification handling, use [userNotificationCenterDelegate](#property_userNotificationCenterDelegate).
