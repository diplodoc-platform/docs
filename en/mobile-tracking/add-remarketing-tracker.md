# Creating a remarketing tracker

{% note alert %}

You can only create a tracker after you integrate the AppMetrica SDK. For more information, see [Android](../sdk/android/analytics/quick-start.md) | [iOS](../sdk/ios/analytics/quick-start.md) SDK integration.

{% endnote %}

This section explains the steps for creating a tracker for a [remarketing campaign](*remarketing campaign).

AppMetrica uses a remarketing tracker to track user [re-engagement](*re-engagement) and new installs. The results of the remarketing campaign are available in the [Remarketing report](../mobile-reports/remarketing-report.md).

{% note info %}

You can configure Yandex Direct ad campaign targeting by AppMetrica segments. To do this, save a segment in AppMetrica and add it to [Yandex Audience](https://yandex.ru/support2/audience/en/segments/app-metrica). For more information, see [How to set up retargeting](https://yandex.com/adv/news/how-to-set-up-retargeting-for-ads-for-mobile-apps).

{% endnote %}

## Step 1. Prepare your app {#step1}

Before starting a remarketing campaign, prepare your app:

{% list tabs %}

- Android

   1. Add [deeplink support](https://developer.android.com/training/app-links/deep-linking#adding-filters) to your app.
   1. When using AppMetrica SDK version 4.0.0 or lower, add [tracking deeplink redirects for Android](../data-collection/deeplinks.md).

- iOS

   1. Make sure that you have the AppMetrica SDK version 3.1.2 or higher.
   2. Add [Universal Links support](../sdk/ios/analytics/ios-universal-links.md) to your app.
   3. Add tracking deeplink redirects for [iOS](../sdk/ios/analytics/ios-operations.md#deeplink).

{% endlist %}

## Step 2. Fill in the campaign details {#step2}

1. In the AppMetrica interface, go to **Tracking** → **Create tracker**.

2. Under **Campaign details**, enable the option **This is a remarketing tracker** and fill in the fields:
   - **Tracker name**: A name for the tracker. The tracker will be shown in the Trackers list with the specified name.
   - **Application**: The app you want to track.
   - **Media Source**: The media source to attribute clicks, installs, and conversions to. If the media source isn't in the list, you can [add](add-partner.md) it. After being added, the new source will be saved in the list.

   {% note info %}

   Once the tracker has been created, you can't change the media source in the settings.

   {% endnote %}

3. If you want to use a SmartLink to configure a destination URL, enable this option.
   A Smartlink enables you to create a single URL that leads to the app or relevant app stores on different platforms:

   - Use this option if the advertising network accepts an HTTP tracking URL.
   - Don't use this option if the advertising network accepts a deeplink.

   When enabling a Smartlink, add [Universal Links support](../sdk/ios/analytics/ios-universal-links.md) in the app.

## Step 3. Configure a destination URL / SmartLink {#step3}

{% list tabs %}

- Configuring a destination URL

   Fill in the fields of the **Destination link settings** section:

   ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-tracking/add-destination-url-remarketing.png){style="border: solid 1px #cccccc; max-width: 800px;"}

   Available fields:

   - **Platform**: The target platform — Android and iOS.
   - **Destination URL**: A link that leads to the app store or a page where the user can install the app.
   - **Deeplink**: A link in `myapp://some_data` format which can be used to send data to the app.

      {% note alert %}

      A deeplink is required for remarketing campaigns.

      {% endnote %}

- Configuring a SmartLink

   {% include [smart-link](_includes/smart-link.md) %}

{% endlist %}

## Step 4. _(Optional)_ Configure attribution {#step4}

{% include [attribution](_includes/attribution.md) %}

## Step 5. _(Optional)_ Configure postbacks {#step5}

{% include [postback](_includes/postback.md) %}

## Step 6. Use the created tracking URL and re-engagement deeplink {#step6}

{% note alert %}

Don't use the `target= "_blank"` attribute when inserting a URL into the markup. Some browsers may block the click-through when opening a URL in a new window.
Don't place the URL in the `iframe` element.

{% endnote %}

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-tracking/use-tracking-url-remarketing.png){style="border: solid 1px #cccccc; max-width: 800px;"}

The tracking URL and the re-engagement deeplink can be used in an ad campaign after successful testing. To do this, copy the URL that looks like `https://redirect.appmetrica.yandex.com/serve/123456` from the **Tracking URL** block .

In a tracking URL, you can specify predefined, static (UTM), and custom parameters that will be passed to the destination URL, deeplink, and postback URLs. For example, you can disable JavaScript redirect using the `appmetrica_js_redirect=0` parameter:
```
https://redirect.appmetrica.yandex.com/serve/123456?appmetrica_js_redirect=0
```
For more information, see [Parameters of the tracking URL](tracking-specification.md).

## Example {#example}

Launching a remarketing campaign for a mobile e-commerce app. The goal is for the user to view a specific screen (for example, a product page).

Depending on the advertising network, there are two ways to create a remarketing campaign:

- The advertising network accepts an HTTP tracking URL.
- The advertising network accepts a deeplink.

{% note info %}

Deeplinks in tracking URLs don't work on iOS 12.3 and higher. For remarketing campaigns to perform correctly, add [Universal Links support](../sdk/ios/analytics/ios-universal-links.md) to your app.

{% endnote %}

{% list tabs %}

- Tracking URL

   If you need to lead the user to an app, including on iOS, use an [app-to-app tracking URL](../sdk/ios/analytics/ios-universal-links.md#types). It will work for both platforms.
   Add the necessary parameters to an app-to-app tracking URL:
   - On Android, app redirects occur via the deeplink specified in the tracker. You can send the required parameters from the tracking URL to the Android deeplink. For more information, see [{#T}](tracking-specification.md).
   - On iOS, the app is opened with the URL itself, and tags from the URL are sent to AppMetrica and included in the report when there is a click-through.

- Re-engagement deeplink

   Add the necessary parameters to the deeplink.

{% endlist %}

## See also {#learn-more}

- [{#T}](remarketing-attribution.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*remarketing campaign]: An ad campaign aimed at getting users to come back to an app they previously installed.

[*re-engagement]: {{ re-engagement }}

[*Postbacks]: A GET request to a specified URL, which is known as the postback URL. The request can include specific parameters. You can add up to 5 requests per campaign. For more information, see the [postback policy](policy.md).

[*PostbackURL]: A link for sending an event message (about an install or a conversion). The event recipient is a partner. You can [send additional parameters](postback-specification.md) to the postback URL.
