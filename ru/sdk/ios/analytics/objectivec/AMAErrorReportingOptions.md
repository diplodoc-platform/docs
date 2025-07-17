# AMAErrorReportingOptions

Содержит параметры отправки ошибок.

## Перечисления {#enum_summary}

#|
|| [AMAErrorReportingOptions](#enum_AMAErrorReportingOptions) | Содержит параметры отправки ошибок. ||
|#

## Описание перечислений {#enum_detail}

### AMAErrorReportingOptions {#enum_AMAErrorReportingOptions}

`AMAErrorReportingOptions`

#|
|| **Константа** | **Описание** ||
|| `AMAErrorReportingOptionsNoBacktrace = 1 << 0` | Опция, которая не прикрепляет бэктрейс вызова отправки к ошибке. Может увеличить скорость отправки отчетов.
{% note info %}

Опция не влияет на бэктрейсы, которые переданы в самой ошибке.

{% endnote %} ||
|#
