# Tracking in iOS 15

Starting with iOS 15, you can set up sending SKAdNetwork postback directly from Apple to AppMetrica. In this case, the [User Acquisition SKAdNetwork](../mobile-reports/user-acquisition-skadnetwork.md) report collects data on ad-triggered installations of all users including those that haven't granted access to their IDFA.

## Configuring sending postback copies to AppMetrica {#ios15-postbacks}

To send postback copies about installations:

1. Select the `Info.plist` file in the project navigator in Xcode.
2. Add the new key to the properties list.
3. Enter the key name [NSAdvertisingAttributionReportEndpoint](https://developer.apple.com/documentation/bundleresources/information_property_list/nsadvertisingattributionreportendpoint?changes=latest_minor).
4. Enter the String property type.
5. In the property value, enter **https://appmetrica.yandex** — the URL to receive SKAdNetwork postbacks in AppMetrica.

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
