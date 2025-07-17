# Tracking Apple Search Ads campaigns

AppMetrica tracks Apple Search Ads campaigns. Apple links app installations from Search Ads on its own.

{% note info %}

For full attribution of Apple Search Ads on devices running iOS 14.5 and higher, we recommend using the AppMetrica SDK 3.15.1 and later.

{% endnote %}

For iOS versions 14.5 and higher, the user is asked for permission to access the advertising ID and use tracking. For users who do not grant access to the IDFA, a new attribution system is used: AdServices Framework.

For iOS versions 14.4 and below, the old iAd Framework tracking method is supported. The AppMetrica SDK 2.9.4 or higher is suitable for this purpose.

For iOS 14.5 and higher, you can also use the iAd Framework, but users who haven't granted access to IDFA aren't attributed.

**Comparison of attribution systems**

#|
||   | **iAd framework** | **AdServices framework** ||
|| Supported iOS versions | 10 and higher | 14.3 and higher ||
|| Tracking for iOS 14.4 and lower | Access to IDFA isn't required. The iAd framework will still work. | Access to IDFA isn't required. The AdServices Framework works on devices running iOS versions 14.3–14.4. ||
|| Tracking restrictions for iOS 14.5 and higher | Only attributes users who have consented to tracking provided their IDFA is available in the app.

Doesn't attribute users who haven't granted access to their IDFA: `ATTrackingManager.AuthorizationStatus = denied` or `notDetermined` | Users who haven't granted access to their IDFA are attributed with fewer details (without the click date). ||
|| How to customize |
 - The AppMetrica SDK 2.9.4 or higher.
 - Add the iAd Framework library to the project according to the [instructions](#iad). | The AppMetrica SDK 3.15.1 or higher. ||
|| Available campaign parameters |

`iad-org-name` — String. The name of the organization that hosts the campaign.

`iad-org-id` — Integer. The ID of the organization that hosts the campaign.

`iad-campaign-id` — Integer. The ID of the campaign that the ad belongs to.

`iad-campaign-name` — String. The name of the campaign that the ad belongs to.

`iad-click-date` — Date/time string. The date and time of the ad click.

`iad-purchase-date` — Date/time string. The date and time when the user first downloaded your app. When `iad-conversion-type` takes the value `redownload`, `iad-purchase-date` is the date of the original download. It's possible that the download wasn't related to an ad in Apple Search Ads.

`iad-conversion-date` — Date/time string. The date and time when the user downloaded your app after clicking an ad.

`iad-conversion-type` — String. The type of conversion. Possible values: `new download` — first download, `redownload` — a download by users who installed your app before.

`iad-adgroup-id` — Integer. The ID of the ad group.

`iad-adgroup-name` — String. The name of the ad group.

`iad-country-or-region` — String. The country or region associated with the campaign that led to the installation.

`iad-keyword` — String. The keyword that led to the ad impression and click.

`iad-keyword-id` — Integer. The ID of the keyword that led to the ad impression.

`iad-keyword-matchtype` — String. The match type of keyword that led to the ad impression.

`iad-creativeset-id` — Integer. The ID of the creative set.

`iad-creativeset-name` — String. The name of the creative set. |

Only entity IDs are supported.

`orgId` — Integer. The ID of the organization that hosts the campaign.

`campaignId` — Integer. The ID of the campaign that the ad belongs to.

`conversionType` — String. The type of conversion. Possible values: `new download` — first download, `redownload` — a download by users who installed your app before.

`clickDate` — Date/time string. The date and time of the ad click.

`adGroupId` — Integer. The ID of the ad group.

`countryOrRegion` — String. The country or region associated with the campaign that led to the installation.

`keywordId` — Integer. The ID of the keyword that led to the ad impression and click.

`creativeSetId` — Integer. The ID of the creative set.

Names aren't supported. ||
|#

{% list tabs %}

- iAd Framework

  **Step 1. Integrate the iAd Framework**

  :   Integrate the iAd Framework into an application with the AppMetrica SDK installed, so that Apple Search Ads can detect and link app installations. Integration instructions are available [on the Search Ads site](https://developer.apple.com/documentation/iad/setting_up_apple_search_ads_attribution) (see paragraph **Add the iAd Framework to Your Xcode Project**).

      {% cut "Enabling the iAd framework in Unity" %}

      In the Unity 3D interface, go to **Settings** → **Other Settings** → **Scripting Define** → **Symbols**. Add the APP_METRICA_ADD_IAD_FRAMEWORK directive.

      {% note info %}

      If you added the iAd Framework in the Xcode project, you don't need to add the directive.

      {% endnote %}

      {% endcut %}

      After the iAd Framework is added, the AppMetrica SDK starts to detect installations from Apple Search Ads automatically.

  **Step 2. Perform a test installation**

  :   Create a test advertising campaign for Search Ads and install the application through ad placement. The tracker for this source will appear in the AppMetrica interface automatically.

  **Step 3. (_Optional_) Configure attribution**

  :   Set up the Search Ads attribution by using the tracker configuration:

      1. Go to the **Trackers** section. In order to filter the trackers by a media source, click on the **Media Source** drop-down list in the menu on the left and select **Apple Search Ads**.
      2. Choose the tracker to set up attribution for from the list. The tracker name matches the name of the Apple Search Ads campaign.
      3. Make the necessary changes to the **Attribution settings** section and click **Save**. Learn more about setting up [attribution](add-tracker.md#step4).

  **Step 4. (_Optional_) Configure postbacks**

  :   The campaign parameters can be sent in postbacks similar to macros. For example, to pass the campaign ID in the `campaign_id` parameter in the postback URL, specify `campaign_id={iad-campaign-id}`. You can also use all [system macros](postback-specification.md).

      Set up postbacks using the tracker settings:

      1. Go to the **Trackers** section. In order to filter the trackers by a media source, click on the **Media Source** drop-down list in the menu on the left and select **Apple Search Ads**.
      2. Choose the tracker to set up the postback for from the list. The tracker name matches the name of the Apple Search Ads campaign.
      3. Make the necessary changes to the **Postback settings** section and click **Save**. More information about setting up [postbacks](add-tracker.md#step5).

- AdServices Framework

  You can use AdServices Framework to attribute users who haven't allowed access to the advertising ID and tracking. To switch to this tracking system, update the AppMetrica SDK to version 3.15.1. No further configuration is necessary.

  The AppMetrica SDK versions 3.15.0 and below don't support AdServices Framework, and you can't attribute users without access to the IDFA.

  **Step 1. Perform a test installation**

  :   Create a test advertising campaign for Search Ads and install the application through ad placement. The tracker for this source will appear in the AppMetrica interface automatically:

      ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-tracking/searchads.png){style="border: solid 1px #cccccc; max-width: 800px;"}

  **Step 2. (_Optional_) Configure attribution**

  :   Set up the Search Ads attribution by using the tracker configuration:

      1. Go to the **Trackers** section. In order to filter the trackers by a media source, click on the **Media Source** drop-down list in the menu on the left and select **Apple Search Ads**.
      2. Choose the tracker to set up attribution for from the list. The tracker name matches the name of the Apple Search Ads campaign.
      3. Make the necessary changes to the **Attribution settings** section and click **Save**. Learn more about setting up [attribution](add-tracker.md#step4).

  **Step 3. (_Optional_) Configure postbacks**

  :   The campaign parameters can be sent in postbacks similar to macros. For example, to pass the campaign ID in the `campaign_id` parameter in the postback URL, specify `campaign_id={campaignId}`. You can also use all [system macros](postback-specification.md).

      Set up postbacks using the tracker settings:

      1. Go to the **Trackers** section. In order to filter the trackers by a media source, click on the **Media Source** drop-down list in the menu on the left and select **Apple Search Ads**.
      2. Choose the tracker to set up the postback for from the list. The tracker name matches the name of the Apple Search Ads campaign.
      3. Make the necessary changes to the **Postback settings** section and click **Save**. More information about setting up [postbacks](add-tracker.md#step5).

{% endlist %}

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
