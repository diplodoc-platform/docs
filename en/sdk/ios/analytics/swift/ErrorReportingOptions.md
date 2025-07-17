# ErrorReportingOptions

Contains parameters for sending errors.

## Enumerations {#enum_summary}

#|
|| [ErrorReportingOptions](#enum_ErrorReportingOptions) | Contains parameters for sending errors. ||
|#

## Enumeration descriptions {#enum_detail}

### ErrorReportingOptions {#enum_ErrorReportingOptions}

`ErrorReportingOptions`

#|
|| **Константа** | **Описание** ||
|| `static var noBacktrace: ErrorReportingOptions { get }` | An option that doesn't attach the send call backtrace to the error. Can speed up sending reports.
{% note info %}

This option doesn't affect the backtraces that are passed in the error itself.

{% endnote %} ||
|#
