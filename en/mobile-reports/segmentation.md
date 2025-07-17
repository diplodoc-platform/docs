# Segmentation

{% note alert %}

You can configure Yandex.Direct ad campaign targeting by AppMetrica segments. To do this, save a segment in AppMetrica and add it to [Yandex Audience](https://yandex.ru/support2/audience/en/segments/app-metrica). For more information, see [How to set up retargeting](https://yandex.ru/adv/news/kak-nastroit-retargeting-dlya-reklamy-mobilnykh-prilozheniy).

{% endnote %}

AppMetrica collects and processes a large volume of information about apps and their users. To pull the desired data from the full set of statistics, you can create a [segment](*segment). For example, you can use segments to get statistics for tablet users who installed the app in Russia, but now they are in the US.

A segment is created by using criteria to filter data. A filter can consist of one or more criteria. When selecting multiple criteria, you can use the "AND" and  "OR" operators. If you select criteria in the same filter, the  "OR" operator is applied. If you select criteria in different filters, the  "AND" operator is applied.

You can save the resulting segments and use them when [creating push campaigns](../push/marketing.md).

{% note info %}

Saving segments option is only available to users with [editing rights](../common/access.md).

{% endnote %}

Segmentation is available in all AppMetrica reports, but the number of available filters depends on the selected report. When you switch between reports, AppMetrica applies the selected filters to the data in the new report. If any of the filter criteria can't be applied, AppMetrica displays them in the **Incompatible filters** section.

AppMetrica has two levels of segmentation filters:

- [User level](#users-segment)
- [Report level](#specific-segments)

## User level {#users-segment}

Allows you to set criteria for sampling data that is relevant to a specific user. This includes demographic data and various attributes of the installs such as region and tracker parameters.

The following user level filters are available:

- Event
- Demography
  - Gender
  - Age
- Session start
- Installation
  - Installation date
  - Media source
  - Tracker
  - Tracker parameters
  - Geography of installation
  - Operating system
  - App version
  - App Installer
  - Attribution type
  - Attribution source
  - Fraud assessment
- Re-engagement
  - Date
  - Media source
  - Tracker
  - Tracker parameters
  - Geography
  - Operating system
  - App version
- Start by deeplink
  - Date of start by deeplink
  - Media source
  - Tracker
  - Parameters
- Push campaigns (events)
  - Sent
  - Delivered
  - Opened
  - Dismissed
  - Control sample
- Lifetime metrics
  - Days since installation
  - Days since last session
  - Number of sessions
  - Number of crashes
  - Opened push notifications
- In-App Revenue
  - In-App Purchase events
  - Purchase date
  - Product
  - Purchase amount
  - Purchase currency
  - Validation status
  - Order ID
  - Purchase geography
  - Revenue payload
- Ad revenue
  - Ad Revenue date
  - Purchase amount
  - Ad Revenue currency
  - Geography of Ad Revenue
  - Ad type
  - Ad network
  - Ad unit ID
  - Ad unit name
  - Ad placement ID
  - Ad placement name
  - Ad precision
  - Ad revenue payload
- Current values
  - Region
  - Application
  - Device
  - Device attributes

{% note alert %}

For [User Acquisition](user-acquisition-report.md), [Remarketing](remarketing-report.md), [Cohort analysis](cohort-report.md), [Retention analysis](retention-report.md), and [Profiles](profile-list.md) reports, only user filters are available.

{% endnote %}

## Report level {#specific-segments}

Allows you to select data specific to the opened report. For example, in the **Audience** report (which is based on sessions) you can select the user's location, event, and the type of device used in the session during the specified period.

The following reports have report level filters:

- Events report.
- Sessions report.
- Report on push campaigns.
- Crash and error report.

## See also (#learn-more)

- [Creating a segment](segment-creation.md)
- [A segment based on AppMetrica data in Yandex.Audience](https://yandex.ru/support/audience/segments/app-metrica.html)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*segment]: A subset of users filtered by a formal attribute (for example, by the OS name).
