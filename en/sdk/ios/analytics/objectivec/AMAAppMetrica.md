# AMAAppMetrica class

Methods of the class are used for configuring the library.

## Instance methods {#instance_summary}

#|
|| +[activateReporterWithConfiguration:](#method_activateReporterWithConfiguration) | Initializes a reporter with the extended configuration. ||
|| +[activateWithConfiguration:](#method_activateWithConfiguration) | Initializes the library in an app with the [extended startup configuration](../ios-operations.md). ||
|| +[clearAppEnvironment](#method_clearAppEnvironment) | Deleting all key-value data associated with all future events. ||
|| +[pauseSession](#method_pauseSession) | Pauses the session. ||
|| +[reportAdRevenue:onFailure:](#method_reportAdRevenue__onFailure) | Sends information about advertising revenue to the AppMetrica server. ||
|| +[reportECommerce:onFailure:](#method_reportECommerce__onFailure) | Sends a message about an E-commerce event. ||
|| +[reportEvent:onFailure:](#method_reportEvent__onFailure) | Sends an [event message](../ios-operations.md#report-event). ||
|| +[reportEvent:parameters:onFailure:](#method_reportEvent__parameters__onFailure) | Sends an [event message with additional parameters](../ios-operations.md#report-event-params). ||
|| [+reportExternalAttribution:source:onFailure:](#method_reportExternalAttribution__source__onFailure) | Sends [external attribution](../../../../data-collection/attribution-integration.yaml) data to AppMetrica. ||
|| +[reportRevenue:onFailure:](#method_reportRevenue__onFailure) | Sends information about the purchase to the AppMetrica server. ||
|| +[reportUserProfile:onFailure:](#method_reportUserProfile__onFailure) | Sends information about a user profile update. ||
|| +[reporterForAPIKey:](#method_reporterForAPIKey) | Creates a reporter for [sending events to an additional API key](../ios-operations.md#reporter-different-apikey). ||
|| +[requestStartupIdentifiersWithCompletionQueue:completionBlock:](#method_requestStartupIdentifiersWithCompletionQueue__completionBlock) | Requests all predefined IDs. ||
|| +[requestStartupIdentifiersWithKeys:completionQueue:completionBlock:](#method_requestStartupIdentifiersWithKeys__completionQueue__completionBlock) | Requests IDs for specific keys. ||
|| +[resumeSession](#method_resumeSession) | Resumes the session or creates a new one if the session timeout has expired. ||
|| +[sendEventsBuffer](#method_sendEventsBuffer) | Sends stored events from the buffer. ||
|| +[setAppEnvironmentValue:forKey:](#method_setAppEnvironmentValue__forKey) | Sets a key-value pair associated with all future events. ||
|| +[setDataSendingEnabled:](#method_setDataSendingEnabled) | Enables/disables sending statistics to the AppMetrica server. ||
|| +[setupWebViewReporting:onFailure:](#method_setupWebViewReporting__onFailure) | Adds a JavaScript interface with the AppMetrica name in a window to the specified WebView. This lets you send client events from JavaScript code. ||
|| +[trackOpeningURL:](#method_trackOpeningURL) | Processes the URL that opened the app. ||
|#

## Properties {#property_summary}

#|
|| [UUID](#property_UUID) | The current UUID. ||
|| [accurateLocationTrackingEnabled](#property_accurateLocationTrackingEnabled) | Controls the accuracy of location tracking used by the internal location manager. ||
|| [activated](#property_activated) | Indicates whether AppMetrica was activated. ||
|| [allowsBackgroundLocationUpdates](#property_allowsBackgroundLocationUpdates) | Enable/disable background tracking of location updates. ||
|| [customLocation](#property_customLocation) | Sets [custom location of the device](../ios-operations.md#location-manual). ||
|| [deviceIDHash](#property_deviceIDHash) | The current appmetrica_device_id_hash. ||
|| [deviceID](#property_deviceID) | The current appmetrica_device_id. ||
|| [libraryVersion](#property_libraryVersion) | The current version of the AppMetrica library. ||
|| [locationTrackingEnabled](#property_locationTrackingEnabled) | Enables/disables [sending location of the device](../ios-operations.md#track-location). ||
|| [userProfileID](#property_userProfileID) | Sets the ID of the [user profile](../../../../data-collection/about-profiles.md). ||
|#

## Method descriptions {#method_detail}

### +activateReporterWithConfiguration: {#method_activateReporterWithConfiguration}

```objectivec translate=no
+ (void)activateReporterWithConfiguration:(AMAReporterConfiguration *)configuration;
```

Initializes a reporter with the extended configuration.

The configuration of the reporter should be initialized before the first call to the reporter. Otherwise, the configuration of the reporter is ignored.

The reporter should be activated with the configuration using a different API key instead of the app's API key.

**Parameters:**

#|
|| `configuration` | The instance of the [AMAReporterConfiguration](AMAReporterConfiguration.md) class which contains the extended configuration for the reporter. ||
|#

### +activateWithConfiguration: {#method_activateWithConfiguration}

```objectivec translate=no
+ (void)activateWithConfiguration:(AMAAppMetricaConfiguration *)configuration;
```

Initializes the library in an app with the [extended startup configuration](../ios-operations.md#initialize).

**Parameters:**

#|
|| `configuration` | The instance of the [AMAAppMetricaConfiguration](AMAAppMetricaConfiguration.md) class which contains the extended startup configuration for the library. ||
|#

### +clearAppEnvironment {#method_clearAppEnvironment}

```objectivec translate=no
+ (void)clearAppEnvironment;
```

Cleaning the app environment, such as deleting all key-value data associated with all future events.

### +pauseSession {#method_pauseSession}

```objectivec translate=no
+ (void)pauseSession;
```

Pauses the session.

{% note info %}

The session duration depends on the [specified timeout](AMAAppMetricaConfiguration.md#property_sessionTimeout). If the time interval between pausing and resuming the session is less than the specified timeout, the current session will be resumed; otherwise, a new one will be created.

For more information about sessions, see [Tracking user activity](../ios-listen.md).

{% endnote %}

### +reportAdRevenue:onFailure: {#method_reportAdRevenue__onFailure}

```objectivec translate=no
+ (void)reportAdRevenue:(AMAAdRevenueInfo *)adRevenue
              onFailure:(nullable void (^)(NSError *error))onFailure;
```

Sends information about advertising revenue to the AppMetrica server.

**Parameters:**

#|
|| `adRevenue` | The instance of the [AMAAdRevenueInfo](AMAAdRevenueInfo.md) class which contains information about advertising revenue. ||
|| `onFailure` | A callback method to be called in the event of an error. ||
|#

### +reportECommerce:onFailure: {#method_reportECommerce__onFailure}

```objectivec translate=no
+ (void)reportECommerce:(AMAECommerce *)eCommerce
              onFailure:(nullable void (^)(NSError *error))onFailure;
```

Sends a message about an E-commerce event.

**Parameters:**

#|
|| `eCommerce` | The [AMAECommerce](AMAECommerce.md) class instance. ||
|| `onFailure` | A callback method to be called in the event of an error. ||
|#

### +reportEvent:onFailure: {#method_reportEvent__onFailure}

```objectivec translate=no
+ (void)reportEvent:(NSString *)name
          onFailure:(nullable void (^)(NSError *error))onFailure;
```

Sends an [event message](../ios-operations.md#report-event).

**Parameters:**

#|
|| `name` | Short name or description of the event. ||
|| `onFailure` | The block that is executed when an error occurs. The error is passed as a block argument. ||
|#

### +reportEvent:parameters:onFailure: {#method_reportEvent__parameters__onFailure}

```objectivec translate=no
+ (void)reportEvent:(NSString *)name
         parameters:(nullable NSDictionary *)params
          onFailure:(nullable void (^)(NSError *error))onFailure;
```

Sends an [event message with additional parameters](../ios-operations.md#report-event-params).

**Parameters:**

#|
|| `name` | Short name or description of the event. ||
|| `params` | Parameters as <q>key-value</q> pairs. ||
|| `onFailure` | A callback method to be called in the event of an error. ||
|#

### +reportExternalAttribution:source:onFailure: {#method_reportExternalAttribution__source__onFailure}

```objectivec translate=no
+ (void)reportExternalAttribution:(NSDictionary *)attribution
                           source:(AMAAttributionSource)source
                        onFailure:(nullable void (^)(NSError *error))onFailure;
```

Sends [external attribution](../../../../data-collection/attribution-integration.yaml) data to AppMetrica.

**Parameters:**

#|
|| `attribution` | A dictionary with attribution data. It must be convertible to JSON, or else the method fails with the `onFailure` error block run. ||
|| `source` | The attribution data source. [Source list](AMAAttributionSource.md). ||
|| `onFailure` | A callback method to be called in the event of an error. The error is passed as an argument. ||
|#

### +reportRevenue:onFailure: {#method_reportRevenue__onFailure}

```objectivec translate=no
+ (void)reportRevenue:(AMARevenueInfo *)revenueInfo
            onFailure:(nullable void (^)(NSError *error))onFailure;
```

Sends information about the purchase to the AppMetrica server.

**Parameters:**

#|
|| `revenueInfo` | The instance of the [AMARevenueInfo](AMARevenueInfo.md) class which contains information about a purchase. ||
|| `onFailure` | A callback method to be called in the event of an error. ||
|#

### +reportUserProfile:onFailure: {#method_reportUserProfile__onFailure}

```objectivec translate=no
+ (void)reportUserProfile:(AMAUserProfile *)userProfile
                onFailure:(nullable void (^)(NSError *error))onFailure;
```

Sends information about a user profile update.

**Parameters:**

#|
|| `userProfile` | The instance of the [AMAUserProfile](AMAUserProfile.md) class which contains information about the user profile. ||
|| `onFailure` | A callback method to be called in the event of an error. ||
|#

### +reporterForAPIKey: {#method_reporterForAPIKey}

```objectivec translate=no
+ (nullable id<AMAAppMetricaReporting>)reporterForAPIKey:(NSString *)APIKey;
```

Creates a reporter for [sending events to an additional API key](../ios-operations.md#reporter-different-apikey).

To initialize a reporter with the extended configuration, use the [activateReporterWithConfiguration:](#method_activateReporterWithConfiguration) method. The configuration of the reporter should be initialized before the first call to the reporter. Otherwise, the configuration of the reporter is ignored.

**Parameters:**

#|
|| `APIKey` | An API key that differs from the app's API key. ||
|#

**Returns:**

The instance that implements the [AMAAppMetricaReporting](AMAAppMetricaReporting.md) protocol for the specified API key.

### +requestStartupIdentifiersWithCompletionQueue:completionBlock: {#method_requestStartupIdentifiersWithCompletionQueue__completionBlock}

```objectivec translate=no
+ (void)requestStartupIdentifiersWithCompletionQueue:(nullable dispatch_queue_t)queue
                                     completionBlock:(AMAIdentifiersCompletionBlock)block;
```

Getting all predefined IDs

**Parameters:**

#|
|| `queue` | Queue for sending a block. If the value is zero, the main queue is used. ||
|| `block` | The block will be sent when available IDs appear or in case of an error.

Predefined IDs are:
- `kAMAUUIDKey`
- `kAMADeviceIDKey`
- `kAMADeviceIDHashKey`

If they are available at the time of calling, the block is sent immediately. See the `AMAIdentifiersCompletionBlock` definition for more information about the returned types.

||
|#

### +requestStartupIdentifiersWithKeys:completionQueue:completionBlock: {#requestStartupIdentifiersWithKeys__completionQueue__completionBlock}

```objectivec translate=no
+ (void)requestStartupIdentifiersWithKeys:(NSArray<AMAStartupKey> *)keys
                          completionQueue:(nullable dispatch_queue_t)queue
                          completionBlock:(AMAIdentifiersCompletionBlock)block;
```

Getting IDs for specific keys

**Parameters:**

#|
|| `keys` | An array of identification keys for the query. See `AMAStartupKey`. ||
|| `queue` | Queue for sending a block. If the value is zero, the main queue is used. ||
|| `block` | The block will be sent when available IDs appear or in case of an error.

If they are available at the time of calling, the block is sent immediately. See the `AMAIdentifiersCompletionBlock` definition for more information about the returned types.

||
|#

### +resumeSession {#method_resumeSession}

```objectivec translate=no
+ (void)resumeSession;
```

Resumes the session, or creates a new one if the session timeout has expired.

{% note info %}

The session duration depends on the [specified timeout](AMAAppMetricaConfiguration.md#property_sessionTimeout). If the time interval between pausing and resuming the session is less than the specified timeout, the current session will be resumed; otherwise, a new one will be created.

For more information about sessions, see [Tracking user activity](../ios-listen.md).

{% endnote %}

### +sendEventsBuffer {#method_sendEventsBuffer}

```objectivec translate=no
+ (void)sendEventsBuffer;
```

Sends stored events from the buffer.

AppMetrica SDK does not send an event immediately after it occurred. The library stores event data in the buffer. The `+sendEventsBuffer` method sends data from the buffer and flushes it. Use the method to force sending stored events after passing important checkpoints of user scenarios.

{% note alert %}

Frequent use of the method can lead to increased outgoing internet traffic and energy consumption.

{% endnote %}

### +setAppEnvironmentValue:forKey: {#method_setAppEnvironmentValue__forKey}

```objectivec translate=no
+ (void)setAppEnvironmentValue:(nullable NSString *)value
                        forKey:(NSString *)key;
```

Setting key-value data to be used as additional information associated with all future events.

If the value is zero, the previously set key value is deleted. Nothing is done if the key wasn't added.

**Parameters:**

#|
|| `value` | Value. ||
|| `key` | Key. ||
|#

### +setDataSendingEnabled: {#method_setDataSendingEnabled}

```objectivec translate=no
+ (void)setDataSendingEnabled:(BOOL)enabled;
```

Enables/disables sending statistics to the AppMetrica server.

For more information about using the method, see [Disabling and enabling sending statistics](../ios-operations.md#stat).

{% note info %}

Disabling sending also turns off sending data from all reporters that initialized with the other API key.

{% endnote %}

**Parameters:**

#|
|| `enabled` | A flag indicating that sending statistics is enabled. The default value is `YES`.

Possible values:

- `YES`: Sending statistics is enabled.
- `NO`: Sending statistics is disabled. ||
   |#

### +setupWebViewReporting:onFailure: {#method_setupWebViewReporting__onFailure}

```objectivec translate=no
+ (void)setupWebViewReporting:(id<AMAJSControlling>)controller
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

### +trackOpeningURL: {#method_trackOpeningURL}

```objectivec translate=no
+ (void)trackOpeningURL:(NSURL *)URL;
```

Processes the URL that opened the app.

Used for [tracking app openings via deeplink](../ios-operations.md#deeplink).

**Parameters:**

#|
|| `URL` | URL that opened the app. ||
|#

## Property descriptions {#property_detail}

### uuid {#property_UUID}

```objectivec translate=no
@property (class, nonatomic, readonly) NSString *UUID;
```

Retrieves the current UUID.

### accurateLocationTrackingEnabled {#property_accurateLocationTrackingEnabled}

```objectivec translate=no
@property (class, nonatomic, getter=isAccurateLocationTrackingEnabled) BOOL accurateLocationTrackingEnabled;
```

Controls the accuracy of location tracking used by the internal location manager.

If set to `YES`, the location manager attempts to use the most accurate location data available.
This property takes effect only if the `isLocationTrackingEnabled` parameter is set to `YES`, and the location
wasn't set manually using the `customLocation` property.

### activated {#property_activated}

```objectivec translate=no
@property (class, assign, readonly, getter=isActivated) BOOL activated;
```

Indicates whether AppMetrica was activated.

{% note info %}

Use this property to check whether AppMetrica has already been activated, typically to avoid redundant activation calls or to make sure that statistics collection is running.

{% endnote %}

### allowsBackgroundLocationUpdates {#property_allowsBackgroundLocationUpdates}

```objectivec translate=no
@property (class, nonatomic) BOOL allowsBackgroundLocationUpdates;
```

Enable/disable background tracking of location updates. Disabled by default.

### customLocation {#property_customLocation}

```objectivec translate=no
@property (class, nonatomic, nullable) CLLocation *customLocation;
```

Sets [custom location of the device](../ios-operations.md#location-manual).

### deviceIDHash {#property_deviceIDHash}

```objectivec translate=no
@property (class, nonatomic, nullable, readonly) NSString *deviceIDHash;
```

Retrieves the appmetrica_device_id_hash.

### deviceID {#property_deviceID}

```objectivec translate=no
@property (class, nonatomic, nullable, readonly) NSString *deviceID;
```

Retrieves the appmetrica_device_id.

### libraryVersion {#property_libraryVersion}

```objectivec translate=no
@property (class, nonatomic, readonly) NSString *libraryVersion;
```

Returns the current version of the AppMetrica library.

### locationTrackingEnabled {#property_locationTrackingEnabled}

```objectivec translate=no
@property (class, nonatomic, getter=isLocationTrackingEnabled) BOOL locationTrackingEnabled;
```

Enables/disables [sending location of the device](../ios-operations.md#track-location) .

### userProfileID {#property_userProfileID}

```objectivec translate=no
@property (class, nonatomic, nullable) NSString *userProfileID;
```

Sets the ID of the [user profile](../../../../data-collection/about-profiles.md). AppMetrica doesn't display `predefined attributes` in the web interface if [ProfieId](../../../../data-collection/profile-attributes.md#pre-defined) sending isn't configured.
