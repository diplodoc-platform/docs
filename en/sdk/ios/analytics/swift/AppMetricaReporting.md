# AppMetricaReporting protocol

## Instance methods {#instance_summary}

#|
|| [clearAppEnvironment()](#method_clearAppEnvironment) | Deleting all key-value data associated with all future events. ||
|| [pauseSession()](#method_pauseSession) | Pauses the user session. ||
|| [reportAdRevenue(_:onFailure:)](#method_reportAdRevenue__onFailure) | Sends information about advertising revenue to the AppMetrica server. ||
|| [reportECommerce(_:onFailure)](#method_reportECommerce__onFailure) | Sends a message about an E-commerce event. ||
|| [reportEvent(name:onFailure)](#method_reportEvent__onFailure) | Sends an arbitrary event message. ||
|| [reportEvent(name:parameters:onFailure)](#method_reportEvent__parameters__onFailure) | Sends an arbitrary event message with additional parameters. ||
|| [reportRevenue(_:onFailure:)](#method_reportRevenue__onFailure) | Sends information about the purchase to the AppMetrica server. ||
|| [reportUserProfile(_:onFailure)](#method_reportUserProfile__onFailure) | Sends information about a user profile update. ||
|| [resumeSession()](#method_resumeSession) | Resumes the session, or creates a new one if the session timeout has expired. ||
|| [sendEventsBuffer()](#method_sendEventsBuffer) | Sends stored events from the buffer. ||
|| [setAppEnvironment(_:forKey:)](#method_setAppEnvironmentValue__forKey) | Sets a key-value pair associated with all future events. ||
|| [setDataSendingEnabled(_:)](#method_setDataSendingEnabled) | Enables/disables sending statistics to the AppMetrica server. ||
|| [setupWebViewReporting(with:onFailure:)](#method_setupWebViewReporting__onFailure) | Adds a JavaScript interface with the AppMetrica name in a window to the specified WebView. This lets you send client events from JavaScript code. ||
|#

## Properties {#property_summary}

#|
|| [userProfileID](#property_userProfileID) | Sets the ID of the [user profile](../../../../data-collection/about-profiles.md). ||
|#

## Method descriptions {#method_detail}

### clearAppEnvironment() {#method_clearAppEnvironment}

```swift translate=no
func clearAppEnvironment()
```

Cleaning the app environment, such as deleting all key-value data associated with all future events.

### pauseSession() {#method_pauseSession}

```swift translate=no
func pauseSession()
```

Pauses the user session.

### reportAdRevenue(_:onFailure) {#method_reportAdRevenue__onFailure}

```swift translate=no
func reportAdRevenue(_ adRevenue: AdRevenueInfo, onFailure: ((Error) -> Void)?)
```

Sends information about advertising revenue to the AppMetrica server.

**Parameters:**

#|
|| `adRevenue` | The instance of the [AdRevenueInfo](AdRevenueInfo.md) class which contains information about advertising revenue. ||
|| `onFailure` | The block that is executed when an error occurs. The error is passed as a block argument. ||
|#

### reportECommerce(_:onFailure) {#method_reportECommerce__onFailure}

```swift translate=no
func reportECommerce(_ eCommerce: ECommerce, onFailure: ((Error) -> Void)?)
```

Sends a message about an E-commerce event.

**Parameters:**

#|
|| `eCommerce` | The [ECommerce](ECommerce.md) class instance. ||
|| `onFailure` | The block that is executed when an error occurs. The error is passed as a block argument. ||
|#

### reportEvent(name:onFailure) {#method_reportEvent__onFailure}

```swift translate=no
func reportEvent(name: String, onFailure: ((Error) -> Void)?)
```

Sends a custom event message.

**Parameters:**

#|
|| `name` | Short name or description of the event. ||
|| `onFailure` | The block that is executed when an error occurs. The error is passed as a block argument. ||
|#

### reportEvent(name:parameters:onFailure) {#method_reportEvent__parameters__onFailure}

```swift translate=no
func reportEvent(name: String, parameters: [AnyHashable : Any]?, onFailure: ((Error) -> Void)?)
```

Sends a custom event message with additional parameters.

**Parameters:**

#|
|| `name` | Short name or description of the event. ||
|| `parameters` | Parameters as key-value pairs. ||
|| `onFailure` | The block that is executed when an error occurs. The error is passed as a block argument. ||
|#

### reportRevenue(_:onFailure:) {#method_reportRevenue__onFailure}

```swift translate=no
func reportRevenue(_ revenueInfo: RevenueInfo, onFailure: ((Error) -> Void)?)
```

Sends information about the purchase to the AppMetrica server.

**Parameters:**

#|
|| `revenueInfo` | The instance of the [RevenueInfo](RevenueInfo.md) class which contains information about a purchase. ||
|| `onFailure` | The block that is executed when an error occurs. The error is passed as a block argument. ||
|#

### reportUserProfile(_:onFailure) {#method_reportUserProfile__onFailure}

```swift translate=no
func reportUserProfile(_ userProfile: UserProfile, onFailure: ((Error) -> Void)?)
```

Sends information about the user profile update to the AppMetrica server.

**Parameters:**

#|
|| `userProfile` | The instance of the [UserProfile](UserProfile.md) class which contains information about the user profile. ||
|| `onFailure` | The block that is executed when an error occurs. The error is passed as a block argument. ||
|#

### resumeSession() {#method_resumeSession}

```swift translate=no
func resumeSession()
```

Resumes the session, or creates a new one if the session timeout has expired.

### sendEventsBuffer() {#method_sendEventsBuffer}

```swift translate=no
func sendEventsBuffer()
```

Sends stored events from the buffer.

AppMetrica SDK does not send an event immediately after it occurred. The library stores event data in the buffer. The `+sendEventsBuffer` method sends data from the buffer and flushes it. Use the method to force sending stored events after passing important checkpoints of user scenarios.

{% note alert %}

Frequent use of the method can lead to increased outgoing internet traffic and energy consumption.

{% endnote %}

### setAppEnvironment(_:forKey:) {#method_setAppEnvironmentValue__forKey}

```swift translate=no
func setAppEnvironment(_ value: String?, forKey: String)
```

Setting key-value data to be used as additional information associated with all future events.

If the value is zero, the previously set key value is deleted. Nothing is done if the key wasn't added.

**Parameters:**

#|
|| `value` | Value. ||
|| `key` | Key. ||
|#

### setDataSendingEnabled(_:) {#method_setDataSendingEnabled}

```swift translate=no
func setDataSendingEnabled(_ enabled: Bool)
```

Enables/disables sending statistics to the AppMetrica server.

{% note info %}

Disable sending statistics to the reporter does not affect the sending of data from the main API key. But disabling data sending for the main API key stops sending statistics from all reporters.

{% endnote %}

**Parameters:**

#|
|| `enabled` | A flag indicating that sending statistics is enabled. The default value is `true`.
Possible values:

- `true`: Sending statistics is enabled.
- `false`: Sending statistics is disabled. ||
   |#

### setupWebViewReporting(with:onFailure:) {#method_setupWebViewReporting__onFailure}

```swift translate=no
class func setupWebViewReporting(with: JSControlling, onFailure: ((Error) -> Void)?)
```

Adds a JavaScript interface with the AppMetrica name in a window to the specified webview. This lets you send client events from JavaScript code.

Notes:

- The method must be called from the main queue.
- The method is not available on tvOS.
- Call this method before loading any content. We recommend calling this method before creating a webview and before adding your scripts to WKUserContentController.
   For more information, see [Usage examples](../ios-operations.md#js-event).

**Parameters:**

#|
|| `controller` | The `JSControlling` instance. ||
|| `onFailure` | A callback method to be called in the event of an error. ||
|#

## Property descriptions {#property_detail}

### userProfileID {#property_userProfileID}

```swift translate=no
var userProfileID: String { get; set; }
```

Sets the ID of the [user profile](../../../../data-collection/about-profiles.md). AppMetrica doesn't display `predefined attributes` in the web interface if [ProfieId](../../../../data-collection/profile-attributes.md#pre-defined) sending isn't configured.
