# Insights

Insights is a new feature in AppMetrica that automatically analyzes your app’s key metrics, identifies meaningful changes, and displays notifications with updates right in your interface.

Insights draw your attention to the most important changes and enable you to access relevant reports for deeper analysis in just a single click.

## How does it work {#how}

Insights monitor your key app metrics for any changes and highlight the results in a timely pop-up notification directly in your interface. If you want more details on the data, you can click on the button in the pop-up and go directly to the report in question.

You can also find a detailed list of all identified insights within a chosen period in the Insights report, located in the left-hand menu.

An insight notification includes information on:

- What changed
- In what date range
- In what user segment
- By how much in % or an absolute number
If an insight is connected to a report, it also includes a click-through link to that report.

![](../../_images/insights-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

By default, insights are displayed to users with the following roles:

- App owner
- Read/edit
- Read only

If you haven't noticed any notifications, then there were most likely no significant changes detected in your app's metrics or they flattened out over time.

## Why use insights {#why}

Insights is a valuable tool for all AppMetrica users. It’s designed to simplify app monitoring, saving you time and ensuring you never miss critical changes in your app’s key metrics.

You’ll find Insights most helpful:

- If you’re new to app analytics and unsure which metrics to track.
- If you want a simple way to keep an eye on your app’s performance without getting lost in complex reports.
- When launching new app versions or features.

## Types of insights {#types}

{% note info %}

This feature is in open beta. In the future, we'll be adding more insights and improving their visual presentation. If you have any suggestions for this feature, please [share](../troubleshooting/improvement-idea.md) them with us. Your feedback is greatly appreciated!

{% endnote %}

### Timespent changes in new app versions {#timespent}

This insight tracks whether the average time spent per user per day has increased or decreased in your new app versions.

**For example**
:   On September 12, AppMetrica detected that the "Timespent per user" value for your Android 2.1.0 app spiked 24.2% (599 seconds) above average.

Calculation specifics:

- A version is considered new if it was rolled out to at least 5% of the audience no more than 14 days ago.
- For an app version to be taken into account, it needs to be used by at least 1% of users on the platform over the last 14 days.
- Devices with different versions within the period aren't included in the calculation.
- The exact figures in the notification are current at the time the insight appears.

### Changes in the share of paying users {#pay}

Shows the change in the share of paying users per day. An abnormal change is a statistically significant change, while an insight is a noticeable, but not statistically significant change.

**For example**
:   On October 24, AppMetrica detected that the share of paying users in the app had grown by 2.5%. It also notices a 4% increase in the number of paying users, with no significant changes in the app's overall audience.

<!-- How to interpret this data:

- If the share grew and the absolute number didn't change, then the paying audience remained the same and the non-paying audience reduced the use of the app.
- If the share grew along with the audience, this could indicate improvements in the quality of your app's traffic.-->

Calculation specifics:

- Statistics are counted for the last 21 days.
- For AppMetrica to perform calculations, there must be at least 50 paying users every day.
- The exact figures in the notification are current at the time the insight appears.

### Weekly sticky factor {#weekly-sticky}

In short, this will show you your DAU to WAU / WAU to MAU ratio. Based on this data, you can conclude whether your users are using your app less or more frequently, on average.

### E-commerce ARPPU {#arppu-ecom}

The ARPPU stands for Average Revenue per Paying User. This update for e-commerce apps will keep you in the loop on how much revenue your paying users are bringing in.

### Ad ARPWAU {#arpwau}

This metric shows the average ad revenue per weekly active user for apps that monetize through ads.

### In-app RPPU {#rppu}

This metric highlights the revenue per paying user within your app.

## Make a suggestion {#idea}

If you want to track changes for other metrics or have any feedback on how we could improve the functionality, please share your ideas with us.

[Make a suggestion](../troubleshooting/improvement-idea.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
