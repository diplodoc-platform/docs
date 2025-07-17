# Tracking Google Ads campaigns

AppMetrica allows you to track Google Ads advertising campaigns.

To enable tracking, you should link the AppMetrica and Google Ads accounts via the link identifier that is used for attributing the installation source.

## How tracking works

Google Ads tracking requires collecting advertising IDs (GAID/IDFA) from devices. If the app doesn't collect advertising IDs, tracking won't work.

#### Android

Access to [advertising IDs](../sdk/android/get-ad-id) is granted by default.

#### iOS

{% note alert %}

Starting from version 14.5, apps don't have access to IDFA by default. To enable tracking, you have to implement an [access request for IDFA](../mobile-tracking/ios-tracking#request).

{% endnote %}

This section explains the steps for setting up AppMetrica tracking to work with Google Ads ad campaigns:

## Step 1. Get the Google Ads link ID {#step6}

Create a link to AppMetrica for advertised app in the Google Ads web interface:

1. Sign in to the Google Ads account and click **Tools**&nbsp;![Tools](../../_images/tools.png){width=20px} in the pages menu.
2. In the section menu select **Data Manager**.
3. On the **Data Manager** page click **Connect product**.
4. Select **Third-party app analytics** and click **Continue**
5. Click **Create link ID** if you link accounts for the first time, or the **+** button if your account already linked AppMetrica or other third-party app analytics accounts.
6. In the **App analytics provider** drop-down list, select **Other provider**. Specify the provider ID AppMetrica — 1444794547.
7. Select the platform of the mobile app.
8. Find the advertised application using the search field.
9. Click **Create link ID**.
10. Copy the received link ID and use it when creating a tracker in AppMetrica.

## Step 2. Create a tracker in AppMetrica {#step2}

[Create a tracker](add-tracker.md) in the AppMetrica interface. Pay special attention to the following settings:

1. Go to the **Campaign details** section and choose **Google Ads** as a media source.
2. In the section that opens, fill in the **Link id** field.
3. _(Optional)_ To track conversions in the Google Ads interface, set up sending target events in **Postback settings** of AppMetrica. More information about setting up [postbacks](add-tracker.md#step5).

{% note alert %}

You don't need to configure the **Installation postback** for Google Ads. Attribution to the source is performed by link ID.

{% endnote %}

## Step 3. Import conversions {#step3}

After your ad campaign launches, import the events in the Google Ads interface:

1. In the Google Ads account in the pages menu click **Goals**&nbsp;![Goals](../../_images/goals.png){width=20px}.
2. In the section menu expand the list **Conversions**.
3. Select **Summary**.
4. Click **New conversion action**.
5. Select **Import**&nbsp;→**Third-party app analytics** and click **Continue**.
6. Select the `first_open` event of the advertised application.

    {% note info %}

    You can also select target events that are sent via [postback](*postback).

    {% endnote %}

7. Click **Import and continue**.

{% note alert %}

Events for import can be displayed with a delay. If events do not appear immediately, start the Google Ads campaign and check the list after a few hours.

{% endnote %}

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*postback]: A GET request to the specified URL (the postback URL), which certain parameters can be sent to. You can add up to 5 requests per campaign. For more information, see the [postback policy](policy.md).


