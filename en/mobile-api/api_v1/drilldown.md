# Drill down

Allows you to generate a multi-level (tree view) report. Each level corresponds to a single dimension.

A request to the `drilldown` method returns one sublevel for the specified parent level. The parent level is specified in the `parent_id` parameter. To get data for the top level, send a request without the `parent_id` parameter.

To get data for nested levels, you must specify the path from the root. The path is formed from values of the `id` field for the `dimension` parameter. If the id field is omitted, specify the `name` field.

## Request format {#request}

```
GET {{ api-url }}/stat/v1/data/drilldown
  ? ids=<int,int,...>
  & metrics=<string>
  & [accuracy=<string>]
  & [callback=<string>]
  & [date1=<string>]
  & [date2=<string>]
  & [dimensions=<string>]
  & [filters=<string>]
  & [group=<group_type>]
  & [id=<integer>]
  & [include_undefined=<boolean>]
  & [lang=<string>]
  & [limit=<integer>]
  & [offset=<integer>]
  & [parent_id=<string>]
  & [pretty=<boolean>]
  & [sort=<string>]
```

#|
|| `ids`* | Comma-separated list of counter numbers. Used instead of the `id` parameter. ||
|| `metrics`* | Comma-separated list of metrics.

Limit: 20 metrics per request. ||
|| `accuracy` | Accuracy of results. Allows you to manage sampling (the number of visits used to calculate the final value).
Default value: `medium`. ||
|| `callback` | Callback function that processes the API response. ||
|| `date1` | Start date of the report period in YYYY-MM-DD format. You can also use the values: `today`, `yesterday`, `ndaysAgo`.

Default value: `6daysAgo`. ||
|| `date2` | End date of the report period in the format YYYY-MM-DD. You can also use the values: `today`, `yesterday`, `ndaysAgo`.

Default value: `today`. ||
|| `dimensions` | Comma-separated list of dimensions.

Limit: 10 dimensions per request. ||
|| `filters` | [Segmentation filter](segmentation.md).

Limit: Maximum of 10 unique dimensions and metrics, 20 separate filters, and 10,000 characters per filter string. ||
|| `group` | Grouping data by time.
Default value: `week`.

Acceptable values:

- `all` — The time range is not broken down.
- `hours` — The time range is divided into intervals of several hours.
- `auto` — Automatic mode.
- `week` — The time range is divided into weeks.
- `month` — The time range is divided into months.
- `hour` — The time range is divided into hourly intervals.
- `year` — The time range is divided into years.
- `minutes` — The time range is divided into intervals of a certain number of minutes.
- `day` — The time range is divided into days.
- `dekaminute` — The time range is divided into 10-minute intervals.
- `quarter` — The time range is divided into quarters.
- `minute` — The time range is divided into one-minute intervals. ||
   || `id` | The tag number. Obsolete. Use `ids`. ||
   || `include_undefined` | Outputs rows that don't have defined dimension values. This only affects the first dimension. Disabled by default. ||
   || `lang` | Language. ||
   || `limit` | Number of items on the results page.

Limit: 10000.

Default value: 100. ||
|| `offset` | Index of the first row of requested data, starting from 1.
Default value: 1. ||
|| `parent_id` | Row for expanding further. Consists of a JSON list of keys. ||
|| `pretty` | Specifies the formatting for results. To use formatting, set the value to `true`.
The default value is `false`. ||
|| `sort` | Comma-separated list of dimensions and metrics to use for sorting.  By default, sorting occurs in ascending order. To sort data in descending order, put the <q>-</q> sign before the dimension or metric. ||
|#

## Response format {#response}

```json translate=no
{
    "total_rows" :  < long > ,
    "sampled" :  < boolean > ,
    "sample_share" :  < double > ,
    "sample_size" :  < long > ,
    "sample_space" :  < long > ,
    "data_lag" :  < int > ,
    "query" : {
        "ids" : [  < int > , ... ],
        "dimensions" : [  < string > , ... ],
        "metrics" : [  < string > , ... ],
        "sort" : [  < string > , ... ],
        "date1" :  < string > ,
        "date2" :  < string >,
        "filters" :  < string > ,
        "limit" :  < integer > ,
        "offset" :  < integer >
    },
    "totals" : [  < double > , ... ],
    "min" : [  < double > , ... ],
    "max" : [  < double > , ... ],
    "data" : [ {
        "dimension" : {
            "key_1" :  < string > ,
            "key_2" : ...
        },
        "metrics" : [  < double > , ... ],
        "expand" :  < boolean >
    }, ... ]
}
```

| Parameters | Description |
| ----- | ----- |
| `total_rows` | The total number of rows in the response. |
| `sampled` | Sampling flag. Indicates whether sampling was applied. Possible values: `true`, `false`. |
| `sample_share` | Percentage of data used for the calculation. Available values range from 0 to 1. |
| `sample_size` | Number of rows in the requested data. |
| `sample_space` | Number of data rows. |
| `data_lag` | Delay in updating data, in seconds. |
| `query` | Original request. Contains the request parameters, including detailed parameters from the template and parameters for attribute parametrization. |
| `totals` | Total results for metrics across the entire dataset (with filtration). |
| `min` | Minimum results for metrics among keys output. |
| `max` | Maximum results for metrics among keys output. |
| `data` | Response rows. An array in which each item is a single row of the result. |
| `query.ids` | Counter IDs. |
| `query.dimensions` | Array of dimensions. |
| `query.metrics` | Array of metrics. |
| `query.sort` | Array of sortings. |
| `query.date1` | Start date of the report period in the format YYYY-MM-DD. |
| `query.date2` | End date of the report period in the format YYYY-MM-DD. |
| `query.filters` | Segmentation filter. |
| `query.limit` | Number of items on the results page. |
| `query.offset` | Index of the first row of requested data, starting from 1. |
| `data.dimension` | Dimension value for the specified level of the tree. For example, the second tree level is set (the `parent_id` array is one ID long). In this case, the field contains the value of the second dimension in the request. |
| `data.metrics` | Array of metric values for this row. The values in this array are numbers or `null`. |
| `edata.xpand` | Indicates whether to expand this row to the next level of the tree. |

## Sample request {#example}

{% list tabs %}

- cURL

   ```bash translate=no
   curl -X GET \
     '{{ api-url }}/stat/v1/data/drilldown?ids=1111&metrics=ym:ge:users' \
     -H 'Authorization: OAuth <your_token>'
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../intro/authorization.md#get-oauth-token).

- HTTP

   ```http translate=no
   GET /stat/v1/data/drilldown?ids=1111&metrics=ym%3Age%3Ausers HTTP/1.1
   Host: api.appmetrica.yandex.ru
   Authorization: OAuth <your_token>
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../intro/authorization.md#get-oauth-token).

{% endlist %}

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
