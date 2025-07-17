# Audience

You can use the **Audience** report data to find out which type of audience the ad campaign has drawn, and how changes to the app affect traffic from a certain region.

{% include notitle [segments](_includes/segments.md) %}

To build a report, you need to choose the time period, the audience segment, and the dimension. By default, the report shows the number of active and new users over a one-week period, grouped by date.

## The report will help you: {#resolve-tasks}

1. Evaluate your audience.

   Determine the structure of your audience, including both [new users](*new-user) and those who returned after being inactive. Estimate the number of [dormant users](*inactive-user) who might have been your app's active users.

   Interacting with each user group requires an individual approach. For many businesses, re-engagement of [dormant users](*inactive-user) is more cost-effective than attracting [new users](*new-user).

   More importantly, you need to proactively engage with users who are at risk of becoming dormant to keep them active. That's why it's crucial to understand who your dormant users are, what causes them to lose interest, and how to prevent it.

2. Use parameter-based dimensions to analyze dependencies.

   Group users by various parameters such as country, traffic source, gender, or age to identify key patterns. For example, you might discover that women use your app more frequently than men, or that Android users are more likely to become [dormant](*inactive-user) than iOS users. These insights can help you identify areas for growth. For example, the problem may be related to technical issues or how users interact with your app on certain devices.

3. Select an acceptable [inactivity period](*dormant-period) for a user.

## Working with the report {#work-report}

### General settings {#how-to}

1. Choose the time period and audience segment. By default, the report shows data for the week grouped by days.

   The time in the report is the beginning of the session on the user's device in the time zone specified in the app settings.

   {% note info "" %}

   {% include [period](_includes/period.md) %}

   {% endnote %}

2. You can select specific users for the report using [segmentation](segmentation.md).
3. You can set up [dimensions](#group) and [metrics](#metrics) in the report.

### Configuring a chart with a choice of metrics {#metrics-in-graph}

{% include notitle [metrics-in-graph](_includes/metrics-in-graph.md) %}

![](../../_images/audience-report-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 700px;"}   

If the period on the chart, such as a month, is longer than the inactivity period, such as a week, we might see instances where a user becomes new (installs the app), then dormant (doesn't use it for 7 days), then resurrected (starts using it again).

### Selecting dimensions and metrics {#groups-metrics}

{% include notitle [groups-metrics](_includes/groups-metrics.md) %}

#### Dimensions {#group}

{% include notitle [audience-group](_includes/audience-group.md) %}

{% include notitle [geo-group](_includes/geo-group.md) %}

{% include notitle [date-event-group](_includes/date-event-group.md) %}

{% include notitle [app-group](_includes/app-group.md) %}

{% include notitle [profile-attributes](_includes/profile-attributes.md) %}  

#### Metrics {#measure}

{% cut "Audience" %}

- **Users**. The number of app [users](*user) for the specified period.
- **New users**. The number of [new users](*new-user) for the specified period.
- **New user share**. The percentage of [new users](*new-user) relative to the total number of users for the specified period.

    Formula: $(\text{New users} / \text{Users}) * 100$.

- **Dormant users**. The number of inactive users for the specified period.

    Dormant users are those who used a mobile app in the past, but didn't show any activity over the specified period.

- **Resurrected users**. The number of returning users for the specified period. Resurrected users are those who showed no activity during the specified period, then returned to the app.

- **Percentage of dormant users**. The share of inactive users relative to the total number of users for the specified period.

    Formula: $(\text{Dormant users} / \text{Users}) * 100$.

- **Percentage of resurrected users**. The share of returning users relative to the total number of users for the specified period.

    Formula: $(\text{Resurrected users} / \text{Users}) * 100$.

{% endcut %}       

#### Days of inactivity {#dormant-period}

You can specify the period of inactivity to gain insights into dormant and resurrected users.

It shows the number of days during which the user didn't use the app. The default period is 7 days, but you can adjust it based on how your app is used.

Every app has its own appropriate inactivity period. For instance, you might order tea once a month, take a taxi once a week, and play a game every couple of days.

![](../../_images/inactive-period-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 550px;"}

**How the inactivity period is calculated**

Let's consider an example with a 7-day inactivity period.

In the report, check out the **Dormant users** metric for the following dates:

- September 27 shows the number of users whose last activity in the app was 7 days ago, on September 20.
- September 28 shows the number of users whose last activity in the app was 7 days ago, on September 21.

The number of such users doesn't add up daily, but is calculated only for newly acquired users.

### See also {#learn-more}

- [The report shows events and sessions, but not installations](../troubleshooting/troubleshooting.md#no-installs)

## Data export {#export}

{% include notitle [export-api](_includes/export-api.md) %}

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*new-user]: {% include notitle [описание](../_includes/glossary-src.md#new-user) %}

[*user]: {% include notitle [описание](../_includes/glossary-src.md#user) %}

[*inactive-user]: Users who used a mobile app in the past, but didn't show any activity over the specified period.

[*dormant-period]: The number of days during which the user didn't use the app. The default period is 7 days, but you can adjust it based on how your app is used.
