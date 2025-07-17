# AMAAppMetricaReporting protocol

## Instance methods {#instance_summary}

#|
|| -[clearAppEnvironment](#method_clearAppEnvironment) | Deleting all key-value data associated with all future events. ||
|| -[pauseSession](#method_pauseSession) | Pauses the session. ||
|| -[reportAdRevenue:onFailure:](#method_reportAdRevenue__onFailure) | Sends information about advertising revenue to the AppMetrica server. ||
|| -[reportECommerce:onFailure](#method_reportECommerce__onFailure) | Sends a message about an E-commerce event. ||
|| -[reportEvent:onFailure](#method_reportEvent__onFailure) | Sends a custom event message. ||
|| -[reportEvent:parameters:onFailure](#method_reportEvent__parameters__onFailure) | Sends a custom event message with additional parameters. ||
|| -[reportRevenue:onFailure:](#method_reportRevenue__onFailure) | Sends information about the purchase to the AppMetrica server. ||
|| -[reportUserProfile:onFailure](#method_reportUserProfile__onFailure) | Sends information about a user profile update. ||
|| -[resumeSession](#method_resumeSession) | Resumes the session or creates a new one if the session timeout has expired. ||
|| -[sendEventsBuffer](#method_sendEventsBuffer) | Sends stored events from the buffer. ||
|| -[setAppEnvironmentValue:forKey:](#method_setAppEnvironmentValue__forKey) | Sets a key-value pair associated with all future events. ||
|| -[setDataSendingEnabled:](#method_setDataSendingEnabled) | Enables/disables sending statistics to the AppMetrica server. ||
|| -[setupWebViewReporting:onFailure:](#method_setupWebViewReporting__onFailure) | Adds a JavaScript interface with the AppMetrica name in a window to the specified webview. This lets you send client events from JavaScript code. ||
|#

## Properties {#property_summary}

#|
|| [userProfileID](#property_userProfileID) | Sets the ID of the [user profile](../../../../data-collection/about-profiles.md). ||
|#

## Method descriptions {#method_detail}

### -clearAppEnvironment {#method_clearAppEnvironment}

```objectivec translate=no
- (void)clearAppEnvironment;
```

Cleaning the app environment, such as deleting all key-value data associated with all future events.

### -pauseSession {#method_pauseSession}

```objectivec translate=no
- (void)pauseSession;
```

Pauses the user session.

### -reportAdRevenue:onFailure: {#method_reportAdRevenue__onFailure}

```objectivec translate=no
- (void)reportAdRevenue:(AMAAdRevenueInfo *)adRevenue
              onFailure:(nullable void (^)(NSError *error))onFailure;
```

Sends information about advertising revenue to the AppMetrica server.

**Parameters:**

#|
|| `adRevenue` | The instance of the [AMAAdRevenueInfo](AMAAdRevenueInfo.md) class which contains information about advertising revenue. ||
|| `onFailure` | The block that is executed when an error occurs. The error is passed as a block argument. ||
|#

### -reportECommerce:onFailure {#method_reportECommerce__onFailure}

```objectivec translate=no
- (void)reportECommerce:(AMAECommerce *)eCommerce
              onFailure:(nullable void (^)(NSError *error))onFailure;
```

Sends a message about an E-commerce event.

**Parameters:**

#|
|| `eCommerce` | The [AMAECommerce](AMAECommerce.md) class instance. ||
|| `onFailure` | The block that is executed when an error occurs. The error is passed as a block argument. ||
|#

### -reportEvent:onFailure {#method_reportEvent__onFailure}

```objectivec translate=no
- (void)reportEvent:(NSString *)name
          onFailure:(nullable void (^)(NSError *error))onFailure;
```

Sends a custom event message.

**Parameters:**

#|
|| `name` | Short name or description of the event. ||
|| `onFailure` | The block that is executed when an error occurs. The error is passed as a block argument. ||
|#

### -reportEvent:parameters:onFailure {#method_reportEvent__parameters__onFailure}

```objectivec translate=no
- (void)reportEvent:(NSString *)name
         parameters:(nullable NSDictionary *)params
          onFailure:(nullable void (^)(NSError *error))onFailure;
```

Sends a custom event message with additional parameters.

**Parameters:**

#|
|| `name` | Short name or description of the event. ||
|| `params` | Parameters as key-value pairs. ||
|| `onFailure` | The block that is executed when an error occurs. The error is passed as a block argument. ||
|#

### -reportRevenue:onFailure: {#method_reportRevenue__onFailure}

```objectivec translate=no
- (void)reportRevenue:(AMARevenueInfo *)revenueInfo
            onFailure:(nullable void (^)(NSError *error))onFailure;
```

Sends information about the purchase to the AppMetrica server.

**Parameters:**

#|
|| `revenueInfo` | The instance of the [AMARevenueInfo](AMARevenueInfo.md) class which contains information about a purchase. ||
|| `onFailure` | The block that is executed when an error occurs. The error is passed as a block argument. ||
|#

### -reportUserProfile:onFailure {#method_reportUserProfile__onFailure}

```objectivec translate=no
- (void)reportUserProfile:(AMAUserProfile *)userProfile
                onFailure:(nullable void (^)(NSError *error))onFailure;
```

Sends information about the user profile update to the AppMetrica server.

**Parameters:**

#|
|| `userProfile` | The instance of the [AMAUserProfile](AMAUserProfile.md) class which contains information about the user profile. ||
|| `onFailure` | The block that is executed when an error occurs. The error is passed as a block argument. ||
|#

### -resumeSession {#method_resumeSession}

```objectivec translate=no
- (void)resumeSession;
```

Resumes the session, or creates a new one if the session timeout has expired.

### -sendEventsBuffer {#method_sendEventsBuffer}

```objectivec translate=no
- (void)sendEventsBuffer;
```

Sends stored events from the buffer.

AppMetrica SDK does not send an event immediately after it occurred. The library stores event data in the buffer. The `+sendEventsBuffer` method sends data from the buffer and flushes it. Use the method to force sending stored events after passing important checkpoints of user scenarios.

{% note alert %}

Frequent use of the method can lead to increased outgoing internet traffic and energy consumption.

{% endnote %}

### -setAppEnvironmentValue:forKey: {#method_setAppEnvironmentValue__forKey}

```objectivec translate=no
- (void)setAppEnvironmentValue:(nullable NSString *)value
                        forKey:(NSString *)key;
```

Setting key-value data to be used as additional information associated with all future events.

If the value is zero, the previously set key value is deleted. Nothing is done if the key wasn't added.

**Parameters:**

#|
|| `value` | Value. ||
|| `key` | Key. ||
|#

### -setDataSendingEnabled: {#method_setDataSendingEnabled}

```objectivec translate=no
- (void)setDataSendingEnabled:(BOOL)enabled;
```

Enables/disables sending statistics to the AppMetrica server.

{% note info %}

Disable sending statistics to the reporter does not affect the sending of data from the main API key. But disabling data sending for the main API key stops sending statistics from all reporters.

{% endnote %}

**Parameters:**

#|
|| `enabled` | A flag indicating that sending statistics is enabled. The default value is `YES`.
Possible values:

- `YES`: Sending statistics is enabled.
- `NO`: Sending statistics is disabled. ||
   |#

### -setupWebViewReporting:onFailure: {#method_setupWebViewReporting__onFailure}

```objectivec translate=no
- (void)setupWebViewReporting:(id<AMAJSControlling>)controller
                    onFailure:(nullable void (^)(NSError *error))onFailure;
```

Adds a JavaScript interface with the AppMetrica name in a window to the specified webview. This lets you send client events from JavaScript code.

Notes:

- The method must be called from the main queue.
- The method is not available on tvOS.
- Call this method before loading any content. We recommend calling this method before creating a webview and before adding your scripts to WKUserContentController.
   For more information, see [Usage examples](../ios-operations.md#js-event).

**Parameters:**

#|
|| `controller` | The `AMAJSControlling` instance. ||
|| `onFailure` | A callback method to be called in the event of an error. ||
|#

## Property descriptions {#property_detail}

### userProfileID {#property_userProfileID}

```objectivec translate=no
@property (class, nonatomic, nullable) NSString *userProfileID;
```

Sets the ID of the [user profile](../../../../data-collection/about-profiles.md). AppMetrica doesn't display `predefined attributes` in the web interface if [ProfieId](../../../../data-collection/profile-attributes.md#pre-defined) sending isn't configured.
