# AppMetricaCrashesConfiguration class

The `AppMetricaCrashesConfiguration` class provides a customizable interface for managing how the app handles different types of errors and issues. It allows you to enable or disable certain types of crash messages and customize the behavior of the reporter (the error reporting mechanism).

## Properties {#property_summary}

#|
|| [autoCrashTracking](#property_autoCrashTracking) | Manages the automatic monitoring of app crashes. ||
|| [probablyUnhandledCrashReporting](#property_probablyUnhandledCrashReporting) | Manages messages about possible unhandled crashes, such as "Out of Memory" errors. ||
|| [ignoredCrashSignals](#property_ignoredCrashSignals) | Defines the array of signals that should be ignored by the reporter. ||
|| [applicationNotRespondingDetection](#property_applicationNotRespondingDetection) | Manages "Application Not Responding" (ANR) status detection. ||
|| [applicationNotRespondingWatchdogInterval](#property_applicationNotRespondingWatchdogInterval) | The timeout period before `watchdog`reports the "Application Not Responding" (ANR) status. ||
|| [applicationNotRespondingPingInterval](#property_applicationNotRespondingPingInterval) | Sets the frequency at which `watchdog` checks for the "Application Not Responding" (ANR) status. ||
|#

### autoCrashTracking {#property_autoCrashTracking}

```swift translate=no
var autoCrashTracking = true
```

Manages the automatic sending of messages about app crashes. Enabled by default.

### probablyUnhandledCrashReporting {#property_probablyUnhandledCrashReporting}

```swift translate=no
var probablyUnhandledCrashReporting = false
```

Manages messages about possible unhandled crashes, such as "Out of Memory" errors. Use this property to enable or disable tracking of crashes that the app might not handle. Disabled by default.

### ignoredCrashSignals {#property_ignoredCrashSignals}

```swift translate=no
var ignoredCrashSignals: [NSNumber]?
```

Defines the array of signals that should be ignored by the reporter. The array must contain `NSNumber` objects configured using signal values as defined in `sys/signal.h`. No signals are ignored by default.

### applicationNotRespondingDetection {#property_applicationNotRespondingDetection}

```swift translate=no
var applicationNotRespondingDetection = false
```

Manages "Application Not Responding" (ANR) status detection. When enabled, the reporter checks if the main thread is blocked and reports accordingly. Detection is automatically paused when the app is running in the background. Disabled by default.

### applicationNotRespondingWatchdogInterval {#property_applicationNotRespondingWatchdogInterval}

```swift translate=no
var applicationNotRespondingWatchdogInterval: TimeInterval = 4.0
```

Specifies the timeout period before `watchdog` reports the "Application Not Responding" (ANR) status. By default, the interval is 4 seconds. Only takes effect after activation and only if the `allowsBackgroundLocationUpdates` option is enabled.

### applicationNotRespondingPingInterval {#property_applicationNotRespondingPingInterval}

```swift translate=no
var applicationNotRespondingPingInterval: TimeInterval = 0.1
```

Sets the frequency at which `watchdog` checks for the "Application Not Responding" (ANR) status. By default, the interval is 0.1 seconds. Reducing the interval may lead to a decrease in app performance. Only takes effect after activation and only if the `allowsBackgroundLocationUpdates` option is enabled.
