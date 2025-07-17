# Conversions

A conversion is a target action performed by a user, such as a sign-up, purchase, or buying a subscription.

The conversion attribution window is calculated as follows:

- For E-commerce, Revenue, Ad Revenue, and custom events, it's the period of time between installing or opening the app (re-engagement) and a conversion.

- For Install and Re-engagement events, it's the period of time between clicking an ad and installing or opening the app.

The report shows all conversions within the attribution window, including the ones that came from organic search. 

{% include notitle [segments](_includes/segments.md) %}

## Tasks that the report helps to solve {#resolve-tasks}

- Determine which sources and campaigns bring you conversion actions, such as installs, purchases, or subscriptions.

- Evaluate the overall effectiveness of User Acquisition and re-engagement (remarketing).

- Understand how each type of ad campaign contributes to your results.

- Identify the sources of conversions that occurred during a specific time period.

- Compare the first-touch and last-touch [attribution models](#attribution).

## Report period {#period}

The report is formed for a specific time period. The default period is one week.

The conversion report is based on the date and time of a target action, unlike the [User Acquisition](user-acquisition-report.md) report that uses the app installation date and the [Remarketing](remarketing-report.md) report that is created cohort-wise based on the date of re-engagement.

## Configuring a chart with a choice of metrics {#metrics-in-graph}

{% include notitle [metrics-in-graph](_includes/metrics-in-graph.md) %}

<!-- ![](../../_images/conversion-report-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 700px;"}   -->

## Dimensions {#group}

{% include notitle [audience-group](_includes/audience-group.md) %}

{% include notitle [geo-group](_includes/geo-group.md) %}

{% cut "Conversions" %}

- **Conversion**.

{% endcut %}

{% cut "Conversion date" %}

- **Day**.
- **Week**.
- **Month**.

{% endcut %}

{% cut "Sources" %}

- **Partners**.
- **Trackers**.
- **Parameter**.
- **All parameters**.
- **Attributed touch**.
- **Engagement type**.

{% endcut %}

{% include notitle [app-group](_includes/app-group.md) %}

{% cut "Profile attributes" %}

  {% include notitle [profile-attributes-system](_includes/profile-attributes-system.md) %}

  {% include notitle [profile-attributes-install](_includes/profile-attributes-install.md) %}

{% endcut %}

## Metrics {#measure}

{% cut "Metrics by conversions" %}

- **Number of conversions**.

{% endcut %}

{% cut "Metrics by users" %}

- **Users**. The number of users with conversions.
- **Conversions per user**.
- **% of all users**.

{% endcut %}

{% cut "Metrics by sessions" %}

- **Converted sessions**.
- **Conversions per session**.

{% endcut %}

{% cut "Metrics by revenue" %}

- **Income**.
- **ARPU**. {{ arpu }}
- **Purchases**. {{ purchases }}
- **Paying users**. {{ paying-users }}
- **Average order value**.

{% endcut %}

## Attribution {#attribution}

When creating a report, you can select one of the following attribution methods:

- First-touch attribution: Attributes conversions to the initial source of user acquisition. For example, if a user installs your app after seeing an ad on the site of Partner 1 and then returns through a re-engagement campaign run by Partner 2 and makes a purchase, the conversion is attributed to Partner 1.

- Last-touch attribution: Attributes conversions to the last source a user interacted with before performing a target action. For example, if a user installs your app after seeing an ad on the site of Partner 1 and then opens the app by following a deeplink on the site of Partner 2 and makes a purchase, the conversion is attributed to Partner 2.

## Data export {#export}

{% include notitle [export](_includes/export-api.md) %}

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
