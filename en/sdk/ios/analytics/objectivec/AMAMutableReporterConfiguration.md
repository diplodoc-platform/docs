# AMAMutableReporterConfiguration class

The mutable version of the [AMAReporterConfiguration](AMAReporterConfiguration.md) class with the advanced configuration of the reporter.

## Properties {#property_summary}

#|
|| [dataSendingEnabled](#property_dataSendingEnabled) | Enables/disables sending statistics to the AppMetrica server. ||
|| [dispatchPeriod](#property_dispatchPeriod) | Time interval between sending events in seconds. ||
|| [logsEnabled](#property_logsEnabled) | Enables/disables logging the activity of the library. ||
|| [maxReportsCount](#property_maxReportsCount) | Sending events is triggered when the number of events reaches `maxReportsCount`. ||
|| [maxReportsInDatabaseCount](#property_maxReportsInDatabaseCount) | The maximum number of error reports stored in the internal DB. ||
|| [sessionTimeout](#property_sessionTimeout) | Sets the session timeout in seconds. ||
|| [userProfileID](#property_userProfileID) | Sets the ID of the user profile (`ProfileID`) when activated. ||
|#

## Property descriptions {#property_detail}

### dataSendingEnabled {#property_dataSendingEnabled}

`(nonatomic, assign) BOOL dataSendingEnabled`

Enables/disables sending statistics to the AppMetrica server.

{% note info %}

Disable sending statistics to the reporter does not affect the sending of data from the main API key. But disabling data sending for the main API key stops sending statistics from all reporters.

{% endnote %}

By default, sending is enabled.

### dispatchPeriod {#property_dispatchPeriod}

`(nonatomic, assign) NSUInteger dispatchPeriod`

Time interval between sending events in seconds.

### logsEnabled {#property_logsEnabled}

`(nonatomic, assign, getter=areLogsEnabled) BOOL logsEnabled`

Enables/disables logging the activity of the library.

Logging is disabled by default.

### maxReportsCount {#property_maxReportsCount}

`(nonatomic, assign) NSUInteger maxReportsCount`

Sending events is triggered when the number of events reaches `maxReportsCount`.

### maxReportsInDatabaseCount {#property_maxReportsInDatabaseCount}

`(nonatomic, assign) NSUInteger maxReportsInDatabaseCount`

The maximum number of error reports stored in the internal DB.

The allowed range of values is [100; 10,000]. Values outside this range are automatically replaced with values from the nearest range limits.

Default value: 1000.

{% note info %}

Separate databases are used for various `apiKeys` and independent limits on the number of events can be set for them. This parameter only affects the limitation for the corresponding `apiKey`. To change the maximum allowed number of events for other `apiKeys`, use [AMAAppMetricaConfiguration.maxReportsInDatabaseCount](AMAAppMetricaConfiguration.md#property_maxReportsInDatabaseCount).

{% endnote %}

### sessionTimeout {#property_sessionTimeout}

`(nonatomic, assign) NSUInteger sessionTimeout`

Sets the session timeout in seconds.

The default value is `10` (minimum allowed value).

### userProfileID {#property_userProfileID}

`(nonatomic, copy, nullable) NSString *userProfileID`

Sets the ID of the user profile (`ProfileID`) when activated.

{% note alert %}

The maximum length of the `ProfileID` string is 200 characters.

{% endnote %}
