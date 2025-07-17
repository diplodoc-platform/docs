# Cohort analysis

This report lets you select groups of users ([cohorts](*cohorts)) and track metrics of completed events for the selected period of time in the cohort. You can use the report to assess the quality of traffic sources and the quality of the audience produced by media sources. Also, the report allows you to analyze how many users have completed an event in the selected cohort. In this way, you can calculate the users from a particular partner.

The report allows you to pull out certain users by defining [data segments](segmentation.md). For example, you can create a segment of users who made a purchase in a certain region. With data segments, you can also set the period of the target action for your report.

To build a report, you need to choose the time period, the audience segment, the grouping type, the cohort size (a date range such as a day, week, or month), and the event to analyze.

By default, the report shows dynamics of the "Session start" event after the app was installed (day 0), on the following day (day 1), a day later (day 2), and so on.

## Grouping data {#group}

The data in the report can be grouped by:

- Installation date.
- Media source.
- Tracker and tracking URL parameters.
- Country.
- Region.
- City.
- Operating system.
- Gender.
- Age.
- App version

To exclude negligible partners, trackers, or tracking URL parameters, specify the minimum size of the cohort. This enables you to focus on the key metrics.

## Metrics {#measure}

_Events_, _Users_, _Total Revenue_, _In-App Revenue_, _Ad Revenue_, _Paying users_, and _Purchases_ are available for analysis.

{% list tabs %}

- Events

   ![](../../_images/cohort-events-{{ locale }}.png){style="max-width: 600px;"}

   **Average number of events per user**
   :   This metric is calculated as the ratio of the cumulative sum of events on Day N to the number of users in the cohort.

   **Cumulative sum of events**
   :   This metric is calculated for Day N as the total number of events for that day and all previous days in the selected period.

   {% include notitle [cohort](_includes/cohort.md) %}

- Users

   ![](../../_images/cohort-users-{{ locale }}.png){style="max-width: 600px;"}

   **Percentage of users completing the event on Day N**
   :   This metric is calculated as the ratio of the cumulative sum of unique users on Day N to the total number of users in the cohort.

   **Cumulative sum of unique users completing the event on Day N**
   :   This metric is calculated for Day N as the total number of unique users for that day and all previous days in the selected period. If the user has completed the event several times in the selected period, the event is counted only once.

   {% include notitle [cohort](_includes/cohort.md) %}

- Total Revenue

   {{ total-revenue}} Learn more about currency [conversions](../data-collection/about-revenue.md#currency).

   **ARPU**
   :   This metric is calculated as the ratio of cumulative revenue on Day N to the number of users in the cohort.

   **Total revenue**
   :   Total revenue for Day N is calculated as the total revenue for that day and all previous days in the selected period.

   {% include notitle [cohort](_includes/cohort.md) %}

- In-App Revenue

   {{ in-app-revenue }} Learn more about currency [conversions](../data-collection/about-revenue.md#currency).

   **ARPU**
   :   This metric is calculated as the ratio of cumulative revenue on Day N to the number of users in the cohort.

   **Total revenue**
   :   Total revenue for Day N is calculated as the total revenue for that day and all previous days in the selected period.

   {% include notitle [cohort](_includes/cohort.md) %}

- Ad Revenue

   {{ ad-revenue-new }}

   **ARPU**
   :   This metric is calculated as the ratio of cumulative revenue on Day N to the number of users in the cohort.

   **Total revenue**
   :   Total revenue for Day N is calculated as the total revenue for that day and all previous days in the selected period.

   {% include notitle [cohort](_includes/cohort.md) %}

- Paying Users

   {{ paying-users }}

   **Percentage of paying users**
   :   This metric is calculated as the ratio of the number of paying users on Day N to the total number of users in the cohort.

   **Number of paying users**
   :   The total number of paying users for Day N and all previous days in the selected period.

   {% include notitle [cohort](_includes/cohort.md) %}

- Purchases

   {{ purchases }}

   **Purchases per user**
   :   This metric is calculated as the ratio of the number of purchases on Day N to the number of users in the cohort.

   **Number of purchases**
   :   The total number of purchases for Day N and all previous days in the selected period.

   {% include notitle [cohort](_includes/cohort.md) %}

{% endlist %}

## Data export {#export}

You can export data by choosing an item from the **Export** dropdown list above the chart. The data is exported based on the selected report settings: segmentation, grouping, and time period.

The dropdown list contains the following elements:

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-reports/export-data-cohorts.png){style="border: solid 1px #cccccc; max-width: 800px;"}

- **Cohorts as CSV** — Exports the data from the table in the `CSV` format.
- **Chart as PNG** — Exports the chart image in the `PNG` format.

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*cohorts]: A group of users who share a characteristic and the date of when they completed a target event. The shared characteristic may be an app install or a target event.
