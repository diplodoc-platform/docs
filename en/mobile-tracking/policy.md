# App install attribution

This attribution type correctly detects the source that brought users to your app and accurately links app installs to ad interactions, whether they're a click or an impression.

AppMetrica uses the "last-click" approach when linking an app install to a click. This helps avoid multiple attributions and attributes the install to the last media source that brought the user to app installation.

If no click is found for an install, the install will be attributed to the source of the last impression. For more information, see [Impression attribution](vta-tracking-specification.md).

Let's look at an example of an app that is promoted through multiple advertising partners.

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-tracking/07rulastclick.png)

## Attribution interval {#interval}

To ensure accurate and precise attribution, AppMetrica sets a restriction on the interval between the ad interaction and app install.

For click attribution when using Device Identifier Matching or Install Referrer, the interval is ten days, while it's 24 hours for Device Fingerprint Matching. You can change the timeframe when [adding a tracker](add-tracker.md): from 1 to 10 days, and from 1 to 24 hours, respectively.

The interval limit for impression attribution is 24 hours regardless of the method.

If the interval between the ad interaction and app install was longer than specified, the install will be marked as organic rather than being attributed to the partner.

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-tracking/05ruwatrib-1.png)

## Deduplication of clicks {#deduplication}

To make the conversion tracker report as accurate as possible, AppMetrica performs click deduplication. Deduplication uses the value of the `click_id` parameter in the [tracking URL](tracking-specification.md).

If this parameter is omitted or null, the click is considered unique. Otherwise, AppMetrica searches for a matching `click_id` from this media source in this tracker over the past 7 days. If matching `click_id`'s were found, the new click isn't counted (it isn't shown in the report and isn't linked to installs).

## Reattribution {#reattribution}

In AppMetrica, reattribution is attribution of repeat installs by pre-existing users from advertising channels tracked using AppMetrica. Reattribution is disabled by default. If reattribution is disabled, new installs on a device that previously had attributed installs are considered reinstalls and are not displayed in reports. You can find them in the [Logs API](../mobile-api/logs/endpoints.md#installations) by setting the `is_reinstallation` parameter. If more than 180 days have passed between the attributed install and the reinstall, the source will be overwritten.

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-tracking/06rureattribution.png)

{% note info %}

The installation isn't counted as new if reattribution assigned it to the same tracker as the previous installation. For example, if you install an app from one device using the MyCampaign tracker link (where reattribution is enabled), then delete and install it again, the **User Acquisition** report will show one installation, and postback will be sent only for the first one.

{% endnote %}

The reattribution policy can be changed in the [tracker settings](add-tracker.md). When reattribution is enabled, installs on the same device might be attributed multiple times to different sources.

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-tracking/06ruonreattribution.png)

AppMetrica supports setting a list of test devices that always have reattribution allowed. This can be useful for testing advertising campaigns before a launch.

## Restrictions {#restrictions}

Clicks from trackers that show both substantial volumes and abnormally low conversion rates for these placements may be excluded from processing. Excluding them helps prevent data distortion in reports due to tracker misuse (click flooding, for example).

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
