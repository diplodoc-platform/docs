# About events

AppMetrica collects basic data on app usage through different types of events. Most events are registered automatically. However, collecting data on some events requires a manual setup.

This data can help you understand what's happening within your app, for example, how often in-app purchases are made, how many users are active, and much more.

#|
|| **Event and its type** | **Tracking** | **Description** | **Logs API/ Data Stream API** | **Segmentation** | **Reports** ||
|| Installations (basic) | Auto | Registered when the app is first started with AppMetrica initialized. | Yes | Yes |
- [User Acquisition](../mobile-reports/user-acquisition-report.md) ||
   || Session start and end (basic) | Auto | App startup/shutdown with AppMetrica initialized. A session is considered new when the user returns to the app after a period that exceeds the specified timeout (Android, iOS). The end of the current session is registered when the next one starts. Used in reports to identify active users. | Yes | Yes, by session start within a specified period |
- [Engagement](../mobile-reports/engagement-report.md)
- [User Acquisition](../mobile-reports/user-acquisition-report.md)
- [Remarketing](../mobile-reports/remarketing-report.md) ||
   || [Deeplinks](deeplinks.md) (basic) | Auto / Custom | App openings via deeplinks, including universal links. Used to track remarketing campaigns. | Yes, in the Logs API | Yes, via deeplinks (if they contain tracking parameters) |
- [User Acquisition](../mobile-reports/user-acquisition-report.md)
- [Remarketing](../mobile-reports/remarketing-report.md) ||
   || [Events](about-events.md) (custom) | Custom | User actions specific to your app (for example, using a certain feature or switching to a certain screen). | Yes | Yes, by events, including their parameters |
- [Events](../mobile-reports/events-report.md)
- [Funnels](../mobile-reports/funnels-report.md) ||
   || [Profile attributes](about-profiles.md) (basic) | Custom | App user attributes, such as level achieved, loyalty program status, and internal ID. | Yes, in the Logs API | Yes |
- [Profiles](../mobile-reports/profile-report.md) ||
   || [In-app purchases](about-revenue.md) (basic) | Auto / Custom | Events of in-app purchases that were made via the App Store / Google Play. | Yes | Yes |
- [In-app and Ad Revenue](../mobile-reports/revenue-report.md) ||
   || [Ad Revenue](about-adrevenue.md) (basic) | Custom | Revenue from ad impressions received from a demand platform and provided for each impression (Impression Level Revenue Data). | Yes | Yes |
- [In-app and Ad Revenue](../mobile-reports/revenue-report.md)
- [User Acquisition](../mobile-reports/user-acquisition-report.md)
- [Remarketing](../mobile-reports/remarketing-report.md)
- [Cohort analysis](../mobile-reports/cohort-report.md)
- [Funnels](../mobile-reports/funnels-report.md)||
   || [E-commerce](about-ecommerce.md) (basic) | Custom | Events that track the product interaction cycle in e-commerce apps. | Yes | Planned |
- [E-commerce](../mobile-reports/ecommerce-report.md) ||
   || [In-app subscriptions](about-subscription.md) (basic) | Auto | Data on subscription purchases and status changes made via the App Store or Google Play. | No | Yes |
- [In-app and Ad Revenue](../mobile-reports/revenue-report.md)
- [User Acquisition](../mobile-reports/user-acquisition-report.md)
- [Remarketing](../mobile-reports/remarketing-report.md)
- [Funnels](../mobile-reports/funnels-report.md)
- [Cohort analysis](../mobile-reports/cohort-report.md) ||
   || [Crashes](about-crashes-and-errors.md) (basic) | Auto | Crash events that enable tracking stability metrics, identifying problematic cross-sections, and configuring monitoring thresholds. Deobfuscation requires uploading mapping, SO, or dSYM files. | Yes | No |
- [Crashes](../mobile-reports/crashes-and-errors.md) ||
   || [Errors](about-crashes-and-errors.md) (basic) | Custom | Events that track the most frequent errors grouped by ID and stack trace. | Yes | No |
- [Errors](../mobile-reports/crashes-and-errors.md) ||
   || Push tokens (basic) | Auto | Events that contain a special device ID in Firebase Cloud Messaging (FCM), Apple Push Notification Service (APNS), and Huawei Messaging Service (HMS). Required for sending push notifications directly to systems without using the Push API. | Yes | No | No ||
   |#

## Event verification {#verification-events}

{% note warning "" %}

Verification is only available on Android.

{% endnote %}

Each app is signed with a unique developer signature represented as a certificate fingerprint. All events sent from the app to AppMetrica servers come with this fingerprint.

If there's no fingerprint or it isn't the expected one, your app data received by AppMetrica may be distorted.

To identify these potentially fraudulent actions, AppMetrica offers the `certificate_verification_status` parameter within the Data Stream API. This parameter returns the result of matching the target certificate footprint with the certificate footprint that came with the event.

{% note warning "" %}

A valid signature doesn't guarantee that the event is authentic.

{% endnote %}

### How to enable {#how-to}

1. Get the SHA1 fingerprint of the certificate from your app development team.

2. Upload the fingerprint via the API: [Uploading an app certificate fingerprint](../mobile-api/management/fingerprints/fingerprints-android-post.md).

3. Shortly after the upload is complete, AppMetrica will begin validating the data coming from your app to its servers against the uploaded certificate.

4. When exporting data from the Data Stream API, add the `certificate_verification_status` field that will contain the verification result.

Managing certificate fingerprints:

- [Information about app certificate fingerprints](../mobile-api/management/fingerprints/fingerprints-android-get.md)
- [Uploading app certificate fingerprints](../mobile-api/management/fingerprints/fingerprints-android-post.md)
- [Deleting app certificate fingerprints](../mobile-api/management/fingerprints/fingerprints-android-delete.md)

### FAQ {#faq}

{% cut "What if I have more than one certificate?" %}

Upload all the certificates used by your app.

{% endcut %}

{% cut "Do I need to tag anything else in the app code?" %}

No, the fingerprints will be automatically sent to the server along with all types of events as soon as you upload the target certificates via the API.

{% endcut %}

{% cut "Can I see the validation result in reports?" %}

No, at the moment the validation result is only available over the Data Stream API in the `certificate_verification_status` field.

{% endcut %}

{% cut "Will this field be added to the Logs API?" %}

This field is only available in the Data Stream API.

{% endcut %}

{% cut "Where can I share my feedback and suggestions?" %}

Please share them using the [form](../troubleshooting/improvement-idea.md).

{% endcut %}

## Learn more {#learn-more}

- [Limiting custom events](../troubleshooting/limit-events.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
