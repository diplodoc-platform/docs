# ErrorReportingOptions

Содержит параметры отправки ошибок.

## Перечисления {#enum_summary}

#|
|| [ErrorReportingOptions](#enum_ErrorReportingOptions) | Содержит параметры отправки ошибок. ||
|#

## Описание перечислений {#enum_detail}

### ErrorReportingOptions {#enum_ErrorReportingOptions}

`ErrorReportingOptions`

#|
|| **Константа** | **Описание** ||
|| `static var noBacktrace: ErrorReportingOptions { get }` | Опция, которая не прикрепляет бэктрейс вызова отправки к ошибке. Может увеличить скорость отправки отчетов.
{% note info %}

Опция не влияет на бэктрейсы, которые переданы в самой ошибке.

{% endnote %} ||
|#
