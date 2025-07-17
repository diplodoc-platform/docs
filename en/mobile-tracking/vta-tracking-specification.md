# Impression attribution

Impression attribution, also known as post-view attribution or view-through attribution (VTA), accounts for cases where the user didn't navigate to the app store via an ad click but still installed your app shortly after viewing the ad. For some channels, there can be far more of them than the regular post-click installs. Sending post-impression install data in postbacks helps the ad network optimize their algorithms.

## Impression attribution conditions {#conditions}

Installs are attributed to impressions under the following conditions:

- The impression occurred within the attribution window — no earlier than 24 hours before the install.
- If multiple impressions are found, the install will be attributed to the latest impression.
- Clicks take precedence over impressions. If a click was found within the attribution window for an install, the install is attributed to it.
- Go to the advertising network and set up impression delivery to AppMetrica using the special link you get when setting up the tracker. No additional settings in AppMetrica are required.

## Setting up tracking {#setup}

The setup process is similar to click attribution setup and involves [creating a tracker](add-tracker.md). Details for setting up impression attribution:

1. During the [postback setup](add-tracker.md#step5) stage, use the `{attributed_touch_type}` macro to send the attribution type to the ad network. That helps the ad network optimize better and display more accurate statistics.

2. When setting up a campaign in the advertising network, use a [link for sending impressions](add-tracker.md#impression-link) rather than a tracking link. Use the same [parameters](tracking-specification.md) as in the tracking link.

3. When creating a tracker, in the **Attribution settings** tab, you can adjust the attribution window. There, you can also completely disable impression attribution.

{% note alert "" %}

You can't use impression attribution in channels that don't support tracking links.

{% endnote %}

## Evaluating results {#result}

**Reports**
:   Use the User Acquisition report. Installs attributed to impressions are displayed in the overall statistics the same as any others. Install data is stored in the attributed impression parameters.

    To see the impact impression attribution has, use the **Attribution type** dimension. You can also add a variety of metrics to the report, both on the chart and in the table. For more information on report setup, see [User Acquisition](../mobile-reports/user-acquisition-report.md).

**Segmentation**
:   Every install is linked to its attributed impression — the partner, tracker, and install parameters. For data filtering during [segmentation](../mobile-reports/segmentation.md), use the **Attribution type** parameter.

**Data export and Logs API**
:   Data for impressions is stored in the parameters of the installs attributed to them. To identify installations during [export](../mobile-api/logs/about.md), use the additional `attributed_touch_type` parameter. A similar parameter is available for postbacks.

    By default, impressions are exported along with clicks. Use the `touch_type` parameter to identify them.

## Restrictions {#restriction}

**Attribution window**
:   The attribution interval is 24 hours. Impressions that occur more than 24 hours before the first app launch are not used for attribution.

**Supported sources**
:   Tracking is available for ad networks that support placement of impression attribution links.

**Restriction**
:   Impressions from trackers that show both substantial volumes and abnormally low conversion rates for these placements may be excluded from processing. Excluding them helps prevent data distortion in reports due to tracker misuse (click flooding, for example).

**Types of tracked campaigns**
:   We support install attribution. We do not support attribution of re-engagement in remarketing campaigns.

## Learn more {#learn-more}

- [App install attribution](policy.md)
- [How to create a tracker](add-tracker.md)
- [Tracking link structure and parameters](tracking-specification.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
