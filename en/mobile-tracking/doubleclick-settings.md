# Tracking DoubleClick campaigns

AppMetrica detects DoubleClick advertising campaigns by using [DoubleClick Floodlight](https://support.google.com/dcm/partner/answer/2823388).

{% note info %}

This article is intended for users who are familiar with the DoubleClick ad network and its settings.

{% endnote %}

This section explains the steps for setting up AppMetrica tracking to work with DoubleClick ad campaigns.

## Step 1. Create a tracker {#step1}

[Create a tracker](add-tracker.md) in the AppMetrica interface.

Pay special attention to the following settings:

1. Go to the **Campaign details** section and choose **DoubleClick** as a media source.
2. In the **DoubleClick** section that opens, fill in the following fields:

   ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-tracking/doubleclick-settings.png){style="border: solid 1px #cccccc; max-width: 800px;"}

   - **src** — The Advertiser ID. If you use **DoubleClick Bid Manager**, take the `src` value from the Floodlight tag settings. The value can be found in the Pixel setup screen.
   - **type** — The value that identifies the activity group, with which the Floodlight activity is associated.
   - **token** — The advertiser-specific string. It is transferred with each reqest to the **DoubleClick Bid Manager** server.
   - **cat** — The tag used by Floodlight servers.

## Step 2. Save the tracker {#step2}

Save the customized tracker. The tracker is available in the **Trackers** section.

## See also

- [About Floodlight](https://support.google.com/dcm/partner/answer/2823388)

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
