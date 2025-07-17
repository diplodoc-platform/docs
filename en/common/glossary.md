# Glossary

{% note warning "" %}

To view sample reports, you need demo access.

{% endnote %}

Active user/user

:   {% include notitle [описание](../_includes/glossary-src.md#user) %}

    [Sample report](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&report=audience&metrics=ym_u_activeUsers&sampling=1&tableRoot=date&chartType=line&sort=-ym%3Au%3Adate).

Ad revenue

:   {{ ad-revenue }}

Age

:   This metric is detected using [Crypta](http://company.yandex.ru/technologies/crypta/) technology. [Sample report](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&report=audience&metrics=ym_u_activeUsers&sampling=1&tableRoot=age&chartType=pie&sort=-ym%3Au%3AactiveUsers).

App version

:   The version of the application that the user has installed, including the build number. [Sample report](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&report=app-version&metrics=ym_t_devices&sampling=1).

ARPU

:   {{ arpu }}

ARPPU

:   {{ arppu }}

Attribution

:   - First-touch attribution: Attributes conversions to the initial source of user acquisition. For example, if a user installs your app after seeing an ad on the site of Partner 1 and then returns through a re-engagement campaign run by Partner 2 and makes a purchase, the conversion is attributed to Partner 1.

    - Last-touch attribution: Attributes conversions to the last source a user interacted with before performing a target action. For example, if a user installs your app after seeing an ad on the site of Partner 1 and then opens the app by following a deeplink on the site of Partner 2 and makes a purchase, the conversion is attributed to Partner 2.

Crash

:   A critical error that leads to emergency shutdown of the app. Collected and sent automatically. To disable collecting and sending errors, call the `setReportCrashesEnabled` method in the SDK API. Sample report: [Android](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&report=crash-logs-android&sampling=1) | [iOS](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&report=crash-logs-ios&sampling=1).

Cohort analysis

:   Allows you to group users by the app install date and track changes over time for each cohort in the percentage of users who return to the app, or the percentage of users who complete a target event (event conversion). You can also compare these cohorts with each other. For more information, see [Cohort analysis](../mobile-reports/cohort-report.md). [Sample report](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&report=cohort&metrics=ym_m_users&sampling=medium).

Cohort

:   A group of users who share a characteristic and the date of completing a target event. The shared characteristic may be an app install or a target event.

Connection

:   Type of internet connection (for example, Wifi, Hspa+, LTE, HSDPA). [Sample report](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&report=network-type&metrics=ym_t_devices&sampling=1).

Conversion

:   Depending on the context, is determined as:

   - A target action performed by a user, such as a sign-up, purchase, or buying a subscription.

   - The percentage of the total number of users who completed a target event during the selected time period.

Conversion attribution window   

:   For E-commerce, Revenue, Ad Revenue, and custom events, it's the period of time between installing or opening the app (re-engagement) and a conversion.

    For Install and Re-engagement events, it's the period of time between clicking an ad and installing or opening the app.

Error

:   Any error (not a crash) that occurred in the app. It can be sent by calling the `ReportError` method in the SDK API. Sample report: [Android](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&report=error-logs-android&sampling=1) | [iOS](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&report=error-logs-ios&sampling=1).

Event

:   Programming code used for transmitting information about user activity that you want to track, such as app installs.

   You can use the [AppMetrica SDK](../sdk/platforms.md) to transmit event messages and events with additional parameters.

   You can pass any data structure in [JSON](http://www.json.org/json-ru.html) for calculations:

   * **object** — A tree branch is created for each object key, and the algorithm is called recursively for each value.
   * **string** — Counts the number of times each different value of the string occurs.
   * **number** — Calculates the total and average value of all numbers.
true, false, or null — Calculates the number of times each value occurs.
   * **array** — Creates a [Parameters] tree branch and calculates the number of times when the value is an array. The algorithm is run recursively for each item in the array.

   [Sample report](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&report=events&dimensionValues=tab_1+finished%3Bbutton_1+opened%3Bbutton_1+closed&metrics=ym_m_clientEvents&sampling=1). For more information about how data is presented in reports, see [Events](../data-collection/about-events.md).

Deeplink

:   {{ deeplink }}

Deferred deeplink

:   A link that transfers specified data to the application at the first start. A valid deferred deeplink example: `sampleapp://samplepath?sampleparam1=samplevalue1`.

   The maximum number of characters that can be transferred in the deferred deeplink parameters is 7475.

Destination URL

:   Leads to the app store or a page where the user can install the app.

Device

:   Names of device models. [Sample report](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&report=mobile-model&metrics=ym_t_devices&sampling=1).

Gender

:   This metric is detected using [Crypta](http://company.yandex.ru/technologies/crypta/) technology. [Sample report](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&report=audience&metrics=ym_u_activeUsers&sampling=1&tableRoot=gender&chartType=pie&sort=-ym%3Au%3AactiveUsers).

Geography

:   The region of the user's location is detected using GPS, LBS. [Sample report](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&report=audience&metrics=ym_u_activeUsers&sampling=1&tableRoot=region&chartType=pie&sort=-ym%3Au%3AactiveUsers).

Guest access

:   Allows you to give another user access to your app statistics. For more information, see [Managing app access](access.md).

Identification

:   For device identification, the AppMetrica SDK uses various types of identifiers available in the system depending on the platform, or combines them for increased accuracy. For this purpose, the Google AID is collected on Android devices, and the Apple IDFA and IFV are collected on iOS devices.

   {% cut "More information about identifiers" %}

   _Google AID_

      An advertising ID that is assigned by Google Play services. The advertiser can use it to identify a unique user, display targeted ads, and track the number of click-throughs from an ad to a website. If desired, the user can reset the ID or disable ad personalization.

   _Apple IDFA_

      An advertising ID. The advertiser can use it to identify a unique user, display targeted ads, and track the number of click-throughs from an ad to a website. If desired, the user can reset the ID.

   _IFV_

      An ID that is issued to the advertiser of an app. The same IFV is used for all apps from the same developer.

   {% endcut %}

IAP Revenue

:   {{ iap }}

Interface language

:   The system locale (such as ru-RU or tr-TR). [Sample report](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&report=locale&dimensionValues=ru-RU%3Btr-TR%3Bru_RU&metrics=ym_m_users&sampling=1).

Median

:   The value of data samples which means that half of sample items are greater than this value and the other half are less.

    For example, for the {23, 32, 24, 26, 40} sample the median is equal to 26.

    To obtain the median value, arrange the sample items in ascending or descending order and take the middle item: {23, 24, 26, 32, 40}. If the sample has an even number of items, the median is half the sum of the two middle items.

New user

:   {% include notitle [описание](../_includes/glossary-src.md#new-user) %}

Platform

:   The platform that the app is running on (for example, iOS, Android, or WindowsPhone). [Sample report](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&report=operating-system-version&dimensionValues=iOS%3Bandroid%3BWindowsPhone&metrics=ym_m_users&sampling=1).

Organic

:   All app installs that users make themselves (for example, from the app store), as well as installs that weren't attributed to a partner or advertising campaign.

Operator

:   The mobile carrier that the device uses to connect to mobile internet. Determined based on the MCC (Mobile Country Code) and MNC (Mobile Network Code). [Sample report](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&report=operator&dimensionValues=null%23null%3B250+1%23250%3B250+2%23250&metrics=ym_m_users&sampling=1).

Postback

:   A GET request to the specified URL (the postback URL), which certain parameters can be sent to. You can add up to 5 requests per campaign. For more information, see the [postback policy](../mobile-tracking/policy.md).

Postback URL

:   A link for sending an event message (about an install or a target event). The event recipient is a partner. You can [send additional parameters](../mobile-tracking/postback-specification.md) to the postback URL.

Post-click landing

:   {% note warning "" %}

    The post-click landing option is no longer supported.

    {% endnote %}

   The page that will be opened in the user's browser after clicking the link to install the app. You can enter it when you [configure the tracker](../mobile-tracking/add-tracker.md).

Re-engagement

:   {{ re-engagement }}

Remarketing campaign

:   An ad campaign aimed at getting users to come back to an app they previously installed. For more information, see [Creating a remarketing tracker](../mobile-tracking/add-remarketing-tracker.md).

Retention

:   The percentage of users who installed the app during a given day, week, or month (the reference period) and then returned to the app (opened it) on a specific day, week, or month after installing.

   This metric is calculated as the ratio of the number of users running the app during the Nth day, week, or month to the number of users who installed the app in the reference period (this number is taken as 100%).

Revenue

:   App revenue. App revenue can be divided into two types: [IAP (in-app purchase)](*iap) and [Ad (Advertising)](*ad).
To track revenue in reports, you should configure sending in the library. For more information, see [{#T}](../data-collection/about-revenue.md#send-revenue).

Rolling Retention

:   The percentage of users who installed the app during a given day, week, or month (the reference period) and then returned to the app during a specific day, week, or month, assuming they could have potentially returned during the preceding time period. These users are not interpreted as lost (inactive) until the last time they start the app.

   To better understand how Rolling Retention works, imagine a user who first opened the app on the day of installation (the reference day), and next opened it on the fourth day after installing. This user is counted as active on the fourth day and for all the previous days, as well. Even though it took the user four days to come back to the app, this was always a possibility during that time.

Root status

:   Whether the device has root access. Root access is used on a device for deleting system applications, making unauthorized changes, or installing apps that only work in this mode. [Sample report](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&report=root-status&dimensionValues=Not+Rooted%3BRooted&metrics=ym_m_users&sampling=1).

Sampling

:   Controls the accuracy of report data. If generating a report requires a large amount of data, collecting this information might take a long time. In order to generate the report faster, the service can use just part of the data (for example, 10%). You can control sampling manually.

Screen

:   The screen resolution in pixels (such as 1280x720). Orientation is not considered. [Sample report](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&report=resolutions&dimensionValues=1024⨯768%3B1280⨯720%3B568⨯320&metrics=ym_m_users&sampling=1).

Segment

:   A subset of users filtered by a formal attribute (for example, by the OS name).

Session {#session}

:   {% include notitle [Отслеживание активности пользователей](../sdk/_includes/listen-intro.md) %}

Session length

:   The time difference between the first and last event in the session. The session starts when the app is opened, and ends when the app is closed, a new session is force started, the app crashes, or the user is inactive for a prolonged period (session timeout). By default, the timeout is 10 seconds. You can change this value using the extended library configuration. [Sample report](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&period=2024-10-01%3A2024-10-31&group=hour&accuracy=absolute&sampling=1&reportId=engagement&chartMetrics=[["ym%3As%3AtotalSessionDurationPerUser"]]&selectedDimensionKeys=[["ym%3As%3Adate"]]&tableMetrics=[["ym%3As%3AtotalSessionDurationPerUser"]%2C["ym%3As%3Asessions"]%2C["ym%3As%3AsessionsPerUser"]%2C["ym%3As%3AavgSessionDuration"]%2C["ym%3As%3AtotalSessionDuration"]]&view=Hierarchical&sortBy=-ym%3As%3AtotalSessionDurationPerUser&metricValueMode=Absolute).

Silent push notification

:   {{ silent-push }}

Tracker

:   {% note warning "" %}

    The post-click landing option is no longer supported.

    {% endnote %}

    A container with URLs and settings for tracking and collecting statistics about app installs via partners as part of an ad campaign. You can use it to set the destination URL, deeplink, or post-click landing page and get a tracking URL. When users go to the URL and then install or open the app, it's reflected in the [report](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&&report=campaigns2&sampling=1).

Tracking URL

:   A link in the `https://appmetrica.yandex.com/serve/*` format that takes the user to the app store for installing the app. If the app is already installed, it opens the app (if a deeplink is specified). Created when setting up the tracker. For more information, see [What is tracking?](../mobile-tracking/index.md).


Traffic source

:   The source for an app install. The source may be an advertising campaign that engages users, or organic installs (directly from the app store). [Sample report](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&report=campaigns2&metrics=ym_m_advInstallDevicesFake&sampling=medium).


Validating purchases

:   Confirming a purchase and payment on Google Play Market or Apple App Store. Validation lets you filter purchases made from hacked apps. With validation enabled, all In-App Revenue metrics are counted based on validated purchases and purchases sent without validation parameters. For invalid purchases, **Invalid revenue** and **Users with invalid revenue**  metrics are counted.

   For more information about validation setup, see [{#T}](../data-collection/about-revenue.md#send-revenue).

[*timeout-session]: Session timeout that you set in the SDK.

[*iap]: {{ iap }}
[*ad]: {{ ad }}
