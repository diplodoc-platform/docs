# AMAErrorReportingOptions

Contains parameters for sending errors.

## Enumerations {#enum_summary}

#|
|| [AMAErrorReportingOptions](#enum_AMAErrorReportingOptions) | Contains parameters for sending errors. ||
|#

## Enumeration descriptions {#enum_detail}

### AMAErrorReportingOptions {#enum_AMAErrorReportingOptions}

`AMAErrorReportingOptions`

#|
|| **Constant** | **Description** ||
|| `AMAErrorReportingOptionsNoBacktrace = 1 << 0` | An option that doesn't attach the send call backtrace to the error. Can speed up sending reports.
{% note info %}

This option doesn't affect the backtraces that are passed in the error itself.

{% endnote %} ||
|#
