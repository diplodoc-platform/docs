# Unified performance campaign (UPC) tracking

A [unified performance campaign](https://yandex.ru/support/direct/{{ locale }}/products-mobile-apps-ads/upc/about) (UPC) is a campaign creation tool that expands the capabilities of regular Yandex Direct campaigns and offers more flexibility for configuring ads for mobile apps.

AppMetrica helps you transmit data on new installs and in-app actions to Yandex Direct. This way, you can track conversions more accurately and optimize your campaigns.

To enable AppMetrica to record conversions and report them to Yandex Direct, follow these steps:

- [Create a tracker](#create-tracker) and get a [tracking URL](*tracking URL) — it will be used in your ad campaigns in Yandex Direct.

- [Add postbacks](#postback) for transmitting event data.

{% note info "" %}

The tracker identifies the source of installs. Postbacks send information about installs and events to the advertising system.

{% endnote %}

## Creating a tracker and getting a tracking URL {#setup-tracker}

1. In the AppMetrica interface, go to **{{ tracking }}** → **{{ create-tracker}}**.

    Enter the name of the tracker.

    If you're launching a remarketing campaign, enable **{{ this-is-a-remarketing-campaign }}**.

2. Choose your app in the **{{ application }}** drop-down list. The SDK should already be integrated into your app code. Learn more about adding the SDK for [Android](../sdk/android/analytics/quick-start.md) and [iOS](../sdk/ios/analytics/quick-start.md).

3. Choose **Yandex.Direct** in the **{{ media-source }}** drop-down list.

    You can't select any other media source: the pixel only works with Yandex Direct. If you need to choose a different media source to optimize your Yandex Direct campaign, contact [support](../troubleshooting/feedback-new.md), making sure to attach your tracker ID.

4. Under **SmartLink**, add one platform that you plan to advertise. Each operating system requires a separate campaign, so you can only specify a single platform per tracker.

    If you're launching a remarketing campaign, make sure to specify the **Deeplink**, having tested it beforehand.

    {% cut "How to test a deeplink" %}

    1. Open any URL shortener, such as [TinyURL](https://tinyurl.com/).

    1. Enter your deeplink in the source link field (long URL) and generate a short URL.

    1. Copy the resulting short URL and open it on your mobile device.

    If the app is installed and opens when you follow the link, everything works correctly. If the app doesn't open, contact your developer to check if you have the correct deeplink.

    {% endcut %}

5. We recommend skipping the **{{ attribution-settings }}** section and keeping the default values there. Learn more about the [tracking technology](technology.md).

## Setting up postbacks {#postback}

A postback for the **{{ event-installation }}** event is added automatically.

To transmit other in-app actions, click **{{ add-postback }}**. Select the type of event and the appropriate template.

{% note info "" %}

Campaigns for advertising mobile apps offer a predefined set of events with corresponding AppMetrica postback templates.  These event names exactly match the [goal names in Yandex Direct](https://yandex.ru/support/direct/{{ locale }}/strategies/average-cpa-mobile-apps#conditions).

{% endnote %}

You can select any event relevant to your application, for example: the **Purchased** event if you transfer the purchase; **Completed registration** if you register the user. Event in AppMetrica does not necessarily have to be named exactly the same way or capture exactly this action.

**Options**

- **{{ send-postback-on-first-target-event-only }}**

    Only the first conversion is sent to the ad network, and the rest are ignored.

    For example, suppose you selected the **Purchase** event and are sending it to the **Purchased** template. A user installed the app on January 1, made the first purchase on January 2, then made their second purchase on January 3. When this option is enabled, only the purchase dated January 2 will be sent to Yandex Direct. In AppMetrica, you'll still see all purchases.

- **{{ send-postback-on-actions-of-all-users }}**

    When this option is enabled, the ad network receives information about all the events selected in the postback, regardless of the install source.

    In these types of postbacks, attributed parameters are excluded to prevent the ad network from attributing installs from other sources to itself. If you need this option, create two postbacks: one with the option enabled and the other with the option disabled. In all other cases, we recommended leaving the option disabled.

  {% endnote %}

## Verifying an app in Yandex Direct {#verification}

If your ad manager and AppMetrica account are registered under the same login, verification is done automatically. If they are registered under different logins, in AppMetrica, go to **{{ settings }}** → **{{ manage-access }}** and grant access to the login from which you want to run campaigns.

## Frequently asked questions {#faq}

{% cut "Can I choose a media source other than Yandex Direct and still use a tracking URL in a Yandex Direct campaign?" %}

No. For correct transmission of install and event data, you must select Yandex Direct as the media source. If you absolutely need to choose a different media source, contact [support](../troubleshooting/feedback-new.md) to activate the media source first.

{% endcut %}

{% cut "Why does the install count in Yandex Direct differs from the one shown in AppMetrica reports?" %}

AppMetrica records installs based on their actual occurrence date, whereas Yandex Direct associates them with the date of the click.

For example, if a user clicked an ad on January 1 and installed the app on January 2, AppMetrica attributes the install to January 2, and Yandex Direct attributes it to January 1.

{% endcut %}

{% cut "Why does the number of clicks and impressions differ between Yandex Direct and AppMetrica?" %}

There are several reasons for this:

1. As an ad network, Yandex Direct has its own anti-fraud system that filters out suspicious clicks. AppMetrica records all clicks on tracking URLs except those in which the user agent passes the `IsBot` flag.

2. Yandex uses its own crawlers that, among other functions, check that links don't lead to phishing sites. If a crawler identifies our tracking URL and the `IsBot` parameter isn't passed in the impression or click, AppMetrica includes the event in its statistics. Yandex Direct, on the other hand, doesn't show such clicks and impressions.

{% endcut %}

## Learn more {#learn-more}

- [Ads for mobile apps](https://yandex.ru/support/direct/{{ locale }}/products-mobile-apps-ads/about)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*tracking URL]: A link formatted as `https://redirect.appmetrica.yandex.com/serve/*` that takes the user to the app store to install the app. If the app is already installed, it opens the app provided a deeplink is specified. Created when setting up the tracker. For more information, see [What is tracking?](index.md).
