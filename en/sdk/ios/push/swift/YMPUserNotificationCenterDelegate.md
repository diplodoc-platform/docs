# YMPUserNotificationCenterDelegate protocol

A delegate for handling foreground push notifications on iOS 10 and higher.

To handle foreground push notifications, add this code to the [application(_:didFinishLaunchingWithOptions:)](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622921-application?language=swift) method:

```swift translate=no
let delegate = YMPYandexMetricaPush.userNotificationCenterDelegate()
UNUserNotificationCenter.current().delegate = delegate
```

## Properties {#property_summary}

#|
|| [presentationOptions](#property_presentationOptions) | {{ presentationOptions }} ||
|| [nextDelegate](#property_nextDelegate) | {{ nextDelegate }} ||
|#

## Property descriptions {#property_detail}

### presentationOptions {#property_presentationOptions}

```swift translate=no
var presentationOptions: UNNotificationPresentationOptions
```

Parameters for displaying push notifications. They are passed to the handler [userNotificationCenter(_:willPresent:withCompletionHandler:)](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/1649518-usernotificationcenter?language=swift).

The delegate invokes the handler if the `nextDelegate` property is not set or if the object is in `nextDelegate` does not respond to the selector.

### nextDelegate {#property_nextDelegate}

```swift translate=no
var nextDelegate: id<UNUserNotificationCenterDelegate>
```

{{ nextDelegate }}
