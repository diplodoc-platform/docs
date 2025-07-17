# Tracking in iOS 14.5+

## Changes in iOS 14.5 {#new-ios-version}

Starting with iOS 14.5, by default, apps and ad networks don't have access to the IDFA, a device ID that helps them recognize the same user across the apps.

There are two was to [request](ios-tracking.md) IDFA access from the user:

- Show the selection window when the app starts, but only once.
- Suggest going to system settings.
   If the user refuses, you can't identify the device.

Previously, the device owner could also prohibit apps from receiving the IDFA (through the same system settings), but only a small percentage of users did this. Now the share of users without an IDFA will grow significantly.

Along with this restriction, Apple's new rules prohibit attempts to identify the device in other ways, including heuristic ones: the company does not allow the use of fingerprints or probability matching.

## What does the lack of IDFA affect? {#idfa}

**Behavioral targeting**

:   In a number of advertising networks, the ability to target by behavioral characteristics of the audience will decrease. Applications will no longer recognize the user and show them relevant ads, so ad effectiveness will decrease.

**Advertising campaign optimization**

:   The advertising partner won't be able to adjust settings on the fly to show ads to the users who convert more. Without the IDFA, it's impossible to choose the users with higher conversion from the entire audience.

**App install attribution**

:   Attribution of iOS installations and subsequent target actions (for devices without an IDFA) will no longer work in mobile measurement partners. If the user doesn't allow IDFA access, the mobile measurement partner won't be able to track specific traffic sources, so the default settings will fall under organic installations.

**Completeness of statistics**

:   Apple's statistics will be aggregated and won't combine with other metrics in the reports, so it will be more difficult to compare site efficiency. It also won't be possible to reliably evaluate the LTV of users who were brought by one advertising network or another.

## SKAdNetwork {#SKAdNetwork}

Apple offers its own attribution: [SKAdNetwork](https://developer.apple.com/documentation/storekit/skadnetwork). It will work even for those users who didn't give tracking permission. This is the only way to calculate complete and accurate statistics.

For this, ad networks must send data about ad placements to Apple, and developers and publishers must send data about conversions from their apps. Sending takes place through the Apple framework: SKAdNetwork, which must be supported by both parties. Apple will return statistics through it, but in an unusual form: the platform won't generate reports. Instead, ad networks will receive aggregated click and installation data from Apple. They can collect them in separate reports and broadcast them to advertisers.

In the new model, trackers don't receive data from SKAdNetwork by default. However, ad networks can [pass](ios-tracking-skadnetwork.md) the data received from Apple to mobile measurement partners so that advertisers can evaluate the efficiency of different channels in a single interface.

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/apple-attribution.png){style="border: solid 1px #cccccc; max-width: 800px;"}

## What do statistics look like in AppMetrica? {#report}

To analyze install sources from iOS 14.5+, there's a separate report with aggregated data from advertising networks that they receive through SKAdNetwork:

The User Acquisition report displays statistics on app install sources obtained from SKAdNetwork. Segmentation and event metrics calculated according to AppMetrica data aren't available in the report.

[Learn more about the report](../mobile-reports/user-acquisition-skadnetwork.md).

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/report-ios-14-2.png){style="border: solid 1px #cccccc; max-width: 800px;"}

## Apple Search Ads {#apple-search-ads}

The release of iOS 14.5 won't affect the capabilities of Apple Search Ads, Apple's own app promotion platform, where attribution works differently. AdServices, another new framework from Apple, provides attribution of a specific device, but doesn't disclose the device IDFA to the developer. This allows you to keep the usual benefits of tracking (accurate counting of conversions and actions in the app by user), as well as grant the ability to segment users and explore their behavior in the app.

{% note info %}

Apple Search Ads doesn't work through SKAdNetwork.

{% endnote %}

You can read about campaign tracking in Apple Search Ads on this [page](searchads-settings.md).

## Requesting IDFA access via App Tracking Transparency {#request}

When working with iOS 14, use the new [App Tracking Transparency](https://developer.apple.com/documentation/apptrackingtransparency) framework. Use it to display the system dialog box in your application. In the window, the user will choose to allow or deny IDFA access.

{% note info %}

The system dialog box can only be displayed once each time the application is installed. If the user chooses **Ask App Not to Track**, there will be no way to show this window again for this application.

{% endnote %}

1. The system dialog box can't be changed, but you can add text with an explanation. To do this, add the `NSUserTrackingUsageDescription` key to `Info.plist`. For example:

   ```no-highlight translate=no
   <key>NSUserTrackingUsageDescription</key>
   <string>This identifier will be used to deliver personalized ads to you.</string>
   ```

   The text from `Info.plist` will be shown to the user in the system dialog box. In this text, explain to the user why the app requests permission to use the IDFA.

2. To display a dialog box requesting IDFA access, call the [requestTrackingAuthorization(completionHandler:)](https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/3547037-requesttrackingauthorization) method.

   {% cut "Example of a system dialog box" %}

   ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/alert-ios-14.png){style="border: solid 1px #cccccc; max-width: 800px;"}

   {% endcut %}

3. Wait until you receive the callback before loading the ad. Then the Yandex Mobile Ads SDK will be able to use the IDFA in the ad requests.

   ```objectivec translate=no
   #import <AppTrackingTransparency/AppTrackingTransparency.h>
   ...
   - (void)requestTrackingAuthorization {
   [ATTrackingManager requestTrackingAuthorizationWithCompletionHandler:^(ATTrackingManagerAuthorizationStatus status) {
   // Start ad loading
   }];
   }
   ```

4. To check the App Tracking Transparency authorization status, use the [trackingAuthorizationStatus](https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/3547038-trackingauthorizationstatus) property.

For more information on App Tracking Transparency, see the [Apple](https://developer.apple.com/documentation/apptrackingtransparency) documentation.

[Learn more](ios15-tracking.md) about tracking in iOS 15 apps.

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
