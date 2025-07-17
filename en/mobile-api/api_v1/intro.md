# Introduction

The Reporting API allows you to get application traffic statistics and other data without using the AppMetrica interface.

Dimensions and metrics are used for making API requests.

A _dimension_ is an attribute that can be used for grouping data.

In API requests, dimensions are set in the `dimensions` parameter. If you need to list multiple dimensions, separate them with commas.

It is also possible to make a report without dimensions; in this case, the total result is calculated.

A _metric_ is a numerical value that is based on an attribute of a session.

In API requests, metrics are set in the `metrics` parameter. If you need to list multiple metrics, separate them with commas.

{% cut "More about terminology" %}

To better understand the terms <q>dimension</q> and <q>metric</q>, consider the example of a report on the device manufacturer:

| Device manufacturer | Number of users |
| ----- | ----- |
| Apple | | 1803 |
| Samsung | 1272 |
| NOKIA | 809 |

Where

- `Device manufacturer` is a session attribute that is used for grouping report data (a _dimension_).
- `Number of users` is a value calculated from numerical session attributes (a _metric_) corresponding to the specified dimension.

{% note info %}

If you are familiar with SQL, you can think of dimensions as columns used for grouping, and metrics as the results returned by aggregate functions.

{% endnote %}

{% endcut %}

You can create the desired report structure by specifying metrics and dimensions in the API request.

For example, to get a report on the number of users with data grouped by the device manufucturer and the name of the device model, use this request:

```httpget translate=no
GET /stat/v1/data?id=1111&metrics=ym:ge:users&dimensions=ym:ge:mobileDeviceBranding,ym:ge:mobileDeviceModel&limit=5 HTTP/1.1
Host: api.appmetrica.yandex.ru
Authorization: OAuth <your_token>
```

where `<your_token>` is an OAuth token that can be obtained using [instructions](../intro/authorization.md#get-oauth-token).

{% cut "Sample response" %}

```json translate=no
{

    "query": {
        "ids": [
            1111
        ],
        "dimensions": [
            "ym:ge:mobileDeviceBranding",
            "ym:ge:mobileDeviceModel"
        ],
        "metrics": [
            "ym:ge:users"
        ],
        "sort": [
            "-ym:ge:users"
        ],
        "date1": "2015-08-28",
        "date2": "2015-09-03",
        "limit": 5,
        "offset": 1

    },
    "data": [
        {
            "dimensions": [
                {
                    "name": "Apple"
                },
                {
                    "name": "iPad 4"
                }

            ],
            "metrics": [
                1240
            ]
        },
        {

            "dimensions": [
                {
                    "name": "Apple"

                },
                {
                    "name": "iPad mini 1G"
                }

            ],
            "metrics": [
                1236
            ]
        },
        {
            "dimensions": [
                {
                    "name": "Apple"
                },
                {
                    "name": "iPad Air"
                }
            ],
            "metrics": [
                948
            ]
        },
        {
            "dimensions": [
                {
                    "name": "Apple"
                },
                {
                    "name": "iPad 2"
                }
            ],
            "metrics": [
                866
            ]
        },
        {

            "dimensions": [
                {
                    "name": "Apple"
                },
                {
                    "name": "iPad 3"
                }
            ],
            "metrics": [
                661
            ]
        }
    ],
    "total_rows": 1163,
    "sampled": false,
    "sample_share": 1,
    "sample_size": 12258000,
    "sample_space": 12258000,
    "data_lag": 0,
    "totals": [
        13290
    ],
    "min": [
        661
    ],
    "max": [
        1240
    ]

}
```

{% endcut %}

To get the text of the query for API, use the **Export** menu in the AppMetrica interface. Open the report, configure a segment, time interval, grouping and click the **Export** button above the chart. Choose **Copy table API request** or **Copy chart API request** in the dropdown menu. For more information about exporting data, see [Working with reports](../../mobile-reports/index.md).

## Compatibility of dimensions and metrics {#comp}

The API supports several types of dimensions and metrics that use different prefixes:

- `ym:ge:` — Dimension or metric for any activity.
- `ym:ce:` — Indicates that your event was sent.
- `ym:c:` — Used in tracking reports to indicate a click.
- `ym:i:` — Used in tracking reports to indicate an app install.
- `ym:s:` — Used in Session dimensions.

You can't use different prefixes in the same request.

{% note info %}

You can specify a prefix other than the one in the request when you are using the `filters` parameter to segment the received data by dimension.

{% endnote %}

## Types of reports {#report-type}

Resulting data can be provided in the following formats:

{% list tabs %}

- Table

   All report levels and metrics are shown as a table.

   To display data as a table, use the [/stat/v1/data](data.md) method.

- Drill down

   Generating a single branch of a tree view report.

   To create branches, use the [/stat/v1/data/drilldown](drilldown.md) method.

{% endlist %}

## Format of reports

The API returns responses in UTF-8 encoding. Responses are in JSON or CSV format.

The format is specified in the request after the URL:

```
GET {{ api-url }}/stat/v1/data.**csv**?<counter_id>&<metrics>&<dimensions>
```

Since JSON is the default format, it can be omitted:

```
GET {{ api-url }}/stat/v1/data?<counter_id>&<metrics>&<dimensions>
```

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
