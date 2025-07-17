# Retention Analysis

This report shows the change in the percentage of users returning to the app over time. For instance, you can estimate:

- User demand for various features of the application.
- How application updates affected retention.
- The user's LTV in the application.

The report allows you to pull out certain users by defining [data segments](segmentation.md). For example, you can create a segment of users who made a purchase in a certain region. With data segments, you can also set the period of the target action for your report.

To build a report, you need to choose the time period, the audience segment, the grouping type, the cohort size (a date range such as a day, week, or month), and the metric to analyze.

By default, the report shows changes in _Retention_ after the app was installed (day 0), on the following day (day 1), a day later (day 2), and so on. This report will show exactly when users start losing interest in the app.

## Grouping data {#group}

Grouping allows you to evaluate metrics such as the effectiveness of the advertising partner, campaign performance, and the impact of updates on retention.

The data in the report can be grouped by:

- Installation date.
- Media source.
- Tracker and tracking URL parameters.

To exclude negligible partners, trackers, or tracking URL parameters, specify the minimum size of the cohort. This enables you to focus on the key metrics.

## Metrics {#measure}

**Retention**, **Rolling Retention** and **Retention Dynamics** are available for analysis.

{% list tabs %}

- Retention

   {{ retention }}

   ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-reports/retention.png)

   The example above shows the actions of four different users over one week:

   - On Day 0, all 4 users installed the application, so the retention metric is 100%.
   - On the next day after the installation (Day 1), only 2 out of 4 users opened the app again. The retention metric is 50%.
   - On the fourth day after the installation (Day 4), none of these 4 users opened the app. The retention metric is 0%.

   ![](../../_images/retention-metrics-ui-{{ locale }}.png){style="max-width: 500px;"}

   The following metrics are displayed in the report:

   - The color key of metrics on the chart. Enables you to show or hide each metric on the chart.
   - Grouping (by date, partner, tracker, and tracking URL parameters).
   - The total number of users in the cohort for the specified period.
   - The Retention metric value.
   - The number of users who returned to the app on Day N.

- Rolling Retention

   The percentage of users who installed the app during a given day, week, or month (the reference period) and then returned to the app during a specific day, week, or month, assuming they could have potentially returned during the preceding time period. These users are not interpreted as lost (inactive) until the last time they start the app.

   To better understand how Rolling Retention works, imagine a user who first opened the app on the day of installation (the reference day), and next opened it on the fourth day after installing. This user is counted as active on the fourth day and for all the previous days, as well. Even though it took the user four days to come back to the app, this was always a possibility during that time.

   ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-reports/retention-rolling.png)

   The example above shows the actions of four different users over one week:

   - On Day 0, all 4 users installed the application, so the rolling retention metric is 100%.
   - On the next day after the installation (Day 1), only 2 out of 4 users opened the app again. But the other 2 users will return to the application during the selected period (one week), so it is assumed that they were intending to return to the app. The rolling retention metric is still 100%.
   - On the fourth day after the installation (Day 4), none of the 4 users returned to the app, but 2 users will return during the selected period. The rolling retention metric is 50%.

   ![](../../_images/rolling-retention-metrics-ui-{{ locale }}.png){style="max-width: 500px;"}

   The following metrics are displayed in the report:

   - The color key of metrics on the chart. Enables you to show or hide each metric on the chart.
   - Grouping (by date, partner, tracker, and tracking URL parameters).
   - The total number of users in the cohort for the specified period.
   - The Rolling Retention metric value.
   - The number of users who returned to the app on Day N.

- Retention Dynamics

   The change in the percentage of users who returned to the app on a specific day, week, or month after installation in the specified time period. This metric allows you to track the Retention metric over time.

   The data is grouped only by the date of installation. 

   ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-reports/retention-dynamics.png)

   The example above shows the actions of four different users over one week. Users are grouped by the date of installation: the first group installed the app earlier than the second one. The figure shows the following:

   - On Day 0, all 4 users installed the application, so the Retention metric is 100% for both groups, despite different installation dates.
   - On the next day after the installation (Day 1, which is outlined with a dotted line), 1 user from the first group and none from the second group returned to the app. The Retention metric is 50% for the first group, and 0% for the second. The installation dates are different, and you can track changes in the Retention metric for the specified period after the installation.
   - On the sixth day after the installation (Day 6), neither of the 2 users from the first group returned to the app. For the second group, the metric is not available: there is no data to calculate the Retention metric.

   ![](../../_images/retention-dynamics-metrics-ui-{{ locale }}.png){style="max-width: 500px;"}

   The following metrics are shown in the report:

   - The color key of metrics on the chart. Enables you to show or hide each metric on the chart.
   - The number of the day since the first user session (Day 1, Day 2, etc.).
   - The date of the first user session.
   - The Retention metric value.
   - The number of users who returned to the app on Day N.

{% endlist %}

{% cut "Retention Dynamics changing" %}

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-reports/retention-dynamics.gif)

{% endcut %}

## Example of Retention calculation {#example}

{% include notitle [retention-example](_includes/retention-example.md) %}

## Data export {#export}

You can export data by choosing an item from the **Export** dropdown list above the chart. The data is exported based on the selected report settings: segmentation, grouping, and time period.

The dropdown list contains the following elements:

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-reports/export-data-cohorts.png)

- **Cohorts as CSV** — Exports the data from the table in the `CSV` format.
- **Chart as PNG** — Exports the chart image in the `PNG` format.

## Frequently asked questions {#faq}

{% include notitle [description](../_includes/faq.md#ua-retention) %} 

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
