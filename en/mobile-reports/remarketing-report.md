# Remarketing

The Remarketing report contains information about [remarketing campaigns](*remarketing campaigns) that are launched to return an audience to your app. There is a special tracker type for remarketing campaigns. For more information, see [Creating a remarketing tracker](../mobile-tracking/add-remarketing-tracker.md).

The report displays data about the users that returned to the app ([re-engagement](*re-engagement)), as well as target events they have completed. AppMetrica counts re-engagements when a user runs the application after clicking on the tracking URL or re-engagement deeplink.

The report allows you to pull out certain users by defining [data segments](segmentation.md). You can apply only [user level](segmentation.md#users-segment) segmentation filters for the report.

{% cut "How it looks" %}

![](../../_images/remarketing-report-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

{% endcut %}

## Report period {#period}

The report is formed for a specific time period. The default period is one week.

{% include [period](_includes/period.md) %}

## Data for deeplinks {#deeplinks}

You can choose to display in the report the data for all [deeplinks](*deeplink) or for [re-engagement](*re-engagement) deeplinks only. 

![](../../_images/remarketing-report-deeplinks-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

A regular deeplink captures metrics only at the time of the first opening. The re-engagement deeplink tracks user actions in multiple sessions until another campaign changes its status.

The choice affects the calculation of metrics from the [Main metrics](#main-metrics) block. All other metrics are calculated only for re-engagement deeplinks.

## Dimensions {#group}

{% include notitle [origins-group](_includes/origins-group.md) %} 

{% include notitle [audience-group](_includes/audience-group.md) %}

{% include notitle [geo-group](_includes/geo-group.md) %}

{% include notitle [installs-group](_includes/installs-group.md) %}

{% include notitle [reengagement-group](_includes/reengagement-group.md) %} 

{% cut "Profile attributes" %}

{% include notitle [profile-attributes-system](_includes/profile-attributes-system.md) %} 

{% include notitle [profile-custom-group](_includes/profile-custom-group.md) %} 

{% endcut %}

To view the list of partner trackers, click on the partner's name in the report (when the data is grouped by media source). When the data is grouped by tracker, you can view the list of all the tracker parameters by clicking the tracker's name.

## Metrics {#measure}

{% note info "" %}

Metrics from the [Main metrics](#main-metrics) block are calculated depending on the [{#T}](#deeplinks) selector.

All other metrics are calculated only for re-engagement deeplinks.

{% endnote %}

The following metrics are available for analysis:

{#main-metrics}

{% cut "Main metrics" %}

- **Clicks**. The number of clicks that users made on the tracking link or re-engagement deeplink.
- **Users**. The number of users that followed the tracking link or re-engagement deeplink.
- **Click-to-deeplink conversion**. The conversion rate from click to deeplink.
- **Deeplinks**. 

{% endcut %}

{% include notitle [conversion-metrics](_includes/conversion-metrics.md) %} 

{% cut "Usage" %}

- **Sessions**. The number of user sessions for the entire time since re-engagement.
- **Loyal users**. {{ loyal-users }}
- **Retention**. {{ retention }}

{% endcut %}

{% cut "Metrics by events" %}

- **Events**. 
- **Users with event**. 
- **Events per user**.
- **Conversion rate by user**.

{% endcut %}       

{% include notitle [total-revenue-metrics](_includes/total-revenue-metrics.md) %} 

{% include notitle [in-app-revenue-metrics](_includes/in-app-revenue-metrics.md) %} 

{% include notitle [in-app-purchase-metrics](_includes/in-app-purchase-metrics.md) %} 

{% include notitle [ad-revenue-metrics](_includes/ad-revenue-metrics.md) %} 

{% include notitle [ecommerce-metrics](_includes/ecommerce-metrics.md) %} 

The report interface also displays the following:

- The color key of metrics on the chart. Use it to show or hide a metric on the chart.
- The traffic source selection for the chart. Enables you to choose which metric to show on the chart: clicks, re-engagements, or conversion.

## Events {#events}

You can add up to 5 events to the report to monitor the information about an event in the context of the traffic source. Sending an event should be configured when the [SDK is initialized](../common/quick-start.md).

To show the event information:

1. Select the metric in the **Metrics by events**.

1. Click the **Select value** link — you will see the events list.

1. Select the events and push **Apply**.

{% cut "How to add custom events" %}

![](../../_images/remarketing-events-{{locale}}.png)

{% endcut %}

## Data export {#export}

{% include notitle [export](_includes/export-api.md) %}

## See also {#learn-more}

- [How do I enable user location sending?](../troubleshooting/troubleshooting.md#region)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*remarketing campaigns]: An ad campaign aimed at getting users to come back to an app they previously installed. For more information, see [Creating a remarketing tracker](../mobile-tracking/add-remarketing-tracker.md).

[*deeplink]: {{ deeplink }}

[*re-engagement]: {{ re-engagement }}
