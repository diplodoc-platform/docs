# In-app and Ad Revenue

The **In-app and Ad Revenue** report displays the main metrics that are related to your app's revenue from in-app purchases or advertising monetization.

To collect statistics on revenue, configure sending in the app. For more information, see [{#T}](../data-collection/about-revenue.md#send-revenue).

## Tasks that the report helps to solve {#resolve-tasks}

- Evaluate the success of new app features using the [ARPU](*ARPU) metric.
- Evaluate the user reaction to price changes using the [ARPPU](*ARPPU) metric.
- Evaluate popular products in the app.
- Evaluate the geography of purchases using a dimension with data grouped by city.
- Evaluate the profitability of individual advertising networks and blocks.

## General settings {#how-to}

Choose the time period and audience segment. By default, the report shows data for the week grouped by days. The time in the report is the beginning of the session on the user's device in the time zone specified in the app settings.

{% note info "" %}

{% include [period](_includes/period.md) %}

{% endnote %}

{% include notitle [segments](_includes/segments.md) %}

You can set up [dimensions](#group) and [metrics](#metrics) in the report.

## Configuring a chart with a choice of metrics {#metrics-in-graph}

{% include notitle [metrics-in-graph](_includes/metrics-in-graph.md) %}

## Selecting dimensions and metrics {#groups-metrics}

{% include notitle [groups-metrics](_includes/groups-metrics.md) %}

### Dimensions {#group}

{% include notitle [audience-group](_includes/audience-group.md) %}

{% include notitle [geo-group](_includes/geo-group.md) %}

{% include notitle [total-revenue-group](_includes/total-revenue-group.md) %}

{% include notitle [in-app-revenue-group](_includes/in-app-revenue-group.md) %}

{% include notitle [ad-revenue-group](_includes/ad-revenue-group.md) %}

{% include notitle [param-events-group](_includes/param-events-group.md) %}

{% include notitle [date-event-group](_includes/date-event-group.md) %}

{% include notitle [app-group](_includes/app-group.md) %}

{% include notitle [profile-attributes](_includes/profile-attributes.md) %}

You can drill down the data if you select the following dimensions: **region**, **country**, or **payload**. Use the ![](../../_images/tab-flat-tree.png =60x) button to enable the drilldown mode.

### Metrics {#measure}

{% include notitle [total-revenue-metrics](_includes/total-revenue-metrics.md) %} 

{% include notitle [in-app-revenue-metrics](_includes/in-app-revenue-metrics.md) %} 

{% include notitle [in-app-purchase-metrics](_includes/in-app-purchase-metrics.md) %} 

{% include notitle [ad-revenue-metrics](_includes/ad-revenue-metrics.md) %} 

{% include notitle [event-params-metrics](_includes/event-params-metrics.md) %} 

{% note info "Validated Revenue tracking" %}

With validation enabled, all In-App Revenue metrics are counted based on validated purchases and purchases passed without parameters for validation. For invalid purchases, **Invalid revenue** and **Users with invalid revenue**  metrics are counted.

{% endnote %}

The report interface also displays the following:

- The color key of metrics on the chart. Use it to show or hide a metric on the chart.

     {% note info "" %}

     This item is not displayed when the data is grouped by date.

     {% endnote %}

- Table structure selector ![](../../_images/tab-flat-tree.png =60x)

<!-- ![](../../_images/revenue-report-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 800px;"} -->

## Data export {#export}

{% include notitle [export-api](_includes/export-api.md) %}

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*ARPU]: {{ arpu }}

[*ARPPU]: {{ arppu }}
