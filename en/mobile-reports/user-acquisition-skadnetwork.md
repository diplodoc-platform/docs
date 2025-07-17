# User Acquisition SKAdNetwork

The User Acquisition SKAdNetwork report provides information on app installation sources obtained from SKAdNetwork. SKAdNetwork is a campaign attribution system for iOS 14.5 and higher that maintains user privacy. Segmentation and event metrics calculated according to AppMetrica data aren't available in the report. The User Acquisition report already includes these installations.

[Learn more about SKAdNetwork](../mobile-tracking/ios-tracking.md).

{% note info "" %}

You can view statistics on Apple Search Ads and the users who agreed to tracking in your app by using a regular [User Acquisition](user-acquisition-report.md) report.

{% endnote %}

## Report period {#period}

The report is based on the time when data is received from SKAdNetwork: because of the way this technology works, the data is received 24–48 hours after the first launch.

{% include [period](_includes/period.md) %}

## Dimensions and metrics {#groups-and-metrics}

{% include [groups-metrics](_includes/groups-metrics.md) %}

### Dimensions {#group} 

{% cut "SKAd: app" %}

- **App ID**. The app ID in the App Store.
- **Bundle ID**.

{% endcut %}

{% cut "SKAd: source parameters" %}

- **Partner ID in SKAd**. The advertising network ID in SKAdNetwork.
- **Partner**.
- **Campaign ID**.
- **App platform ID**. The ID of the app where the user clicked the ad.
- **SKAd protocol version**.
- **Fidelity type**. A technical parameter that indicates the ad type. For more information, see the [Apple](https://developer.apple.com/documentation/storekit/skadnetwork/signing_and_providing_ads) documentation for ad networks.

{% endcut %}

{% cut "SKAd: installation parameters" %}

- **Transaction ID**. The unique ID of the SKAd installation message.
- **Conversion value**.

{% endcut %}

{% cut "SKAd: [ad network parameters](*Ad network parameters)" %}

   - **Campaign ID**
   - **Campaign**
   - **Adset ID**
   - **Adset**
   - **Ad ID**
   - **Ad**

{% endcut %}

{% cut "Event date" %}

- **Install date**.

{% endcut %}

### Metrics {#measure}

{% cut "SKAd: default metrics" %}

- **All installs**
- **New installs**
- **Re-installs**
- **Conversions**

{% endcut %}

{% cut "SKAd: conversions" %}

- **Number of users**.
- **Conversion rate by user**.

{% endcut %}

{% cut "SKAd: number of events" %}

- **Number of users**.
- **Events**.
- **Conversion rate by user**.
- **Events per user**.

{% endcut %}

{% cut "SKAd: revenue" %}

- **Revenue**.
- **Paying users**.
- **Average revenue per user (ARPU)**.
- **Average revenue per paying user (ARPPU)**.

{% endcut %}

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*App ID]: The app ID in the App Store.

[*Partner ID in SKAd]: The advertising network ID in SKAdNetwork.

[*App platform ID]: The ID of the app where the user clicked the ad.

[*Install ID]: The unique ID of the SKAd installation message.

[*Ad network parameters]: Additional data received from the advertising network.

[*Conversions]: Installations with a non-zero conversion value.

[*Fidelity type]: A technical parameter that indicates the ad type. For more information, see the [Apple](https://developer.apple.com/documentation/storekit/skadnetwork/signing_and_providing_ads) documentation for ad networks.
