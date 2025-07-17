# Web+App tracking

Web+App is a placement format that enables you to advertise your website and mobile application at the same time. With this format, the campaign is optimized based on both web and app data.

If a user already has the mobile app installed, a SmartLink directs them to the desired app section; if not, it takes them to the relevant section on the site.

To enable AppMetrica tracking, configure the settings as described below.

## Step 1. Preparing links {#links}

There are several ways to set up tracking:

{% list tabs %}

- AppMetrica tracking URLs

    - [Set up Universal Links on iOS](../sdk/ios/analytics/ios-universal-links.md)

    - [Deeplinks on Android](https://developer.android.com/training/app-links/deep-linking?hl=ru#adding-filters)

    {% note info "Setting up deeplinks in your app" %}

    Deeplinks are configured by the mobile app developer.

    Make sure that each product that you plan to promote has a deeplink schema that can open the relevant app page.

    {% endnote %}

- Universal Links

    Universal Links are formatted like regular links (`ya.ru`) but take the user to the relevant app section if they have the app installed. For example, the link `https://market.yandex.ru/special/kids_dep` opens the children's products section. However, if clicked on a mobile device with the Yandex Market app installed, the page opens in the mobile app instead.

    If the app isn't installed, you can check if Universal Links are correctly set up using an app-site association file. To do this, replace `example.ru` with your domain:

    - iOS: `https://www.example.ru/.well-known/apple-app-site-association`

    - Android: `https://www.example.ru/.well-known/assetlinks.json`

    This should open a page with text or download a text file. If this doesn't happen, this means that Universal Links aren't set up.

    For more information about setting up Universal Links, see the [Yandex Direct documentation](https://yandex.ru/support/direct/en/web-app/tracker-setting#url-settings). Documentation for [iOS](https://developer.apple.com/ios/universal-links/) | [Android](https://developer.android.com/training/app-links?hl=en#add-app-links) developers.

    {% note info "Landing page" %}

    Append the `referrer=reattribution%3D1` parameter to the landing page link in the ad.

    {% endnote %}

{% endlist %}

## Step 2. Setting up E-commerce events {#ecommerce-events}

To optimize campaigns for in-app purchases, implement transmission of events from your app code to AppMetrica. This task is typically handled by the app developer. For more information, see [Configuring the sending of E-commerce events](../data-collection/about-ecommerce.md).

Important events include:

- Product views.
- Add to cart events.
- Purchases.

All events must include the product ID and the revenue amount.

## Step 3. Linking Yandex Direct {#direct}

{% note warning "Access rights" %}

If you're launching an ad campaign under a username different from the the one you registered with AppMetrica, grant access to AppMetrica for this username. Go to **{{ settings }}** → **{{ manage-access }}**. Select either the **Read/Edit** or **Read only** access level. Other access levels won't be sufficient.

{% endnote %}

In your Yandex Direct account, go to **Library** → **Add app**. In the **App from AppMetrica** field, specify the desired app. If you don't see this field, check your access rights (see the note above).

Enter the desired goals under **Goals for the strategy**:

- `ECOMMERCE_SHOW_PRODUCT`
- `ECOMMERCE_ADD_TO_CART`
- `ECOMMERCE_PURCHASE`

For more information, see [Adding your app to the Yandex Direct library](https://yandex.ru/support/direct/{{ locale }}/web-app/add-aps).

## Stage 4. Setting up tracking URLs {#setup-tracker}

{% note info " " %}

If you opted for Universal Links in [Step 1](#links), you can skip this step.

{% endnote %}

1. Go to **{{ tracking }}** → **{{ create-tracker}}**.

    Enter the name of the tracker.

    Enable **{{ this-is-a-remarketing-campaign }}**.

2. Choose your app in the **{{ application }}** drop-down list.

3. Choose **Yandex.Direct** in the **{{ media-source }}** drop-down list.

    You can't select any other media source: the pixel only works with Yandex Direct.

3. Under **SmartLink**, complete the **Google Play**, **App Store (iOS)**, and **Fallback** (for non-Android and non-iOS apps; typically used for desktop) tabs.

    For each platform, in the **{{ destination-url }}** field, add a redirect link for users who don't have the mobile app installed. This is typically a website link.

    In the **Deeplink** field, specify the scheme for redirecting the user if they do have the mobile app installed.

    {% cut "How to set up deeplinks" %}

    Suppose you want to redirect the user to a specific product or service within an app or site. Instead of specifying the end URL, you can enter a macro (which can have any name).

    For example, for the **Google Play** destination URL, you can specify: `https://market.yandex.ru/{path}`. You can pass a value to the `path` parameter using a tracking URL that contains the desired value.

    Suppose your tracking URL is 
    
    ```
    https://123456789.redirect.appmetrica.yandex.com/special/split?appmetrica_tracking_id=98765432123456789
    ```

    When serving ads for children's products, you want to take the user to the "For children" section: `https://market.yandex.ru/special/kids_dep`.

    Append the `path` parameter value to your tracking URL:

    ```
    https://123456789.redirect.appmetrica.yandex.com/special/split?appmetrica_tracking_id=98765432123456789&path=special%2Fkids_dep
    ```

    When clicking the link from an Android device, the `path` parameter is set to `special%2Fkids_dep`. This value is then passed down the chain to the corresponding parameter in the destination URL `https://market.yandex.ru/{path}`, which becomes `https://market.yandex.ru/special/kids_dep`.

    If you specify `path=special%2Ffashion_dep`, the user will be taken to `https://market.yandex.ru/special/fashion_dep`.

    {% endcut %}

    Deeplink configuration:

    {% list tabs %}

    - Android

        Add the `click_id={click_id}` and `yclid={yclid}` parameters to the deeplink.

        Examples:

        `myapp://path?someutm=value&click_id={click_id}&yclid={yclid}`

        `myapp://path?click_id={click_id}&yclid={yclid}`

    - iOS

        If you specify the deeplink in the regular `myapp://somepath` format, the app-to-app tracking URL will look like this:

        `https://123456789.redirect.appmetrica.yandex.com/somepath?appmetrica_tracking_id=98765432123456789`

        When preparing the feed or completing the ad fields, replace `somepath` with an actual path supported on the app code side. You don't need to change anything in the deeplink itself.

    {% endlist %}

4. We recommend skipping the **{{ attribution-settings }}** section and keeping the default values there. Learn more about the [tracking technology](technology.md).

5. Leave the **{{ postback-settings }}** section empty. All events will be transmitted automatically once you add the necessary events to the [Yandex Direct Library](#direct) in Step 3.

## Frequently asked questions {#faq}

{% cut "Why am I seeing automatic trackers with the name "campaign number" after launching my ad campaigns?" %}

This is part of the integration mechanism. The tracker is only needed to set up the scenario to redirect the user to the desired page. Statistics are collected by [automatically generated trackers](auto-create-tracking.md#yandex-direct).

{% endcut %}

## Learn more {#learn-more}

- [Web+App scenario in Yandex Direct](https://yandex.ru/support/direct/{{ locale }}/web-app/about)

- [Ads for mobile apps in Yandex Direct](https://yandex.ru/support/direct/{{ locale }}/products-mobile-apps-ads/about)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
