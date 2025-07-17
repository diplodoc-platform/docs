# AMAAppMetricaConfiguration class

This class contains the extended startup configuration for the library.

The parameters of the extended configuration are applied from the time of library initialization.

## Instance methods {#instance_summary}

#|
|| [-initWithAPIKey:](#method_initWithAPIKey) | Initializes the instance of the `AMAAppMetricaConfiguration` class with the specified API key. ||
|#

## Properties {#property_summary}

#|
|| [APIKey](#property_APIKey) | The API key of the app. ||
|| [accurateLocationTracking](#property_accurateLocationTracking) | Enable/disable accurate location search for the internal location manager. ||
|| [allowsBackgroundLocationUpdates](#property_allowsBackgroundLocationUpdates) | Enable/disable background tracking of location updates. ||
|| [appBuildNumber](#property_appBuildNumber) | Set an app build number for the AppMetrica report. ||
|| [appEnvironment](#property_appEnvironment) | Sets the app environment for all events from the moment of activation. ||
|| [appOpenTrackingEnabled](#property_appOpenTrackingEnabled) | Enables/disables the automatic collection and sending of data about app launches via a deeplink. ||
|| [appVersion](#property_appVersion) | App version. ||
|| [customHosts](#property_customHosts) | Set proxy URLs for AppMetrica that will be used for startup queries. ||
|| [customLocation](#property_customLocation) | Sets custom location of the device. ||
|| [dataSendingEnabled](#property_dataSendingEnabled) | Enables/disables sending statistics to the AppMetrica server. ||
|| [dispatchPeriod](#property_dispatchPeriod) | Set a custom sending period. Interval in seconds between sending events to the server. ||
|| [handleActivationAsSessionStart](#property_handleActivationAsSessionStart) | Defines the AppMetrica SDK initialization as the beginning of a user session. This option is disabled by default. ||
|| [handleFirstActivationAsUpdate](#property_handleFirstActivationAsUpdate) | Defines the first launch of the app as an update. ||
|| [locationTracking](#property_locationTracking) | Enables/disables sending location of the device. ||
|| [logsEnabled](#property_logsEnabled) | Enables/disables logging the activity of the library. ||
|| [maxReportsCount](#property_maxReportsCount) | Set the maximum number of stored events. ||
|| [maxReportsInDatabaseCount](#property_maxReportsInDatabaseCount) | The maximum number of error reports stored in the internal DB. ||
|| [preloadInfo](#property_preloadInfo) | Sets the instance of the [AMAAppMetricaPreloadInfo](AMAAppMetricaPreloadInfo.md) class for tracking pre-installed apps. ||
|| [revenueAutoTrackingEnabled](#property_revenueAutoTrackingEnabled) | Enables/disables the automatic collection of information about in-app purchases. ||
|| [sessionTimeout](#property_sessionTimeout) | Sets the session timeout in seconds. ||
|| [sessionsAutoTracking](#property_sessionsAutoTracking) | Enables/disables automatic tracking of the app lifecycle. ||
|| [userProfileID](#property_userProfileID) | Sets the ID of the user profile (`ProfileID`) when activated. ||
|#

## Method descriptions {#method_detail}

### -initWithAPIKey: {#method_initWithAPIKey}

```objectivec translate=no
- (instancetype)initWithAPIKey:(NSString *)APIKey
```

Initializes the instance of the `AMAAppMetricaConfiguration` class with the specified API key.

**Parameters:**

#|
|| `APIKey` | The API key of the app. ||
|#

**Returns:**

The `AMAAppMetricaConfiguration` class instance.

## Property descriptions {#property_detail}

### APIKey {#property_APIKey}

```objectivec translate=no
@property (nonatomic, copy, readonly) NSString *APIKey;
```

The API key of the application.

### accurateLocationTracking {#property_accurateLocationTracking}

```objectivec translate=no
@property (nonatomic, assign) BOOL accurateLocationTracking;
```

Enable/disable accurate location search for the internal location manager. Disabled by default.

Active only if location tracking has been set to `YES`, and the location isn't set manually.

### allowsBackgroundLocationUpdates {#property_allowsBackgroundLocationUpdates}

```objectivec translate=no
@property (nonatomic, assign) BOOL allowsBackgroundLocationUpdates;
```

Enable/disable background tracking of location updates. Disabled by default.

To enable background tracking of location updates, set the property to `YES`.

### appBuildNumber {#property_appBuildNumber}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSString *appBuildNumber;
```

Set an app build number for the AppMetrica report.

If not set, AppMetrica will use the app build number specified in the app configuration file `Info.plist` (`CFBundleVersion`).
The app build number must be a numeric string that can be converted to a positive integer.

### appEnvironment {#property_appEnvironment}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSDictionary<NSString *, NSString *> *appEnvironment;
```

Sets the app environment for all events from the moment of activation.

### appOpenTrackingEnabled {#property_appOpenTrackingEnabled}

```objectivec translate=no
@property (nonatomic, assign) BOOL appOpenTrackingEnabled;
```

Enables/disables the automatic collection and sending of data about app launches via a deeplink.

{% note alert %}

Starting with version 4.0 of the AppMetrica SDK for iOS, app openings via deeplinks are tracked automatically. For other versions, set up tracking manually:

- iOS AppMetrica SDK version below 4.0. [Setting up](../../../../sdk/ios/analytics/ios-operations.md#ui-app-delegate) deeplink tracking for UIApplicationDelegate.
- [Setting up](../../../../sdk/ios/analytics/ios-operations#ui-scene-delegate) deeplink tracking for UISceneDelegate (AppMetrica doesn't track such app openings automatically).

Automatic tracking captures only those deeplinks that resulted in app launches. To track deeplinks inside the running app, also set up [tracking](../ios-operations.md).

{% endnote %}

The option is enabled by default.

Possible values:

- `YES`: Automatic collection and sending of data about the app launch via a deeplink is enabled.
- `NO`: Automatic collection and sending of data about the app launch via a deeplink is disabled.

### appVersion {#property_appVersion}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSString *appVersion;
```

App version.

### customHosts {#property_customHosts}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSArray *customHosts;
```

Set proxy URLs for AppMetrica that will be used for startup queries.

### customLocation {#property_customLocation}

```objectivec translate=no
@property (nonatomic, strong, nullable) CLLocation *customLocation;
```

### dataSendingEnabled {#property_dataSendingEnabled}

```objectivec translate=no
@property (nonatomic, assign) BOOL dataSendingEnabled;
```

Sets custom location of the device.

### dispatchPeriod {#property_dispatchPeriod}

```objectivec translate=no
@property (nonatomic, assign) NSUInteger dispatchPeriod;
```

Set a custom sending period. Interval in seconds between sending events to the server.

By default, this is 90 seconds. Setting the value to 0 seconds prevents the library from automatically sending events using the timer.

### handleActivationAsSessionStart {#property_handleActivationAsSessionStart}

```objectivec translate=no
@property (nonatomic, assign) BOOL handleActivationAsSessionStart;
```

Defines the AppMetrica SDK initialization as the beginning of a user session.

This option is disabled by default.

Possible values:

- `YES`: The user session is created when the library is initialized.
- `NO`: A background session is created when the library is initialized, and a user session is created after the [UIApplicationDidBecomeActiveNotification](https://developer.apple.com/documentation/uikit/uiapplicationdidbecomeactivenotification) system event.

### handleFirstActivationAsUpdate {#property_handleFirstActivationAsUpdate}

```objectivec translate=no
@property (nonatomic, assign) BOOL handleFirstActivationAsUpdate;
```

Defines the first launch of the app as an update.

{% note info %}

If the first launch of the app is defined as an update, the install is not shown as a new install in reports and is not attributed to partners.

{% endnote %}

Possible values:

- `YES`: The first launch is defined as an update.
- `NO`: The first launch is defined as a new install.

### locationTracking {#property_locationTracking}

```objectivec translate=no
@property (nonatomic, assign) BOOL locationTracking;
```

Enables/disables sending location of the device.

By default, sending is enabled.

### logsEnabled {#property_logsEnabled}

```objectivec translate=no
@property (nonatomic, assign, getter=areLogsEnabled) BOOL logsEnabled;
```

Enables/disables logging the activity of the library.

Logging is disabled by default.

### maxReportsCount {#property_maxReportsCount}

```objectivec translate=no
@property (nonatomic, assign) NSUInteger maxReportsCount;
```

Set the maximum number of stored events. The minimum number of cached events that causes reports to be sent automatically.

By default, events are sent automatically when there are at least 7 items in the storage.

Setting the value to 0 seconds prevents the library from automatically sending events upon reaching the set number of events in the storage.

### maxReportsInDatabaseCount {#property_maxReportsInDatabaseCount}

```objectivec translate=no
@property (nonatomic, assign) NSUInteger maxReportsInDatabaseCount;
```

The maximum number of error reports stored in the internal DB.

The allowed range of values is [100; 10,000]. Values outside this range are automatically replaced with values from the nearest range limits.

Default value: 1000.

{% note info %}

Separate databases are used for various `apiKeys` and independent limits on the number of events can be set for them. This parameter only affects the limitation for the corresponding `apiKey`. To change the maximum allowed number of events for other `apiKeys`, use [AMAReporterConfiguration.maxReportsInDatabaseCount](AMAReporterConfiguration.md#property_maxReportsInDatabaseCount).

{% endnote %}

### preloadInfo {#property_preloadInfo}

```objectivec translate=no
@property (nonatomic, copy, nullable) AMAAppMetricaPreloadInfo *preloadInfo;
```

Sets the instance of the [AMAAppMetricaPreloadInfo](AMAAppMetricaPreloadInfo.md) class for tracking pre-installed apps.

For more information, see [Tracking pre-installed apps](../../../../mobile-tracking/preinstalled-app-attr.md).

### revenueAutoTrackingEnabled {#property_revenueAutoTrackingEnabled}

```objectivec translate=no
@property (nonatomic, assign) BOOL revenueAutoTrackingEnabled;
```

Enables/disables the automatic collection of information about In-App purchases.

The option is enabled by default.

Possible values:

- `YES`: Automatic collection and sending of information about in-app purchases is enabled.
- `NO`: Automatic collection and sending of information about in-app purchases is disabled.

### sessionTimeout {#property_sessionTimeout}

```objectivec translate=no
@property (nonatomic, assign) NSUInteger sessionTimeout;
```

Sets the session timeout in seconds.
The default value is `10` (minimum allowed value).

For more information about sessions, see [Tracking user activity](../ios-listen.md).

### sessionsAutoTracking {#property_sessionsAutoTracking}

```objectivec translate=no
@property (nonatomic, assign) BOOL sessionsAutoTracking;
```

Enables/disables automatic tracking of the application lifecycle.

The option is enabled by default.

If the option is disabled, you need to manually set up session duration control using the [+pauseSession:](AMAAppMetrica.md#method_pauseSession) and [+resumeSession:](AMAAppMetrica.md#method_resumeSession) methods. For more information, see [Manual session tracking](../ios-listen.md).

AppMetrica uses [UIApplicationDidBecomeActiveNotification](https://developer.apple.com/documentation/uikit/uiapplicationdidbecomeactivenotification) and [UIApplicationWillResignActiveNotification](https://developer.apple.com/documentation/uikit/uiapplicationwillresignactivenotification) to track sessions. The maximum session length is 24 hours. To extend the session after 24 hours, invoke the [+resumeSession:](AMAAppMetrica.md#method_resumeSession) method manually.

### userProfileID {#property_userProfileID}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSString *userProfileID;
```

Sets the ID of the user profile (`ProfileID`) when activated.

{% note alert %}

The maximum length of the `ProfileID` string is 200 characters.

{% endnote %}
