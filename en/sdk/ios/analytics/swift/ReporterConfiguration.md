# ReporterConfiguration class

This class contains the extended immutable configuration of the reporter.

Use the [MutableReporterConfiguration](MutableReporterConfiguration.md) class to change the configuration of a reporter.

## Instance methods {#instance_summary}

#|
|| [init?(apiKey:)](#method_initWithApiKey) | Initializes the instance of the `ReporterConfiguration` class with the specified API key. ||
|#

## Properties {#property_summary}

#|
|| [apiKey](#property_apiKey) | API key that differs from the main application API key. ||
|| [areLogsEnabled](#property_areLogsEnabled) | A flag indicating that the logging of the reporter is enabled. ||
|| [dataSendingEnabled](#property_dataSendingEnabled) | A flag indicating that sending statistics is enabled. ||
|| [dispatchPeriod](#property_dispatchPeriod) | Time interval between sending events in seconds. ||
|| [maxReportsCount](#property_maxReportsCount) | Sending events is triggered when the number of events reaches `maxReportsCount`. ||
|| [maxReportsInDatabaseCount](#property_maxReportsInDatabaseCount) | The maximum number of error reports stored in the internal DB. ||
|| [sessionTimeout](#property_sessionTimeout) | Session timeout in seconds. ||
|| [userProfileID](#property_userProfileID) | Sets the ID of the user profile (`ProfileID`) when activated. ||
|#

## Method descriptions {#method_detail}

### init?(apiKey:) {#method_initWithApiKey}

```objectivec translate=no
init?(apiKey: String)
```

Initializes the instance of the `ReporterConfiguration` class with the specified API key.

**Parameters:**

#|
|| `apiKey` | API key that differs from the main application API key. ||
|#

**Returns:**

The `ReporterConfiguration` class instance.

## Property descriptions {#property_detail}

### apiKey {#property_apiKey}

`var apiKey: String? { get }`

API key that differs from the main application API key.

### areLogsEnabled {#property_areLogsEnabled}

`var areLogsEnabled: Bool { get }`

The flag indicating that the logging of the reporter is enabled.

The default value is `NO`.

Possible values:

- `YES`: Reporter logging is enabled.
- `NO`: Reporter logging is disabled.

### dataSendingEnabled {#property_dataSendingEnabled}

`var dataSendingEnabled: Bool { get }`

A flag indicating that sending statistics is enabled.
The default value is `YES`.

Possible values:
- `YES`: Sending statistics is enabled.
- `NO`: Sending statistics is disabled.

### dispatchPeriod {#property_dispatchPeriod}

`var dispatchPeriod: UInt { get }`

Time interval between sending events in seconds.

### maxReportsCount {#property_maxReportsCount}

`var maxReportsCount: UInt { get }`

Sending events is triggered when the number of events reaches `maxReportsCount`.

### maxReportsInDatabaseCount {#property_maxReportsInDatabaseCount}

`var maxReportsInDatabaseCount { get }`

The maximum number of error reports stored in the internal DB.

The allowed range of values is [100; 10,000]. Values outside this range are automatically replaced with values from the nearest range limits.

Default value: 1000.

{% note info %}

Separate databases are used for various `apiKeys` and independent limits on the number of events can be set for them. This parameter only affects the limitation for the corresponding `apiKey`. To change the maximum allowed number of events for other `apiKeys`, use [AppMetricaConfiguration.maxReportsInDatabaseCount](AppMetricaConfiguration.md#property_maxReportsInDatabaseCount).

{% endnote %}

### sessionTimeout {#property_sessionTimeout}

`var sessionTimeout: UInt { get }`

Session timeout in seconds.

The default value is `10` (minimum allowed value).

### userProfileID {#property_userProfileID}

`var userProfileID: String? { get }`

Sets the ID of the user profile (`ProfileID`) when activated.

{% note alert %}

The maximum length of the `ProfileID` string is 200 characters.

{% endnote %}
