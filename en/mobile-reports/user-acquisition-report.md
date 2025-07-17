# User Acquisition

The User Acquisition report displays statistics on app install sources. You can select specific users for the report using [segmentation](segmentation.md).

## Report period {#period}

The User Acquisition report works with user cohorts: when you select the report period it displays installations of this period, but all metrics of the specified user cohort are displayed since the app installed (not only in the specified period).

{% include [period](_includes/period.md) %}

## Dimensions and metrics {#groups-annd-metrics}

{% include [groups-metrics](_includes/groups-metrics-old.md) %}

### Dimensions {#group}

{% cut "Sources" %}

- **Partners**.
- **Trackers**.
- **Parameter**.
- **All parameters**.
- **App Installer**.
- **Reattribution**. Possible dimensions: [new installs](*New installs), [reattributions](*Reattribution installs), and [undefined](*undefined).
- **Attribution type**. Accepts the values Organic, Click, Impression, Preset, and Deeplink
- **Fraud assessment**. 

{% endcut %}

{% include notitle [audience-group](_includes/audience-group.md) %}

{% include notitle [geo-group](_includes/geo-group.md) %}

{% include notitle [date-install-group](_includes/date-install-group.md) %}

{% include notitle [app-group](_includes/app-group.md) %}

{% cut "Profile attributes" %}

{% include notitle [profile-attributes-system](_includes/profile-attributes-system.md) %} 

{% include notitle [profile-custom-group](_includes/profile-custom-group.md) %} 

{% endcut %}

### Metrics {#measure}

{% cut "Main metrics" %}

- **Clicks**. The number of clicks users made.
- **Installs**. The total number of devices with the app installed. To break down the metric by installation types (new, reattributed), use the **Installation Type** grouping.
- **Impressions**. Impression count.
- **Click-to-install conversion rate**. 
- **CTIT**. Average interval between clicks/impressions and installations (depending on the attribution type).
- **CTR**. Impression-to-click conversion rate.
- **IPM**. Installs per thousand impressions.
- **Impression-to-install conversion rate**.
- **Deeplinks**. The number of times the application was opened via deeplinks.

{% endcut %}

{% include notitle [conversion-metrics](_includes/conversion-metrics.md) %} 

{% cut "Usage" %}

- **Sessions**.
- **Loyal users**.
- **Retention**.

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

{% include notitle [ad-revenue-metrics](_includes/ecommerce-metrics.md) %} 

<!-- ![](../../_images/user-acquisition-report-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 800px;"} -->

## Data export {#export}

{% include notitle [export](_includes/export-api.md) %}

## Frequently asked questions {#faq}

{% include notitle [description](../_includes/faq.md#ua-events) %} 

{% include notitle [description](../_includes/faq.md#ua-retention) %} 

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*New installs]: {{ new-installs }}

[*Reattribution installs]: The number of installations for trackers with the reattribution option enabled.

[*Clicks]: The number of clicks users made.

[*Impressions]: Impression count.

[*CTIT]: Average interval between clicks/impressions and installations (depending on the attribution type).

[*CTR]: Impression-to-click conversion rate.

[*IPM]: Installs per thousand impressions.

[*Sessions]: The number of user sessions for the entire time since installation.

[*Loyal users]: {{ loyal-users }}

[*Number of events]: The total number of events that occurred in the app.

[*Number of users with the event]: The number of users who had this event occur in the app.

[*Event conversion]: The percentage of users with the event out of the total number who installed the app.

[*Purchases]: {{ purchases }}

[*Paying users]: {{ paying-users }}

[*Purchases per user]: {{ purchases-per-user }}

[*% of paying users]: {{ percent-per-paying-user }}

[*Invalid revenue]: {{ invalid-revenue }}

[*Users with invalid revenue]: {{ users-with-invalid-revenue }}

[*Revenue]: App revenue. It is calculated as the sum of all purchases.

[*Ad Revenue events]: {{ ad-revenue-events }}

[*Ad Revenue]: {{ ad-revenue-new }}

[*eCPM]: {{ ecpm }}

[*Users with Ad Revenue]: {{ users-with-ad-revenue }}

[*Ad Revenue events per user]: {{ ad-revenue-events-per-user }}

[*Sessions with Ad Revenue]: {{ sessions-with-ad-revenue }}

[*Ad Revenue events per session]: {{ ad-revenue-events-per-session }}

[*% of users with Ad Revenue]: {{ percent-users-with-ad-revenue }}

[*undefined]: Events for which AppMetrica cannot apply the "installation type" term. For example: clicks.

[*Installs]: The total number of devices with the app installed. To specify the metric by installation type (new, reattributed), use the **Installation type** dimension.

[*Events per user]: The average number of events per user. This metric is calculated as the ratio of the total number of events to the specified metric (the default metric is "All installations").

[*In-App Revenue]: {{ in-app-revenue }} {{ currency-conversion }}

[*Average order]: {{ average-order }} {{ currency-conversion }}

[*In-App ARPU]: {{ arpu }} {{ currency-conversion }}

[*In-App ARPPU]: {{ arppu }} {{ currency-conversion }}

[*Ad ARPU]: {{ ad-arpu }} {{ currency-conversion }}

[*Total Revenue]: {{ total-revenue}} {{ currency-conversion }}

[*Total APRU]: {{ total-arpu }} {{ currency-conversion }}

[*deeplink]: {{ deeplink }}

[*Retention]: The percentage of users who installed the app during a given day, week, or month (the reference period) and then returned to the app (opened it) on a specific day, week, or month after installing. This metric is calculated as the ratio of the number of users running the app during the Nth day, week, or month to the number of users who installed the app in the reference period (this number is taken as 100%). More information in the [Retention](retention-report.md) report.

[*Deeplinks]: The number of times the application was opened via deeplinks.

[*Attribution type]: Accepts the values Organic, Click, Impression, Preset, and Deeplink.
