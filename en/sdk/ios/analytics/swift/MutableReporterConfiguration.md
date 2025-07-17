# MutableReporterConfiguration class

The mutable version of the [ReporterConfiguration](ReporterConfiguration.md) class with the advanced configuration of the reporter.

## Properties {#property_summary}

#|
|| [areLogsEnabled](#property_areLogsEnabled) | Enables/disables logging the activity of the library. ||
|| [dataSendingEnabled](#property_dataSendingEnabled) | Enables/disables sending statistics to the AppMetrica server. ||
|| [dispatchPeriod](#property_dispatchPeriod) | Time interval between sending events in seconds. ||
|| [maxReportsCount](#property_maxReportsCount) | Sending events is triggered when the number of events reaches `maxReportsCount`. ||
|| [maxReportsInDatabaseCount](#property_maxReportsInDatabaseCount) | The maximum number of error reports stored in the internal DB. ||
|| [sessionTimeout](#property_sessionTimeout) | Sets the session timeout in seconds. ||
|| [userProfileID](#property_userProfileID) | Sets the ID of the user profile (`ProfileID`) when activated. ||
|#

## Property descriptions {#property_detail}

### areLogsEnabled {#property_areLogsEnabled}

`var areLogsEnabled: Bool`

Enables/disables logging the activity of the library.

Logging is disabled by default.

### dataSendingEnabled {#property_dataSendingEnabled}

`var dataSendingEnabled: Bool`

Enables/disables sending statistics to the AppMetrica server.

{% note info %}

Disable sending statistics to the reporter does not affect the sending of data from the main API key. But disabling data sending for the main API key stops sending statistics from all reporters.

{% endnote %}

By default, sending is enabled.

### dispatchPeriod {#property_dispatchPeriod}

`var dispatchPeriod: UInt`

Time interval between sending events in seconds.

### maxReportsCount {#property_maxReportsCount}

`var maxReportsCount: UInt`

Sending events is triggered when the number of events reaches `maxReportsCount`.

### maxReportsInDatabaseCount {#property_maxReportsInDatabaseCount}

`var maxReportsInDatabaseCount: UInt`

The maximum number of error reports stored in the internal DB.

The allowed range of values is [100; 10,000]. Values outside this range are automatically replaced with values from the nearest range limits.

Default value: 1000.

{% note info %}

Separate databases are used for various `apiKeys` and independent limits on the number of events can be set for them. This parameter only affects the limitation for the corresponding `apiKey`. To change the maximum allowed number of events for other `apiKeys`, use [AppMetricaConfiguration.maxReportsInDatabaseCount](AppMetricaConfiguration.md#property_maxReportsInDatabaseCount).

{% endnote %}

### sessionTimeout {#property_sessionTimeout}

`var sessionTimeout: UInt`

Sets the session timeout in seconds.

The default value is `10` (minimum allowed value).

### userProfileID {#property_userProfileID}

`var userProfileID: String?`

Sets the ID of the user profile (`ProfileID`) when activated.

{% note alert %}

The maximum length of the `ProfileID` string is 200 characters.

{% endnote %}
