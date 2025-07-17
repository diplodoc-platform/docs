# Testing attribution

To make sure that the tracking is set up correctly, test the attribution work before launching the ad campaign.

For more information about attribution, see [Attributing app installs](policy.md).

The section below describes the steps of testing the attribution:

## Step 1. Enable the "Reattribution" option or test with a test device {#test}

{% list tabs %}

- Enabling Reattribution

   In AppMetrica, same-device installs are attributed to the partner only once. All subsequent installs of the same app are considered reinstalls and are not reflected in reports.

   Enabling [reattribution](https://appmetrica.yandex.ru/docs/en/mobile-tracking/policy#reattribute) allows you to count a reinstall if the previous install was from a different source:

   1. Go to the settings of the tracker you want to test.
   2. On the **Attribution settings** tab, select **Reattribution** and keep this option enabled while testing the tracker.
   3. Make sure to disable it after you complete the test.

   {% note warning %}

   If the previous install on the device was from the same tracker, the new install isn't counted a second time even with reattribution enabled. Use a different tracker for testing or add the device to the list of test devices for reattribution.

   {% endnote %}

- Using a test device

   All installs are considered new for a test device, including reinstalls on the same tracker. To add a test device:

   1. Go to **Settings** and select **Test devices**.
   2. Enter the device name and ID: Google AID and Apple IDFA are available.

      {% cut "How to get Google AID" %}

      Open the "Google settings" app on the device and go to **Ads** in the menu. Google AID is shown on the screen (**Your advertising identifier**).

      {% note alert %}

      Android grants access to the advertising ID by default, but its availability may be [restricted](https://appmetrica.yandex.ru/docs/en/sdk/android/get-ad-id) by developers — this can be the case with apps for kids where ID collection is prohibited by the Google Play policy.

      {% cut "How to check that the app is collecting advertising IDs" %}

      To check whether an app has access to GAID, export raw install data via the **Data export** tab or the Logs API. If the `google_aid` field is filled in when installing the latest app version, then ID collection on Android works.

      Another method is to check the app settings on the device. Find **All permissions** on your device: there should be the **Permission for the advertising ID** item. The location of this menu and wording may vary depending on the device firmware.

      {% endcut %}

      {% endnote %}

      {% endcut %}

      {% cut "How to get Apple IDFA" %}

      1. Install the app [The Identifiers](https://itunes.apple.com/us/app/the-identifiers/id564618183) on the device.
      2. In the app, open the **Raw** tab. Your device's IDFA is shown in **Advertising Identifier**.

      {% note alert %}

      Starting with iOS 14.5, apps can no longer access Apple's IDFA. If access to it isn't requested before the AppMetrica SDK initialization, adding the device to the list of test devices by IDFA won't work. In this case, testing is possible only via reattribution in the tracker settings.

      {% cut "How to check whether the app is collecting advertising IDs" %}

      Check that the app has a tracking permission either in the settings or in the relevant window the first time you run the app after reinstall.

      {% endcut %}

      {% endnote %}

      {% endcut %}

   3. Specify the **Purpose** and click **Add**.

   You don't need to enable reattribution in the tracker when using a test device.

{% endlist %}

## Step 2. Click the tracking URL and install the app {#check-the-link}

To test the tracker, open the tracking URL on the test device.

1. Send the tracking URL to the test device. For example:
   - Save the tracking URL in notes;
   - Send the tracking URL to the device via email;
   - (_recommended_) Put the tracking URL on a static web page. In this case, the `rel` attribute of the HTML link should not contain `noopener noreferrer` value.

   {% note alert %}

   Don't use messengers to send tracking URL. Some messengers can remove AppMetrica redirects and send users directly to the app store. In AppMetrica, attribution does not work without redirects.

   {% endnote %}

2. Click the tracking URL.
3. Install the app from the app store and launch it. After the start, use the app for a few seconds.

## Step 3. Make sure the install appeared in the report {#check-the-report}

The install should now have appeared in the **User Acquisition** report. You can view information about installs in the web interface:

1. Open the **User Acquisition** report.
2. Select the tracker that you are testing attribution for.
3. Make sure that the number of installs for your tracker has changed.

{% note info %}

If the install hasn't appeared in the report, wait for 10–15 minutes: there may be a delay when AppMetrica servers experience increased network load.

{% endnote %}

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
