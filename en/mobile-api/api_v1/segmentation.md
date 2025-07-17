# Segmentation

All methods in the Reporting API can return results for each separate data segment, as well as for the entire site. To set the segment, use the `filters` parameter.

You can segment a request by dimensions and metrics. The dimension or metric does not have to be specified in the request.

Dimension filters are applied to source (ungrouped) data, and metric filters are applied to grouped rows in the result.

To set a filter in the request URL, use [URL encoding](http://ru.wikipedia.org/wiki/URL#.D0.9A.D0.BE.D0.B4.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_URL).

## Filter format {#format}

```xml translate=no
attribute operator 'value'
```

where

- `attribute` is the dimension or metric, For example, `ym:ge:mobileDeviceModel` or `ym:ge:users`.
- `operator` is the [filtration operator](../api_v1/relations/relations.md) and specifies which type of filtration to apply. For example, `==`.
- `value` is the comparison value. In the string with the value, the symbols `'` and `\` must be escaped using a `\`.

In addition, the following limits are imposed: a maximum of 10 unique dimensions and metrics, 20 separate filters, and 2000 characters in the filter string.

For example, to get data only for sessions from Moscow, use this filter:

```xml translate=no
filters=ym:ge:regionCity=='Moscow'
```

Different filtration operators are available for different dimensions (for example, see the Relations column in the [Application](attributes/mobmet_events/app.md) section).

To combine filters in a request, use the `AND`, `OR`, and unary `NOT` operators:

```xml translate=no
&metrics=ym:ge:users&dimensions=ym:ge:age&filters=NOT(ym:ge:age!=18)
```

```xml translate=no
ym:ge:regionCity=='Moscow' OR ym:ge:regionCity=='St. Petersburg'
```

You can also set priority using parentheses:

```xml translate=no
(ym:ge:regionCity=='Moscow' OR ym:ge:regionCity=='St. Petersburg') AND ym:ge:gender=='male'
```

You can combine dimension filters and metric filters, but only at the top level (outside of parentheses) and only using the `AND` operator.


{% note info %}

The request language (the `lang` parameter) affects the filter values. We recommend always specifying this parameter.

{% endnote %}

## Example using segmentation {#example}

**Number of users based on the region**

`dimensions=ym:ge:mobileDeviceModel`

`metrics=ym:ge:users`

`filters=ym:ge:regionCityName=='Moscow'`

{% list tabs %}

- cURL

   ```bash translate=no
   curl -X GET \
     'https://api.appmetrica.yandex.ru/stat/v1/data?id=1111&metrics=ym:ge:users&dimensions=ym:ge:mobileDeviceModel&filters=ym:ge:regionCityName==%27Москва%27' \
     -H 'Authorization: OAuth <your_token>'
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](../intro/authorization.md#get-oauth-token).

- HTTP

   ```http translate=no
   GET /stat/v1/data?id=1111&metrics=ym:ge:users&dimensions=ym:ge:mobileDeviceModel&filters=ym:ge:regionCityName=='Москва' HTTP/1.1
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
