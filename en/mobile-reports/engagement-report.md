# Engagement

{% note warning "" %}

If the user opens the app only once, the session duration [is not calculated](engagement-report.md#session-null).

{% endnote %}

The **Engagement** report displays information about how much time the user spends in the app on average, how often the app starts, the average session length, the total number of sessions, and the total time in the app.

{% include notitle [segments](_includes/segments.md) %}

## Tasks that the report helps to solve {#resolve-tasks}

**Evaluate the time users spend in your app**
:   Use the {% if locale == 'ru' %}**Timespent per user**{% endif %}{% if locale == 'en' %}**Timespent per user**{% endif %} metric to determine the average time individual users spend in the app and the {% if locale == 'ru' %}**Total timespent**{% endif %}{% if locale == 'en' %}**Total timespent**{% endif %} metric for the total time spent by all users (this value could be 100,000 hours across all users).

**Identify the average session length**
:   Use the {% if locale == 'ru' %}**Average session length**{% endif %}{% if locale == 'en' %}**Average session length**{% endif %} metric in various combinations with groupings by date, app version, or location. You can also use the {% if locale == 'ru' %}**Session length**{% endif %}{% if locale == 'en' %}**Session length**{% endif %} grouping for a clear breakdown by length.

**Evaluate the frequency of app use**
:   Use the {% if locale == 'ru' %}**Sessions per user**{% endif %}{% if locale == 'en' %}**Session per user**{% endif %} metric in combination with groupings by period (day, week, or month).

**Compare the engagement rates of different user groups**
:   Use groupings by platform, app version, location, or a combination of those (for example, by week and app version).

## General settings {#how-to}

1. Choose the time period and audience segment. By default, the report shows data for the week grouped by days.

   The time in the report is the beginning of the session on the user's device in the time zone specified in the app settings.

   {% note info "" %}

   {% include [period](_includes/period.md) %}

   {% endnote %}

2. You can select specific users for the report using [segmentation](segmentation.md).
3. You can set up [groupings](#group) and [metrics](#metrics) in the report.

## Configuring a chart with a choice of metrics {#metrics-in-graph}

{% include notitle [metrics-in-graph](_includes/metrics-in-graph.md) %}

## Selecting dimensions and metrics {#groups-metrics}

{% include notitle [groups-metrics](_includes/groups-metrics.md) %}

## Dimensions {#group}

{% include notitle [engagement-group](_includes/engagement-group.md) %}

{% include notitle [audience-group](_includes/audience-group.md) %}

{% include notitle [geo-group](_includes/geo-group.md) %}

{% include notitle [events-group](_includes/events-group.md) %}

{% include notitle [date-event-group](_includes/date-event-group.md) %}

{% include notitle [app-group](_includes/app-group.md) %}

## Metrics {#measure}

{% note info "" %}

Data is calculated by user session. Background sessions (sessions in which the app runs in the background and the user doesn't interact with it directly) aren't taken into account.

{% endnote %}

{% cut "Engagement" %}

- **Sessions**. Number of sessions.
- **Timespent per user**. The total duration of sessions divided by the number of users with 1+ session per period (sessions with an undefined duration aren't taken into account. For more information, see [A certain number of sessions have no defined duration](#session-null)).
- **Average session length**. The total duration of sessions divided by their number (sessions with an undefined duration aren't taken into account).
- **Session per user**. The number of sessions divided by the number of users with 1+ session per period.
- **Total timespent**. The total duration of all sessions (sessions with undefined duration aren't taken into account; for more information, see [A certain number of sessions have no defined duration](#session-null)).

{% endcut %}

![](../../_images/engagement-report-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

## Data export {#export}

{% include notitle [export-api](_includes/export-api.md) %}

## Troubleshooting {#problems}

### A certain number of sessions have no defined duration {#session-null}

{% note info "" %}

AppMetrica calculates duration based on [user sessions](../common/glossary.md#session).

{% endnote %}

When using automatic session tracking ([Android](../sdk/android/analytics/android-listen.md) | [iOS](../sdk/ios/analytics/ios-listen.md)), AppMetrica receives information about the end of the session when the next app activity occurs, including in the background. This means that AppMetrica can't calculate the exact duration of a session if a user starts the app only once.

{% note warning "" %}

AppMetrica also doesn't calculate the duration if the app is forcibly closed.

{% endnote %}

### Too many sessions with a duration of 0–9 seconds {#session-min}

User activity is tracked using the SDK ([Android](../sdk/android/analytics/android-listen.md) | [iOS](../sdk/ios/analytics/ios-listen.md)). When using automatic tracking, the default session timeout is 10 seconds. You can change this value using the library configuration settings ([Android](../sdk/android/analytics/android-listen.md) | [iOS](../sdk/ios/analytics/ios-listen.md)).

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
