# Events

The report displays statistics on custom events. You can set up sending these events in the app. For more information, see [Sending your own events](../data-collection/about-events.md).

## The report will help you: {#resolve-tasks}

- Determine the reach of app features and how popular they are.
- Compare the behavior of different user groups.
- Evaluate the frequency of using features within sessions.
- [Analyze nested event parameters](#analytics).

## General settings {#how-to}

1. Choose the time period and audience segment. By default, the report shows events for the week grouped by days.

   The event time is the moment when the event is generated on the user's device in the time zone specified in the app settings.

   {% note info "" %}

   {% include [period](_includes/period.md) %}

   {% endnote %}

2. You can select specific users for the report using [segmentation](segmentation.md).
3. You can set up [dimensions](#group) and [metrics](#metrics) in the report.

## Configuring a chart with a choice of metrics {#metrics-in-graph}

{% include notitle [metrics-in-graph](_includes/metrics-in-graph.md) %}

## Selecting dimensions and metrics {#groups-metrics}

{% include notitle [groups-metrics](_includes/groups-metrics-old.md) %}

### Dimensions {#group}

{% note alert "" %}

Dimensions by parameter are only available for nesting level 1. For more information about nesting levels, see an [example of events](../data-collection/about-events.md).

{% endnote %}

{% include notitle [audience-group](_includes/audience-group.md) %}

{% include notitle [geo-group](_includes/geo-group.md) %}

{% include notitle [events-group](_includes/events-group.md) %}

{% include notitle [date-event-group](_includes/date-event-group.md) %}

{% include notitle [app-group](_includes/app-group.md) %}

### Metrics {#measure}

{% note alert "" %}

Metrics by parameter are only available for nesting level 1. For more information about nesting levels, see an [example of events](../data-collection/about-events.md).

{% endnote %}

{% cut "Events metrics" %}

- **Events**.
- **Unique parameter values**. The number of unique values of the selected event parameter.
- **Sum of parameter values**. The sum of values of the selected event parameter. A missing value or parameter in the event during the calculation is interpreted as 0.
- **Average parameter value**. The sum of values of the selected event parameter divided by the number of events. A missing value or parameter is interpreted as 0.
- **Median parameter value**. The median value of the selected event parameter. A missing value or parameter in the event during the calculation is interpreted as 0.

{% endcut %}

{% cut "User metrics" %}

- **Users**. The number of users with the event.
- **Events per user**. The ratio of the number of events to the total number of app users.
- **% of all users**. The percentage of users with the event out of the total number of app users.
- **Unique parameter values per user**. The ratio of the number of unique values of the selected event parameter to the number of users with the event. A missing value or parameter in the event during the calculation is interpreted as 0.
- **Sum of parameter values per user**. The ratio of the sum of values of the selected event parameter to the number of users with the event. A missing value or parameter in the event during the calculation is interpreted as 0.

{% endcut %}

{% cut "Session metrics" %}

- **Sessions with events**. The number of sessions in which an event occurred.
- **Events per session**. The ratio of the number of events to the number of sessions.
- **Unique parameter values per session**. The ratio of the number of unique values of the selected event parameter to the number of sessions with the event. A missing value or parameter in the event during the calculation is interpreted as 0.
- **Sum of parameter values per session**. The ratio of the sum of values of the selected event parameter to the number of sessions with events. A missing value or parameter in the event during the calculation is interpreted as 0.

{% endcut %}

<!-- ![](../../_images/events-report-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 800px;"} -->

## Analysis of event parameters {#analytics}

**Analysis of nested event parameters**
:   You can use the report to analyze nested event parameters. Along with the audience metrics, the following aggregations of parameter values are available: their sum, average and median values, and the number of unique values. These metrics are helpful in scenarios such as:
    - Comparing events by the selected parameter.
    - Calculating the amount of resources used by players.
     The sum and number of unique parameter values are also available in terms of users and sessions.

**Grouping by a specific event parameter**
:   You can set up groupings (dimensions) by a specific event parameter in the report. This is helpful for:
    - Filtering report data.
    - Scenarios such as comparing events and calculating statistics for all events with the desired parameter.

## Adding a comment {#comments}

To make it easier to navigate reports, you can add comments to events. To do this, follow these steps:

1. Find the desired event in the **Settings** → **Events** section.

   {% note info %}

   You can go to event settings from the report interface. To do this, click the ![]({{ cog }}) icon next to the name of the event.

   {% endnote %}

2. Leave a comment.
3. Go back to the **Events** report and refresh the page.

## Disabling events {#turn-off}

To disable event collecting and remove it from the report, follow these steps:

1. Find the desired event in the **Settings** → **Events** section.

   {% note info %}

   You can go to event settings from the report interface. To do this, click the ![]({{ cog }}) icon next to the name of the event.

   {% endnote %}

2. In the **Events collection** block, select the **Collecting disabled** mode.

## Data export {#export}

{% include notitle [export-api](_includes/export-api.md) %}

## Troubleshooting {#problems}

{% cut "For iOS devices, events fall into background sessions" %}

{#session-background}

Events that are sent immediately after initializing the library are counted in background sessions. To make sure that events belong to user sessions, initialize the library with the `handleActivationAsSessionStart` option enabled.

{% endcut %}

## Frequently asked questions {#faq}

{% include notitle [description](../_includes/faq.md#ua-events) %} 

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
