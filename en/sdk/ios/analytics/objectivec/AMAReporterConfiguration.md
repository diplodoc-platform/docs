# AMAReporterConfiguration class

This class contains the extended immutable configuration of the reporter.

Use the [AMAMutableReporterConfiguration](AMAMutableReporterConfiguration.md) class to change the configuration of a reporter.

## Instance methods {#instance_summary}

#|
|| [-initWithAPIKey:](#method_initWithAPIKey) | Initializes the instance of the `AMAReporterConfiguration` class with the specified API key. ||
|#

## Properties {#property_summary}

#|
|| [APIKey](#property_APIKey) | API key that differs from the app's API key. ||
|| [dataSendingEnabled](#property_dataSendingEnabled) | A flag indicating that sending statistics is enabled. ||
|| [dispatchPeriod](#property_dispatchPeriod) | Time interval between sending events in seconds. ||
|| [logsEnabled](#property_logsEnabled) | A flag indicating that the logging of the reporter is enabled. ||
|| [maxReportsCount](#property_maxReportsCount) | Sending events is triggered when the number of events reaches `maxReportsCount`. ||
|| [maxReportsInDatabaseCount](#property_maxReportsInDatabaseCount) | The maximum number of error reports stored in the internal DB. ||
|| [sessionTimeout](#property_sessionTimeout) | Session timeout in seconds. ||
|| [userProfileID](#property_userProfileID) | Sets the ID of the user profile (`ProfileID`) when activated. ||
|#

## Method descriptions {#method_detail}

### -initWithAPIKey: {#method_initWithAPIKey}

```objectivec translate=no
- (nullable instancetype)initWithAPIKey:(NSString *)APIKey
```

Initializes the instance of the `AMAReporterConfiguration` class with the specified API key.

**Parameters:**

#|
|| `APIKey` | An API key that differs from the app's API key. ||
|#

**Returns:**

The `AMAReporterConfiguration` class instance.

## Property descriptions {#property_detail}

### APIKey {#property_APIKey}

`(nonatomic, copy, nullable, readonly) NSString *APIKey`

An API key that differs from the app's API key.

### dataSendingEnabled {#property_dataSendingEnabled}

`(nonatomic, assign, readonly) BOOL dataSendingEnabled`

A flag indicating that sending statistics is enabled.
The default value is `YES`.

Possible values:
- `YES`: Sending statistics is enabled.
- `NO`: Sending statistics is disabled.

### dispatchPeriod {#property_dispatchPeriod}

`(nonatomic, assign, readonly) NSUInteger dispatchPeriod`

Time interval between sending events in seconds.

### logsEnabled {#property_logsEnabled}

`(nonatomic, assign, readonly, getter=areLogsEnabled) BOOL logsEnabled`

A flag indicating that the logging of the reporter is enabled.

The default value is `NO`.

Possible values:

- `YES`: Reporter logging is enabled.
- `NO`: Reporter logging is disabled.

### maxReportsCount {#property_maxReportsCount}

`(nonatomic, assign, readonly) NSUInteger maxReportsCount`

Sending events is triggered when the number of events reaches `maxReportsCount`.

### maxReportsInDatabaseCount {#property_maxReportsInDatabaseCount}

`(nonatomic, assign, readonly) NSUInteger maxReportsInDatabaseCount`

The maximum number of error reports stored in the internal DB.

The allowed range of values is [100; 10,000]. Values outside this range are automatically replaced with values from the nearest range limits.

Default value: 1000.

{% note info %}

Separate databases are used for various `apiKeys` and independent limits on the number of events can be set for them. This parameter only affects the limitation for the corresponding `apiKey`. To change the maximum allowed number of events for other `apiKeys`, use [AMAAppMetricaConfiguration.maxReportsInDatabaseCount](AMAAppMetricaConfiguration.md#property_maxReportsInDatabaseCount).

{% endnote %}

### sessionTimeout {#property_sessionTimeout}

`(nonatomic, assign, readonly) NSUInteger sessionTimeout`

Session timeout in seconds.

The default value is `10` (minimum allowed value).

### userProfileID {#property_userProfileID}

`(nonatomic, copy, nullable, readonly) NSString *userProfileID`

Sets the ID of the user profile (`ProfileID`) when activated.

{% note alert %}

The maximum length of the `ProfileID` string is 200 characters.

{% endnote %}
