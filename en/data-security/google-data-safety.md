# App privacy in Google Play

[Google requires](https://support.google.com/googleplay/android-developer/answer/10787469) mobile app developers to declare the data types collected by their app to Google Play. To do so, fill out the **Data safety** form on the [App content](https://play.google.com/console/app/app-content/summary) page in the Play Console.

## Collecting data {#data-collection}

Transmitting information from the user's device through the app.

#|
|| Libraries and SDKs | If your app has libraries or SDKs that transmit data from the user's device, note that regardless of whether the information is sent to you or a third-party server. ||
|| WebView | Declare if user data is collected through WebView components opened from your app provided your app controls their code or behavior. You don't need to declare data collected from WebView components used to navigate pages outside the app. ||
|| Ephemeral processing | If user data is transmitted from the device and processed ephemerally, declare that in the form. The information won't be disclosed in the Data safety section on Google Play if the data is only stored in the server memory and retained for no longer than necessary to execute a specific request in real time. That might apply, for example, to data processing in a weather app that transmits the user's location to retrieve information about the weather. In that case, the data is only stored in memory and gets deleted once the request has been executed.

{% note info %}

Using data to build advertising profiles or other user profiles can't be treated as ephemeral and must be declared as collection or sharing for those purposes.

{% endnote %}
||
|| Pseudonymous data | If data is collected pseudonymously, enter that in the form. For example, you must disclose all pseudonymized data that can be re-linked to the user. ||
|#

Not considered to be data collection:

**On-device access and processing**

:   You don't need to disclose user data that is only processed locally on the user's device.

**End-to-end encryption**

:   You don't need to declare user data transmitted from the device if it's encrypted in a way that prevents everyone other than the sender and recipient from reading it, you included. Encryption keys must not be available to any intermediary, including the developer.

## Transmitting data {#data-transmission}

Data sharing refers to transferring user data collected in your app to a third party.

#|
|| Off-device transfer, such as server-to-server transfers | For example, if user data collected in the app is transferred from your server to a third-party server. ||
|| On-device transfer to another app | Transferring user data from your app to another app on the same device. Disclose this in the Data safety section even if your app doesn't send the data off the device. ||
|| Transfer from your app libraries and SDKs | Transferring data collected in the app directly to a third party via libraries or SDKs included in your app. ||
|| Transfer from WebView components opened through your app | Transferring user data to a third party via a WebView component opened from your app. Declare this if your app controls the code or behavior of the WebView component. You don't need to declare data transferred from WebView components used to navigate pages outside the app. ||
|#

Not considered to be data sharing:

**Transfer to service providers**

:   User data is transferred to a service provider that processes it on behalf of the developer.

**Transfer for legal purposes**

:   User data is transferred for purposes stipulated by law. For example, due to a legal obligation or in response to a request from a government agency.

**Transfer following a user-initiated action or prominent disclosure and user consent**

:   Data is transferred to a third party as a result of a user-initiated action, where the user understands that their data will be shared. In addition, this category includes cases where information about data processing is prominently disclosed in the app and the user gives their consent to it.

**Transfer of anonymous data**

:   You're transferring fully anonymized user data that can't be linked to a specific person.

## Required and optional data {#data-optional}

For each data type, you can disclose whether it's required.

For example, a data type can be considered optional if:

- The user has control over its collection and can use the app without providing it.
- The user chooses whether to manually provide it.

To declare that your app collects optional data, make sure all users, regardless of their device or region, can opt in to or out of sharing it.

If a data type is required to perform your app's primary functionality, it must be declared mandatory.

## Other data disclosures {#data-additional}

You can provide additional information about how your app ensures data privacy and security.

#|
|| Encryption in transit | Specify whether data is encrypted when it's sent from the end user's device to the server. Some apps allow users to transfer data to third-party sites or services. For example, a messaging app may have a feature for sending SMS through the user's mobile network operator, which uses different encryption methods. In that case, the Data safety section may declare that information is transferred between the user's device and the app servers over a secure connection. ||
|| Deletion request mechanism | Declare whether users can request to have their data deleted. ||
|#

## Special badge {#data-icon}

Apps that have children as the target audience must comply with the Google Play Families policy. If your app falls under this category and meets the requirements, you can display the **Committed to follow the Families policy** badge in your Data safety section.

To display the badge:

1. In the **Data safety** form, go to the **Security practices** section.
1. Click **Go to Target audience and content**.

## Data types {#data-types}

Information about how user data of each type is collected and shared.

#|
|| **Data type** | **Description** | **AppMetrica SDK data collection (default configuration)** ||
|| **Location** ||
|| Precise location | The location of the user or device within an area of less than three square kilometers, such as a location obtained using Android's `ACCESS_FINE_LOCATION` permission. | No

Collection of this data is disabled by default in all SDK versions starting from 5.0.0.

The app developer can configure the transmission of this data by enabling the `Location tracking` parameter in the SDK settings. ||
|| Approximate location | The location of the user or device within an area of at least three square kilometers, such as the city the user is in or a location obtained using Android's `ACCESS_COARSE_LOCATION` permission. | No

Collection of this data is disabled by default in all SDK versions starting from 5.0.0.

The app developer can configure the transmission of this data by enabling the `Location tracking` parameter in the SDK settings. ||
|| **Personal info** ||
|| Name | The user's preferred name, such as their first name, last name, or nickname. | No

The app developer can configure how that data is transmitted if necessary. ||
|| Email addess | The user's email address. | No

The app developer can configure how that data is transmitted if necessary. ||
|| User IDs | The user's identifiers, such as their account number, ID, or name. | No

The app developer can configure how that data is transmitted if necessary. ||
|| Address | The user's address, such as their postal or home address. | No

The app developer can configure how that data is transmitted if necessary. ||
|| Phone number | The user's phone number. | No

The app developer can configure how that data is transmitted if necessary. ||
|| Race and ethnicity | Information about the user's race or ethnicity. | No

The app developer can configure how that data is transmitted if necessary. ||
|| Political or religious beliefs | Information about the user's political or religious beliefs. | No

The app developer can configure how that data is transmitted if necessary. ||
|| Sexual orientation | Information about the user's sexual orientation. | No

The app developer can configure how that data is transmitted if necessary. ||
|| Other info | Any other personal information, such as date of birth, gender identity, or veteran status. | No

The app developer can configure how that data is transmitted if necessary. ||
|| **Financial info** ||
|| User payment info | Information about the user's financial accounts, such as their credit card number. | No

The app developer can configure how that data is transmitted if necessary.

Starting from SDK version 4.0, automatic collection is available for in-app purchase data. You can disable it using the `withRevenueAutoTracking Enabled` method. ||
|| Purchase history | Information about the user's purchases and transactions. | No

The app developer can configure how that data is transmitted if necessary.

Starting from SDK version 4.0, automatic collection is available for in-app purchase data. You can disable it using the `withRevenueAutoTracking Enabled` method. ||
|| Credit score | Information about the user's credit rating. | No

The app developer can configure how that data is transmitted if necessary.

Starting from SDK version 4.0, automatic collection is available for in-app purchase data. You can disable it using the `withRevenueAutoTracking Enabled` method. ||
|| Other financial info | Other financial information, such as the user's salary or debts. | No

The app developer can configure how that data is transmitted if necessary.

Starting from SDK version 4.0, automatic collection is available for in-app purchase data. You can disable it using the `withRevenueAutoTracking Enabled` method. ||
|| **Health and fitness** ||
|| Health info | Information about the user's health, such as medical records or symptoms. | No ||
|| Fitness info | Information about the user's physical activity, such as workouts. | No ||
|| **Messages** ||
|| Emails | Content, subject line, and information about the sender and recipients of the user's emails. | No ||
|| SMS or MMS | Content and information about the sender and recipients of the user's messages. | No ||
|| Other in-app messages | Other types of messages, such as instant messages or chat content. | No ||
|| **Photos or videos** ||
|| Photos | The user's photos. | No ||
|| Videos | The user's videos. | No ||
|| **Audio files** ||
|| Voice or sound recordings | Audio recordings and recordings of the user's voice, such as voice messages. | No ||
|| Music files | The user's music files. | No ||
|| Other audio files | Other audio files created or provided by the user. | No ||
|| **Files and docs** ||
|| Files and docs | The user's documents and other files or any information about them, such as file names. | No ||
|| **Calendar** ||
|| Calendar events | Information from the user's calendar, such as events, event notes, and attendees. | No ||
|| **Contacts** ||
|| Contacts | Information about the user's contacts, such as contact names or message history, and information like usernames, call history, contact recency, contact frequency, and interaction duration. | No ||
|| **App activity** ||
|| App interactions | Information about how the user interacts with the app, such as the number of times they visited a page or the sections they tapped. | No

The app developer can configure the transmission of this data using custom events. ||
|| In-app search history | Information about what the user has searched for in your app. | No

The app developer can configure transmission for this data using custom events. ||
|| Installed apps | Information about the apps installed on the user's device. | No

The app developer can configure transmission for this data using custom events. ||
|| Other user-generated content | Other user-generated content not mentioned in any section, such as user bios, notes, or open-ended responses. | No

The app developer can configure transmission for this data using custom events. ||
|| Other actions | Other in-app user actions not mentioned in any section, such as gameplay, likes, and selected dialog options. | No

The app developer can configure transmission for this data using custom events. ||
|| **Web browsing** ||
|| Web browsing history | Information about the sites visited by the user. | No ||
|| **App info and performance** ||
|| Crash reports | Data from your app's crash log, such as the number of crashes and stack traces or other information directly related to crashes. | No ||
|| Diagnostics | Information about the app's performance, such as battery life, loading time, latency, frame rate, or technical diagnostics. | Yes

AppMetrica can collect battery level data for crash analytics. ||
|| Other app performance data | Other app performance data not mentioned here. | Yes

AppMetrica can collect additional data. For example, technical information about the device, including the OS version and screen type. ||
|| **Device or other IDs** ||
|| Device or other IDs | Device, browser, or app IDs, such as the IMEI number, MAC address, Widevine device ID, Firebase installation ID, or advertising ID. | Yes, if the developer obtained the user's permission.

Collection of this data can be disabled in SDK version 5.0.0 or higher. ||
|#

## Data collection purposes {#data-goal}

Information about data collection purposes.

| Data purpose | Description |
| ----- | -------- |
| App functionality | Used for the app's operations. For example, to enable app features or perform user authentication. |
| Analytics | Used to collect data about how users interact with the app or its performance. For example, to see how many users selected a particular feature, monitor the app's status, diagnose and fix bugs and crashes, or make performance improvements. |
| Developer communications | Used to send news and notifications about you and your app. For example, to send push notifications about important security updates or new app features. |
| Advertising or marketing | Used to display targeted ads and marketing messages or measure ad performance. For example, to place ads in the app, send push notifications to promote other products and services, or share data with advertising partners. |
| Fraud prevention, security, and compliance | Used to prevent fraud, ensure security, and comply with legal requirements. For example, to monitor failed login attempts and identify suspicious activity. |
| Personalization | Used to personalize the app by displaying recommended content or suggestions. For example, to suggest playlists based on the user's preferences or deliver local news based on their location. |
| Account management | Used to configure user accounts. For example, to enable users to create accounts, add information to accounts you provide for multiple services, log in to the app, or verify their credentials. |

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
