# AppMetrica class

Methods of the class are used for configuring the library.

## Instance methods {#instance_summary}

#|
|| [activate(with:)](#method_activateWithConfiguration) | Initializes the library in an application with the [extended startup configuration](../ios-operations.md). ||
|| [activateReporter(with:)](#method_activateReporterWithConfiguration) | Initializes a reporter with the extended configuration. ||
|| [clearAppEnvironment()](#method_clearAppEnvironment) | Deleting all key-value data associated with all future events. ||
|| [pauseSession()](#method_pauseSession) | Pauses the user session. ||
|| [reportAdRevenue(_:onFailure:)](#method_reportAdRevenue__onFailure) | Sends information about advertising revenue to the AppMetrica server. ||
|| [reportECommerce(_:onFailure:)](#method_reportECommerce__onFailure) | Sends a message about an E-commerce event. ||
|| [reportEvent(name:onFailure:)](#method_reportEvent__onFailure) | Sends an [event message](../ios-operations.md#report-event). ||
|| [reportEvent(name:parameters:onFailure:)](#method_reportEvent__parameters__onFailure) | Sends an [event message with additional parameters](../ios-operations.md#report-event-params). ||
|| [reportExternalAttribution(_:from:onFailure:)](#method_reportExternalAttribution__from__onFailure) | Sends [external attribution](../../../../data-collection/attribution-integration.yaml) data to AppMetrica. ||
|| [reportRevenue(_:onFailure:)](#method_reportRevenue__onFailure) | Sends information about the purchase to the AppMetrica server. ||
|| [reportUserProfile(_:onFailure:)](#method_reportUserProfile__onFailure) | Sends information about a user profile update. ||
|| [reporter(for:)](#method_reporterForAPIKey) | Creates a reporter for [sending events to an additional API key](../ios-operations.md#reporter-different-apikey). ||
|| [requestStartupIdentifiers(for:on:completion:)](#method_requestStartupIdentifiersWithKeys__completionQueue__completionBlock) | Requests IDs for specific keys. ||
|| [requestStartupIdentifiers(on:completion:)](#method_requestStartupIdentifiersWithCompletionQueue__completionBlock) | Requests all predefined IDs. ||
|| [resumeSession()](#method_resumeSession) | Resumes the session, or creates a new one if the session timeout has expired. ||
|| [sendEventsBuffer()](#method_sendEventsBuffer) | Sends stored events from the buffer. ||
|| [setAppEnvironment(:forKey:)](#method_setAppEnvironmentValue__forKey) | Sets a key-value pair associated with all future events. ||
|| [setDataSendingEnabled(_:)](#method_setDataSendingEnabled) | Enables/disables sending statistics to the AppMetrica server. ||
|| [setupWebViewReporting(with:onFailure:)](#method_setupWebViewReporting__onFailure) | Adds a JavaScript interface with the AppMetrica name in a window to the specified WebView. This lets you send client events from JavaScript code. ||
|| [trackOpeningURL(_:)](#method_trackOpeningURL) | Processes the URL that opened the app. ||
|#

## Properties {#property_summary}

#|
|| [allowsBackgroundLocationUpdates](#property_allowsBackgroundLocationUpdates) | Enable/disable background tracking of location updates. ||
|| [customLocation](#property_customLocation) | Sets [custom location of the device](../ios-operations.md#location-manual). ||
|| [deviceIDHash](#property_deviceIDHash) | The current appmetrica_device_id_hash. ||
|| [deviceID](#property_deviceID) | The current appmetrica_device_id. ||
|| [isAccurateLocationTrackingEnabled](#property_accurateLocationTrackingEnabled) | Controls the accuracy of location tracking used by the internal location manager. ||
|| [isActivated](#property_activated) | Indicates whether AppMetrica was activated. ||
|| [isLocationTrackingEnabled](#property_locationTrackingEnabled) | Enables/disables [sending location of the device](../ios-operations.md#track-location). ||
|| [libraryVersion](#property_libraryVersion) | The current version of the AppMetrica library. ||
|| [userProfileID](#property_userProfileID) | Sets the ID of the [user profile](../../../../data-collection/about-profiles.md). ||
|| [uuid](#property_UUID) | The current UUID. ||
|#

## Method descriptions {#method_detail}

### activate(with:) {#method_activateWithConfiguration}

```swift translate=no
class func activate(with: AppMetricaConfiguration)
```

Initializes the library in an app with the [extended startup configuration](../ios-operations.md#initialize).

**Parameters:**

#|
|| `with` | The instance of the [AppMetricaConfiguration](AppMetricaConfiguration.md) class which contains the extended startup configuration for the library. ||
|#

### activateReporter(with:) {#method_activateReporterWithConfiguration}

```swift translate=no
class func activateReporter(with: ReporterConfiguration)
```

Initializes a reporter with extended configuration.

The configuration of the reporter should be initialized before the first call to the reporter. Otherwise, the configuration of the reporter is ignored.

The reporter should be activated with the configuration using a different API key instead of the app's API key.

**Parameters:**

#|
|| `with` | The instance of the [ReporterConfiguration](ReporterConfiguration.md) class which contains the extended configuration for the reporter. ||
|#

### clearAppEnvironment() {#method_clearAppEnvironment}

```swift translate=no
class func clearAppEnvironment()
```

Cleaning the app environment, such as deleting all key-value data associated with all future events.

### pauseSession() {#method_pauseSession}

```swift translate=no
class func pauseSession()
```

Pauses the user session.

{% note info %}

The session duration depends on [specified timeout](AppMetricaConfiguration.md#property_sessionTimeout). If the time interval between pausing and resuming the session is less than the specified timeout, the current session will be resumed; otherwise, a new one will be created.

For more information about sessions, see [Tracking user activity](../ios-listen.md).

{% endnote %}

### reportAdRevenue(_:onFailure:) {#method_reportAdRevenue__onFailure}

```swift translate=no
class func reportAdRevenue(_ adRevenue: AdRevenueInfo, onFailure: ((Error) -> Void)?)
```

Sends information about advertising revenue to the AppMetrica server.

**Parameters:**

#|
|| `adRevenue` | The instance of the [AdRevenueInfo](AdRevenueInfo.md) class which contains information about advertising revenue. ||
|| `onFailure` | A callback method to be called in the event of an error. ||
|#

### reportECommerce(_:onFailure:) {#method_reportECommerce__onFailure}

```swift translate=no
class func reportECommerce(_ eCommerce: ECommerce, onFailure: ((Error) -> Void)?)
```

Sends a message about an E-commerce event.

**Parameters:**

#|
|| `eCommerce` | The [ECommerce](ECommerce.md) class instance. ||
|| `onFailure` | A callback method to be called in the event of an error. ||
|#

### reportEvent(name:onFailure) {#method_reportEvent__onFailure}

```swift translate=no
class func reportEvent(name: String, onFailure: ((Error) -> Void)?)
```

Sends an [event message](../ios-operations.md#report-event).

**Parameters:**

#|
|| `name` | Short name or description of the event. ||
|| `onFailure` | The block that is executed when an error occurs. The error is passed as a block argument. ||
|#

### reportEvent(name:parameters:onFailure) {#method_reportEvent__parameters__onFailure}

```swift translate=no
class func reportEvent(name: String, parameters: [AnyHashable : Any]?, onFailure: ((Error) -> Void)?)
```

Sends an [event message with additional parameters](../ios-operations.md#report-event-params).

**Parameters:**

#|
|| `name` | Short name or description of the event. ||
|| `parameters` | Parameters as <q>key-value</q> pairs. ||
|| `onFailure` | A callback method to be called in the event of an error. ||
|#

### reportExternalAttribution(_:from:onFailure:) {#method_reportExternalAttribution__from__onFailure}

```swift translate=no
class func reportExternalAttribution(_ attribution: [AnyHashable : Any], from source: AttributionSource, onFailure: ((any Error) -> Void)? = nil)
```

Sends [external attribution](../../../../data-collection/attribution-integration.yaml) data to AppMetrica.

#|
|| `attribution` | A dictionary with attribution data. It must be convertible to JSON, or else the method fails with the `onFailure` error block run. ||
|| `source` | The attribution data source. [Source list](AttributionSource.md). ||
|| `onFailure` | A callback method to be called in the event of an error. The error is passed as an argument. ||
|#

### reportRevenue(_:onFailure:) {#method_reportRevenue__onFailure}

```swift translate=no
class func reportRevenue(_ revenueInfo: RevenueInfo, onFailure: ((Error) -> Void)?)
```

Sends information about the purchase to the AppMetrica server.

**Parameters:**

#|
|| `revenueInfo` | The instance of the [RevenueInfo](RevenueInfo.md) class which contains information about a purchase. ||
|| `onFailure` | A callback method to be called in the event of an error. ||
|#

### reportUserProfile(_:onFailure:) {#method_reportUserProfile__onFailure}

```swift translate=no
class func reportUserProfile(_ userProfile: UserProfile, onFailure: ((Error) -> Void)?)
```

Sends information about the user profile update.

**Parameters:**

#|
|| `userProfile` | The instance of the [UserProfile](UserProfile.md) class which contains information about the user profile. ||
|| `onFailure` | A callback method to be called in the event of an error. ||
|#

### reporter(for:) {#method_reporterForAPIKey}

```swift translate=no
class func reporter(for: String) -> AppMetricaReporting
```

Creates a reporter for [sending events to an additional API key](../ios-operations.md#reporter-different-apikey).

To initialize a reporter with the extended configuration, use the [activateReporter(with:)](#method_activateReporterWithConfiguration) method. The configuration of the reporter should be initialized before the first call to the reporter. Otherwise, the configuration of the reporter is ignored.

**Parameters:**

#|
|| `for` | An API key that differs from the app's API key. ||
|#

**Returns:**

The instance that implements the [AppMetricaReporting](AppMetricaReporting.md) protocol for the specified API key.

### requestStartupIdentifiers(for:on:completion:) {#requestStartupIdentifiersWithKeys__completionQueue__completionBlock}

```swift translate=no
class func requestStartupIdentifiers(for: [StartupKey], on: dispatch_queue_t?, completion: ([StartupKey : Any]?, Error?) -> Void)
```

Getting IDs for specific keys

**Parameters:**

#|
|| `for` | An array of identification keys for the query. See `StartupKey`. ||
|| `on` | Queue for sending a block. If the value is zero, the main queue is used. ||
|| `completion` | The block will be sent when available IDs appear or in case of an error.

If they are available at the time of calling, the block is sent immediately. See the `AMAIdentifiersCompletionBlock` definition for more information about the returned types.

||
|#

### requestStartupIdentifiers(on:completion:) {#method_requestStartupIdentifiersWithCompletionQueue__completionBlock}

```swift translate=no
class func requestStartupIdentifiers(on: dispatch_queue_t?, completion: ([StartupKey : Any]?, Error?) -> Void)
```

Getting all predefined IDs

**Parameters:**

#|
|| `on` | Queue for sending a block. If the value is zero, the main queue is used. ||
|| `completion` | The block will be sent when available IDs appear or in case of an error.

Predefined IDs are:
- `StartupKey.uuidKey`
- `StartupKey.deviceIDHashKey`
- `StartupKey.deviceIDKey`

If they are available at the time of calling, the block is sent immediately. See the `AMAIdentifiersCompletionBlock` definition for more information about the returned types.

||
|#

### resumeSession() {#method_resumeSession}

```swift translate=no
class func resumeSession()
```

Resumes the session, or creates a new one if the session timeout has expired.

{% note info %}

The session duration depends on [specified timeout](AppMetricaConfiguration.md#property_sessionTimeout). If the time interval between pausing and resuming the session is less than the specified timeout, the current session will be resumed; otherwise, a new one will be created.

For more information about sessions, see [Tracking user activity](../ios-listen.md).

{% endnote %}

### sendEventsBuffer() {#method_sendEventsBuffer}

```swift translate=no
class func sendEventsBuffer()
```

Sends stored events from the buffer.

AppMetrica SDK does not send an event immediately after it occurred. The library stores event data in the buffer. The `sendEventsBuffer()` method sends data from the buffer and flushes it. Use the method to force sending stored events after passing important checkpoints of user scenarios.

{% note alert %}

Frequent use of the method can lead to increased outgoing internet traffic and energy consumption.

{% endnote %}

### setAppEnvironment(_:forKey:) {#method_setAppEnvironmentValue__forKey}

```swift translate=no
class func setAppEnvironment(_ value: String?, forKey: String)
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
class func setDataSendingEnabled(_ enabled: Bool)
```

Enables/disables sending statistics to the AppMetrica server.

For more information about using the method, see [Disabling and enabling sending statistics](../ios-operations.md#stat).

{% note info %}

Disabling sending also turns off sending data from all reporters that initialized with the other API key.

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
|| `with` | The `JSControlling` instance. ||
|| `onFailure` | A callback method to be called in the event of an error. ||
|#

### trackOpeningURL(_:) {#method_trackOpeningURL}

```swift translate=no
class func trackOpeningURL(_ URL: URL)
```

Processes the URL that opened the application.

Used for [tracking app openings via deeplink](../ios-operations.md#deeplink).

**Parameters:**

#|
|| `URL` | URL that opened the app. ||
|#

## Property descriptions {#property_detail}

### allowsBackgroundLocationUpdates {#property_allowsBackgroundLocationUpdates}

```swift translate=no
var allowsBackgroundLocationUpdates: Bool { get; set; }
```

Enable/disable background tracking of location updates. Disabled by default.

### customLocation {#property_customLocation}

```swift translate=no
var customLocation: CLLocation? { get; set; }
```

Sets [custom location of the device](../ios-operations.md#location-manual).

### deviceIDHash {#property_deviceIDHash}

```swift translate=no
var deviceIDHash: String? { get; }
```

Retrieves the appmetrica_device_id_hash.

### deviceID {#property_deviceID}

```swift translate=no
var deviceID: String? { get; }
```

Retrieves the appmetrica_device_id.

### isAccurateLocationTrackingEnabled {#property_accurateLocationTrackingEnabled}

```swift translate=no
var isAccurateLocationTrackingEnabled: Bool { get; set; }
```

Controls the accuracy of location tracking used by the internal location manager.

If set to `true`, the location manager attempts to use the most accurate location data available.
This property takes effect only if the `isLocationTrackingEnabled` parameter is set to `true`, and the location
wasn't set manually using the `customLocation` property.

### isActivated {#property_activated}

```swift translate=no
var isActivated: Bool { get; }
```

Indicates whether AppMetrica was activated.

{% note info %}

Use this property to check whether AppMetrica has already been activated, typically to avoid redundant activation calls or to make sure that statistics collection is running.

{% endnote %}

### isLocationTrackingEnabled {#property_locationTrackingEnabled}

```swift translate=no
var isLocationTrackingEnabled: Bool { get; set; }
```

Enables/disables [sending location of the device](../ios-operations.md#track-location) .

### libraryVersion {#property_libraryVersion}

```swift translate=no
var libraryVersion: String { get; }
```

Returns the current version of the AppMetrica library.

### userProfileID {#property_userProfileID}

```swift translate=no
var userProfileID: String? { get; set; }
```

Sets the ID of the [user profile](../../../../data-collection/about-profiles.md). AppMetrica doesn't display `predefined attributes` in the web interface if [ProfieId](../../../../data-collection/profile-attributes.md#pre-defined) sending isn't configured.

### uuid {#property_UUID}

```swift translate=no
var uuid: String { get; }
```

Retrieves the current UUID.
