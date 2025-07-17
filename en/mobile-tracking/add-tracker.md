# Creating a tracker

{% note alert "" %}

You can only create a tracker after you integrate the AppMetrica SDK. For more information, see [Android](../sdk/android/analytics/quick-start.md) | [iOS](../sdk/ios/analytics/quick-start.md) SDK integration.

{% endnote %}

This section explains the steps for creating a tracker and getting [the tracking URL](*the tracking URL). The behavior of the tracking link varies depending on these conditions:

 - If the app is already installed, it opens the app directly.
 - If the app isn't installed, it takes the user to the app store for download.

The tracking link is used in ad campaigns to monitor app installs and opens.

{% note info "" %}

AppMetrica features an automated solution for click spam protection. It automatically blocks trackers with a large number of clicks and abnormally low click-to-install conversion rate on a daily basis. AppMetrica won't perform attribution for these trackers. Their historical data won't change.

{% endnote %}

## Step 1. Fill in the campaign details {#step1}

1. In the AppMetrica interface, go to **Tracking** → **Create tracker**.

2. In the **Campaign details** block fill in all fields:

   - **Pre-installing**: Enable this option to create a tracker for pre-installs. Learn more about [creating a tracker for pre-installs](add-preinstall.md).
   - **This is a remarketing tracker**: A flag indicating that the tracker is being created for a [remarketing campaign](*remarketing campaigns). For more information, see [Creating a remarketing tracker](add-remarketing-tracker.md).
   - **Antifraud by FraudScore**: Enable this option to check installs and events for fraud via {% if tld == "ru" %}[FraudScore](../common/fraud-score.md){% else %}FraudScore{% endif %}.

      The option is not available for the media sources Google Ads, Google Search, and Yandex.Direct.

      {% cut "Learn more" %}

      This is a paid option ([Pricing plans](../common/pricing/ru-currency.md)) only available for legal entities registered in Russia.

      {% endcut %}

   - **Tracker name**: A name for the tracker. After being created, the tracker is available in the list with the specified name.
   - **Application**: The application the tracker is being created for.
   - **Media Source**: The media source to attribute clicks, installs, and conversions to. You can use a tracker with media sources from the list, in any advertising network that supports tracking links, and on external sites.
   If the media source isn't in the list, [add a new source](add-partner.md). After being added, the new source will be saved in the list.

    {% note info "" %}

    Once the tracker has been created, you can't change the media source in the settings.

    {% endnote %}

## Step 2. Configure a SmartLink {#step2}

{% include [smart-link](_includes/smart-link.md) %}

## Step 3. Configure the app redirect {#step3}

1. Android: Add a deeplink to your smartlink.
1. iOS 12.3+: Deeplinks are no longer supported in regular tracking URLs. To ensure the link opens the app, follow the [instructions](../sdk/ios/analytics/ios-universal-links.md#types) to enable Universal Links support.
1. Once you've completed the [instructions](../sdk/ios/analytics/ios-universal-links.md#types), the tracker will generate an app-to-app tracking URL that you can use for both platforms.

    {% list tabs %}

    - App not installed

      The app-to-app tracking URL behaves as a regular tracking URL.

    - App installed

      - For Android devices, the app is opened via a redirect to the regular deeplink specified in the tracker settings.
      - On iOS, the app is opened using Universal Links.

    {% endlist %}

## Step 4. *(Optional)*  Configure attribution {#step4}

{% include [attribution](_includes/attribution.md) %}

## Step 5. *(Optional)*  Configure postbacks {#step5}

{% include [postback](_includes/postback.md) %}

## Step 6. Save changes and test the tracker {#step6}

1. Click the **{{ save }}** button at the bottom of the page.
    The list of all saved trackers are in the **Trackers** section. You can edit and archive them. The statistics from archived trackers remain available in reports.

2. Test the tracker before launching an advertising campaign. For more information, see [Testing a tracker](testing-attribution.md).

## Step 7. Use the created tracking link {#step7}

{% note alert "" %}

Don't use the `target= "_blank"` attribute when inserting a URL into the markup. Some browsers may block the click-through when opening a URL in a new window.
Don't place the URL in the `iframe` element.

{% endnote %}

![](../../_images/tracking-url-desc-{{ locale }}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

{% note info "" %}

For the URL to open an iOS app, use an app-to-app tracking link. The app must be installed.

{% endnote %}

Use the tracking URL in an ad campaign after successful testing. For this, copy the URL from the **Tracking URL** section.

{% note info "" %}

For the URL to open an iOS app, copy the URL from the **app-to-app tracking link** section.

{% endnote %}

In a tracking URL, you can specify predefined, static (UTM), and custom parameters that will be passed to the destination URL, deeplink, and postback URLs. For example, you can disable JavaScript redirect using the `appmetrica_js_redirect=0` parameter:
```
https://redirect.appmetrica.yandex.com/serve/123456?appmetrica_js_redirect=0
```

For more information, see [Parameters of the tracking URL](tracking-specification.md).

For impression attribution, use the following link:

```
https://impression.appmetrica.yandex.com/serve/123456
```

## Learn more {#learn-more}

- [How can I create a tracking URL for other install sources?](../troubleshooting/troubleshooting.md#tracking-url)
- [AppMetrica Blog: Parameters of the tracking URL](https://appmetrica.yandex.ru/blog/custom-url-parameters)
- [Does AppMetrica use UTM tags?](../troubleshooting/troubleshooting.md#utm)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*remarketing campaigns]: An ad campaign aimed at getting users to come back to an app they previously installed. For more information, see [Creating a remarketing tracker](add-remarketing-tracker.md).

[*the tracking URL]: A link formatted as `https://redirect.appmetrica.yandex.com/serve/*` that takes the user to the app store to install the app. If the app is already installed, it opens the app provided a deeplink is specified. Created when setting up the tracker. For more information, see [What is tracking?](index.md).

[*Postbacks]: A GET request to a specified URL, which is known as the postback URL. The request can include specific parameters. You can add up to 5 requests per campaign. For more information, see the [postback policy](policy.md).

[*PostbackURL]: A link for sending an event message (about an install or a conversion). The event recipient is a partner. You can [send additional parameters](postback-specification.md) to the postback URL.
