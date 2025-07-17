# YMPUserNotificationCenterDelegate protocol

A delegate for handling foreground push notifications on iOS 10 and higher.

To handle foreground push notifications, add this code to the [application: didFinishLaunchingWithOptions:](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622921-application?language=objc) method:

```objectivec translate=no
[UNUserNotificationCenter currentNotificationCenter].delegate = [YMPYandexMetricaPush userNotificationCenterDelegate];
```

## Properties {#property_summary}

#|
|| [presentationOptions](#property_presentationOptions) | {{ presentationOptions }} ||
|| [nextDelegate](#property_nextDelegate) | {{ nextDelegate }} ||
|#

## Property descriptions {#property_detail}

### presentationOptions {#property_presentationOptions}

```objectivec translate=no
(nonatomic, assign) [UNNotificationPresentationOptions](https://developer.apple.com/documentation/usernotifications/unnotificationpresentationoptions) presentationOptions
```

Parameters for displaying push notifications. They are passed to the handler [userNotificationCenter: willPresentNotification: withCompletionHandler:](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/1649518-usernotificationcenter?language=objc).

The delegate invokes the handler if the `nextDelegate` property is not set or if the object is in `nextDelegate` does not respond to the selector.

### nextDelegate {#property_nextDelegate}

```objectivec translate=no
(nonatomic, weak, nullable) id<UNUserNotificationCenterDelegate> nextDelegate;
```

A delegate to which calls of this protocol will be proxied.
