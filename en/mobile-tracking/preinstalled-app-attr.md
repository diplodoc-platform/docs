# Tracking pre-installed apps

Preinstalls are app installs on devices that occur without a direct user interaction. AppMetrica offers a number of methods for tracking pre-installed apps.

AppMetrica supports attributions for several pre-install types:

- Apps pre-installed by the device manufacturer or retailer.
- Apps pre-installed with PAI.

## Apps pre-installed by the device manufacturer or retailer {#apk}

Pre-installing is a popular method of app distribution. AppMetrica allows you to track activation of pre-installed apps by using tracker data. This data is transmitted using `tracking_ID`. More details on [how to create a tracker](add-preinstall.md#apk) and [get tracking_ID](add-preinstall.md#tracking-id).

![](../../_images/preinst-app-{{ locale }}.png)

For example, you've partnered with a vendor who distributes your app by pre-installing it on devices. All activations of the pre-installed app should be attributed to this partner. In order for this to happen, the first time the app is opened, it should send the AppMetrica SDK information that this is a special build of the app for pre-installation, along with information about the partner.

The AppMetrica SDK has special setter methods for storing ("hard coding") partner information for attribution and sending postbacks. If you have multiple partners who pre-install the app, create a separate app build for each partner. The build should have settings with various information about the partner that this build is for.

## Pre-installing apps with PAI (Google Play Auto Install) {#pai}

{% note info %}

This method only works for apps published on Google Play.

{% endnote %}

The apps are automatically downloaded and installed from the app store when a device is first activated. AppMetrica allows you to track activation of pre-installed apps by using tracker data. This data is transmitted using `utm_campaign`. More details on [creating a tracker](add-preinstall.md#pai) for this method.

When the user first launches the app, the embedded AppMetrica SDK sends a request to the Google Play Install Referrer API. In response, AppMetrica receives the same `install_referrer` with `utm_campaign` which links the install to a specific campaign and media source.

## See also

- [Creating a tracker for apps pre-installed by the device manufacturer](add-preinstall.md#apk)
- [Creating a tracker for PAI pre-installs](add-preinstall.md#pai)
- [How does tracking pre-installs differ from tracking a separate app build?](../troubleshooting/troubleshooting.md#differences)

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
