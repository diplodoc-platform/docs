# AppMetrica tracking technology

App installs are tracked using [attribution](policy.md). AppMetrica uses several attribution methods. They are applied in descending order of accuracy, progressively relaxing the strictness of criteria.

If Device Identifier Matching can't be used, AppMetrica tries to use Install Referrer. If an appropriate Install Referrer wasn't found or this method can't be used (on iOS), Probabilistic Matching is used.

## Device Identifier Matching {#device-identifier-matching}

Details:

- Nearly 100% accurate attribution.
- 10-day attribution window for clicks (the time between the click and the first launch) and 24-hour window for impressions.
- Not all advertising networks support it.

To use this method, the device ID must be transmitted from the advertising network side in most cases.

In some cases, advertising networks don't have access to the device ID. This is usually mobile apps ads. Clicks from this type of ad rarely have information about the device ID.

### How it works {#device-identifier-matching}

1. Your app is promoted in an advertising network that can get the device ID. When a user clicks the ad, the advertising network inserts various parameters in the tracking URL according to a template. One of these parameters is the device ID.

   AppMetrica supports the following types of IDs:

   {% list tabs %}

   - Android

      `google_aid` (Google Advertising ID) and its hashed derivatives

   - iOS

      `ios_ifa` (Apple Identifier for Advertising) and its hashed derivatives

   {% endlist %}

   For more information about parameters, see [Parameters of the tracking URL](tracking-specification.md).

   AppMetrica stores these IDs bound to the click. After clicking, the user goes to the app store to install.

2. When the app has been installed and launched, the AppMetrica SDK collects information about the device, including the device ID, and sends the data to the AppMetrica server.
3. AppMetrica matches the device IDs from the click and the initial app launch.
4. Information about the install is sent to the advertising network via postback. For more information, see [Postback parameters](postback-specification.md).

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-tracking/01rudeviceid-1.png)

## Install Referrer {#install-referrer}

Details:

- Nearly 100% accurate attribution.
- 10-day attribution window for clicks (the time between the click and the first launch) and 24-hour window for impressions.
- Only used for Play Market and Yandex.Store.
- Doesn't require transmitting the device ID from the advertising network.
- Requires [app install source tracking](../sdk/android/analytics/android-operations.md). We recommend using the SDK to set up tracking in advance.

### How it works {#install-referrer}

1. A user clicks an ad for the app. While passing through the redirect service to the targeted link (the one that goes to the app store), a special `&referrer=` parameter with a unique click ID (`ym_tracking_id`) is appended to the link. After the click, the user is redirected to the app store to install.

    {% note info %}
    
    If [S2S](s2s.md) is used, then the unique identifier must be transmitted independently.
    
    {% endnote %}
    
    
2. When the app has been installed and launched, the AppMetrica SDK can get `INSTALL_REFERRER` containing the value of the `ym_tracking_id` parameter from the app store.
3. AppMetrica matches the value of the `ym_tracking_id` parameter for the click and the initial app launch.
4. Information about the install is sent to the advertising network via postback. For more information, see [Postback parameters](postback-specification.md).

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-tracking/02rureferrer-1.png)

## Probabilistic Matching {#device-fingerprint-matching}

Details:

- AppMetrica's heuristic algorithm provides highly accurate attribution.
- 24-hour attribution interval (the time between the click and the first launch).
- Doesn't require transmitting the device ID from the advertising network.
- Attribution is possible for any type of ad placement: in apps, or mobile internet.

This method uses unique AppMetrica technology with excellent attribution accuracy.

### How it works {#device-fingerprint-matching}

1. A user clicks an ad for the app. The redirect service collects all the fingerprint information: the browser User-Agent, the device IP address, the time, and so on. After the click, the user is redirected to the app store to install the app.
2. After the app is installed and launched, the AppMetrica SDK collects information about the device and sends it to the AppMetrica server.
3. AppMetrica correlates parameters from the click and the initial launch of the app and links the installation to the click.
4. Information about the install is sent to the advertising network via postback. For more information, see [Postback parameters](postback-specification.md).

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-tracking/03rufingerprint-1.png)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
