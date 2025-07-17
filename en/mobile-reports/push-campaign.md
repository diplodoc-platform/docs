# Push campaigns

The report displays push campaign statistics, including the number of push notifications sent, delivered, and opened.

{% include notitle [segments](_includes/segments.md) %}

To build a report, you need to choose the time period, audience segment, and necessary push campaign.

## Report period {#period}

The report is formed for a specific time period. The default period is one week.

{% include [period](_includes/period.md) %}

## Dimensions {#group}

{% cut "Push Campaigns" %}

  - **Push campaigns**.
  - **Hypothesis**.
  - **Language**.
  - **Send error type**.
  - **Transport**.
  - **Campaign type**.
  - **Push SDK version**.

{% endcut %}  

{% include notitle [audience-group](_includes/audience-group.md) %}

{% include notitle [geo-group](_includes/geo-group.md) %}

{% include notitle [date-event-group](_includes/date-event-group.md) %}

{% include notitle [app-group](_includes/app-group.md) %}

{% include notitle [profile-attributes](_includes/profile-attributes.md) %}  

The data in the report can be grouped by push campaign name. To expand the campaign report, click ![](../../_images/plus.png =30x) in the list of names.

## Metrics {#measure}

{% note alert %}

If [A/B testing](../push/marketing.md#a-b-testing) wasn't configured when creating a push campaign, all statistics are for hypothesis A.

{% endnote %}

{% cut "Push Campaigns" %}

- **Sent**. Number of sent push notifications.
- **Delivered**. Number of delivered push notifications. By default, for iOS devices, a push notification is considered delivered if it was opened. To track delivery, [set up statistics collection](../sdk/ios/push/ios-settings.md) for push notifications.
- **Opened**. Number of opened push notifications.
- **Conversion from delivered to opened**. Ratio of delivered to opened push notifications.
- **Control sample**.
- **Error sending**.
- **Shown (Android)**
- **Push disabled (Android)**

{% endcut %}

<!-- ![](../../_images/push-report-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 800px;"} -->

## Data export {#export}

{% include notitle [export-api](_includes/export-api.md) %}

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
