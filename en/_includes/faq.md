#### {#ua-events}

{% cut "Event counts in Event and User Acquisition reports don't match" %}

The [User Acquisition](../mobile-reports/user-acquisition-report.md) report displays only events that occurred after the app was installed and the installation occurred during the selected report period. The [Events](../mobile-reports/events-report.md) report displays events that are not related to the installation date. The user could have installed the app earlier, before the selected period, and complete the event later.

{% endcut %}

#### {#ua-retention}

{% cut "Why do the Retention metrics in the User Acquisition and Retention Analysis reports don't match?" %}

In the [Retention Analysis](../mobile-reports/retention-report.md) report, sessions are counted by calendar days — starting from 00:00.

In the [User Acquisition](../mobile-reports/user-acquisition-report.md) report, sessions are counted based on the time since the app was installed. For example, if a user downloaded and opened the app at 7 p.m. on April 20, then the next day will start at 7 p.m. on April 21.

Accordingly, the indicators are also calculated: in the Retention Analysis report — calendar-based, and in the User Acquisition report — interval-based.

{% endcut %}
