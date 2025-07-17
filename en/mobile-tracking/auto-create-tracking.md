# Automatic tracking

For some attribution sources, AppMetrica uses automatic tracking. The system attributes these sources based on the following criteria:

- AppMetrica detects tags from advertising and analytical systems within URL parameters.
- You have remarketing campaigns in Yandex Direct.
- You've enabled the [import of attributions from other SDKs](../data-collection/attribution-integration.yaml).

After attributing the sources, AppMetrica can create automatic trackers, sorting traffic by its media source based on the derived information.

## URL parameter–based attribution {#auto}

AppMetrica automatically collects and displays information about your various campaigns.

The algorithm considers tags from advertising and analytical systems based on URL parameters. Using this data, AppMetrica can create an automatic tracker and identify the media source.

This algorithm allows attributing installs and deeplinks to the media sources that directly led to these actions.

You can find statistics for the **Installs** and **Deeplinks** metrics in the following reports:

- [User Acquisition](../mobile-reports/user-acquisition-report.md])
- [Remarketing](../mobile-reports/remarketing-report.md)

Examples of automatic trackers:

- **Automatic install tracker**. Created based on information from Install Referrer. Only available for Android.
- **Automatic deeplink tracker**. Created based on information from URL parameters.

## Integration-based attribution {#with-intagration}

### Remarketing campaigns from Yandex Direct {#yandex-direct}

If you have remarketing campaigns in Yandex Direct, you need to do the following to ensure correct detection of attribution sources and allow automatic tracking:

1. Prepare your app:

   {% list tabs %}

   - Android

     1. Add [deeplink support](https://developer.android.com/training/app-links/deep-linking#adding-filters) to your app.
     2. If your app uses the AppMetrica SDK version lower than 4.0.0, [enable deeplink tracking for Android](../data-collection/deeplinks.md).

   - iOS

     1. Make sure that you have the AppMetrica SDK version 3.1.2 or higher.
     2. Add [Universal Links support](../sdk/ios/analytics/ios-universal-links.md) to your app.
     3. Add [deeplink tracking for iOS](../sdk/ios/analytics/ios-operations.md#deeplink).

   {% endlist %}

2. Add your app to Yandex Direct.

3. In AppMetrica, you'll see a new automatic remarketing tracker with the Yandex Direct media source. After you add your app to Yandex Direct, AppMetrica automatically sends attributed events to Yandex Direct. To view analytics, use the [Remarketing](../mobile-reports/remarketing-report.md) report.

### Importing attributions from other SDKs {#import-attribution}

If you use attribution in other SDKs, you need to do the following to ensure correct detection of attribution sources and allow automatic tracking:

1. Set up [importing attributions from other SDKs](../data-collection/attribution-integration.yaml).
2. The algorithm checks and compares the parameters retrieved from the third-party tracking system with the parameters of a media source in AppMetrica. If the parameters match a known media source, AppMetrica creates an automatic tracker for this media source. If not, AppMetrica creates an automatic tracker with the **Unknown publishers TrackingSystem** media source.

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
