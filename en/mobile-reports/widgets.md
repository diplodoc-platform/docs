# Widgets

A widget is a tile that displays data from a specific report; clicking the widget title takes you directly to that report.

Widgets can visualize data as charts, tables, metrics, or multiwidgets. Multiwidgets combine metrics and charts in a single view. You can switch between these views:

![](../../_images/widget-types-{{ locale }}.png){style="border: solid 1px #cccccc; max-width: 500px;"}

You can add both [preset](#preset) and [custom](#custom) widgets.

## Preset widgets {#preset}

AppMetrica has preset widgets you can add to a workspace:

#|
|| **Widget** | **Report** | **Topic** | **Metric — Dimension** ||
|| **Pushes sent** | [Push campaigns](push-campaign.md) | Marketing | Sent — Total for the period ||
|| **Pushes delivered** | [Push campaigns](push-campaign.md) | Marketing | Delivered — Total for the period ||
|| **Pushes opened** | [Push campaigns](push-campaign.md) | Marketing | Opened — Total for the period ||
|| **Clicks**

The number of clicks on AppMetrica tracking links grouped by partner. | [User Acquisition](user-acquisition-report.md) | Marketing | Clicks — Top 5 Partners ||
|| **Installs**

New installs grouped by partner. | [User Acquisition](user-acquisition-report.md) | Marketing | Installs — Top 5 partners ||
|| **Click-to-install rate**

The ratio of installations to clicks on tracking links grouped by partner. | [User Acquisition](user-acquisition-report.md) | Marketing | Conversion — Top 5 Partners ||
|| **Fraud dynamics — Installs** | [User Acquisition](user-acquisition-report.md) | Marketing | Installs — Fraud assessment, trackers ||
|| **Fraud dynamics — Scores** | [User Acquisition](user-acquisition-report.md) | Marketing | Installs — Fraud assessment, trackers ||
|| **Fraud dynamics — Partners** | [User Acquisition](user-acquisition-report.md) | Marketing | Installs — Fraud assessment, trackers ||
|| **Fraud dynamics — Trackers** | [User Acquisition](user-acquisition-report.md) | Marketing | Installs — Fraud assessment, trackers ||
|| **Score distribution** | [User Acquisition](user-acquisition-report.md) | Marketing | Installs — Fraud assessment, trackers ||
|| **Audience** | [Audience](audience-report.md) | Product | Audience — Total for the period ||
|| **New users** | [Audience](audience-report.md) | Product | New users, Days of inactivity - 7 — Day ||
|| **Inactive audience** | [Audience](audience-report.md) | Product | New users, Days of inactivity -7 — Day ||
|| **Timespent per user**

The ratio of the total duration of sessions to the number of users. Learn more about [session tracking](engagement-report.md). | [Engagement](engagement-report.md) | Product | Timespent per user — Average for the period ||
|| **Average session length**

The ratio of the total duration of sessions to the number of sessions. Learn more about [session tracking](engagement-report.md). | [Engagement](engagement-report.md) | Product | Average session length — Average for the period ||
|| **Sessions per user**

The ratio of the number of sessions to the number of users. Learn more about [session tracking](engagement-report.md). | [Engagement](engagement-report.md) | Product | Sessions per user — Average for the period ||
|| **Funnels** | [Funnels](funnels-report.md) | Product | ||
|| **Retention**

The percentage of users who returned to the app on a specific day, week, or month. | [Retention](retention-report.md) | Product | Retention — Values on specific days depending on the duration of the selected period ||
|| **Rolling Retention**

The percentage of users who returned to the app on a specific day, week, or month, assuming they could have potentially returned during the preceding time period. | [Retention](retention-report.md) | Product | Rolling Retention — Values on specific days depending on the duration of the selected period ||
|| **Retention Dynamics**

The chart shows the change in Retention of specific days (1, 3, 7, and so on) over time. | [Retention](retention-report.md) | Product | Retention Dynamics — Values on specific days depending on the duration of the selected period ||
|| **Ecom orders**

Number of "Purchase" e-commerce events. | [E-commerce](ecommerce-report.md) | Monetization | Purchases — Amount for the period ||
|| **Ecom Orders per user**

The ratio of the number of "Purchase" e-commerce events to the number of users who triggered this event. | [Ecommerce](ecommerce-report.md) | Monetization | Purchases per user — Average for the period ||
|| **Ecom paying users**

Number of users with a "Purchase" e-commerce event. | [E-commerce](ecommerce-report.md) | Monetization | Paying users — Amount for the period ||
|| **Ecom revenue**

Total revenue from "Purchase" e-commerce events. Learn more about [converting currencies](../data-collection/about-revenue.md#currency). | [Ecommerce](ecommerce-report.md) | Monetization | Revenue — Amount for the period ||
|| **In-app paying users**

The number of users who made an in-app purchase. | [In-app and Ad Revenue](revenue-report.md) | Monetization | Paying users — Amount for the period ||
|| **In-app Purchases**

The number of in-app purchases. | [In-app and Ad Revenue](revenue-report.md) | Monetization | Purchases — Amount for the period ||
|| **In-app purchases per user**

The ratio of the number of in-app purchases to the number of users who made an in-app purchase. | [In-app and Ad Revenue](revenue-report.md) | Monetization | Purchases per user — Average for the period ||
|| **In-app revenue**

The total revenue from in-app purchases. Learn more about [converting currencies](../data-collection/about-revenue.md#currency). | [In-app and Ad Revenue](revenue-report.md) | Monetization | Revenue — Amount for the period ||
|| **In-app ARPU**

Revenue from in-аpp purchases per user. It is calculated as the ratio of the total app revenue to the number of users per day, week, or month. Learn more about [converting currencies](../data-collection/about-revenue.md#currency). | [In-app and Ad Revenue](revenue-report.md) | Monetization | ARPU — Average for the period ||
|| **In-app ARPPU**

Revenue from in-аpp purchases per paying user. It is calculated as the ratio of the total app revenue to the number of paying users per day, week, or month. Learn more about [converting currencies](../data-collection/about-revenue.md#currency). | [In-app and Ad Revenue](revenue-report.md) | Monetization | ARPPU — Average for the period ||
|| **In-app AOV**

Average revenue from one in-app purchase. Learn more about [converting currencies](../data-collection/about-revenue.md#currency). | [In-app and Ad Revenue](revenue-report.md) | Monetization | AOV — average for the period ||
|| **App versions** |  | Technical reports | App versions — Top 5 ||
|| **Operating systems** |  | Technical reports | Operating systems — Top 5 ||
|| **Device models** |  | Technical reports | Device models — Top 5 ||
|| **Android Errors and users with errors** | [Errors](crashes-and-errors.md) | Crashes and errors | Errors and users with errors — Sessions and users ||
|| **iOS Errors and users with errors** | [Errors](crashes-and-errors.md) | Crashes and errors | Errors and users with errors — Sessions and users ||
|#

## Custom widgets {#custom}

You can create a custom widget from any report or using the widget builder in your workspace.

{% list tabs %}

- From a report

  1. Open the desired report, configure it for your needs, and save it. Learn more about [saved reports](save-reports.md).

  1. Add the saved report to your workspace as a widget.

      1. Click **{{ to-workspace }}** in the upper-right corner to open the [widget builder](#builder).

      1. The widget settings are pre-filled based on the metrics, dimensions, and segments you selected in the report. Review the settings and make any changes if necessary.

      1. Click **{{ create }}**.

- In a workspace

  1. Open the workspace where you want to add the widget.

  1. In the upper-right corner, click **{{ button-add }}** → **{{ new-widget }}** to open the [widget builder](#builder).

  1. Fill in the widget settings and click **{{ create }}**.

{% endlist %}

Once the widget is created, you can update its settings by clicking ![](../../_images/dots.svg) → **{{ edit }}**. You can change any settings except for the data source report. To use a different data source, you'll need to create a new widget.

## Widget builder {#builder}

Using the widget builder, you can create widgets to display data in any breakdown or format you need.

{% note info "" %}

Depending on the report used as the data source, the widget builder may show additional settings.

{% endnote %}

1. Enter the name of the widget.

1. If you launch the widget builder from a report, choose the workspace where you want to add the new widget.

    If you start from a workspace, select the report you want to use as the widget’s data source.

1. Select the widget type: chart, table, metric, or multiwidget. A multiwidget contains both metrics and charts.

1. In the **{{ show-in-widget }}** field, choose the dimensions to group data in the widget:

    - **{{ total-or-average }}**: No dimensions; only the total sum and average value are shown for metrics.

    - **{{ automatically-selected-dimension-values }}**: Dimension values are selected automatically.

    - **{{ manually-selected-dimension-values }}**: Enter dimension values manually.

    You can apply these options to one or more metrics, depending on the selected widget type.

1. Select at least one metric from the report.

1. If you chose **{{ automatically-selected-dimension-values }}** or **{{ manually-selected-dimension-values }}** in the **{{ show-in-widget }}** field, make sure to specify at least one dimension.

    If you select **{{ manually-selected-dimension-values }}**, an extra field appears where you can enter the dimension values.

1. Select any [segments set up for the report](segment-creation.md) if needed.

1. Click **{{ create }}**.

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
