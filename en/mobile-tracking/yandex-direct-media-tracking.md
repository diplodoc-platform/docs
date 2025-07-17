# AppMetrica in Yandex display advertising

Since December 2024, Yandex display ads support the AppMetrica pixel. It helps advertisers to track how users install their apps and what in-app actions they take after viewing an ad. Installing the pixel doesn't require any additional payment.

{% note warning "" %}

Currently, AppMetrica helps you track only those users who have installed the app after viewing or clicking an ad. Subsequently, you'll also see in-app events triggered by those users.

If a user already had the app installed on their device when they viewed or clicked on an ad, their in-app events won't be attributed to that ad and their statistics won't be reflected in reports for the associated ad campaign. However, attribution of existing users will be added in future updates.

{% endnote %}

To enable AppMetrica tracking, integrate the [AppMetrica SDK](../sdk/platforms.md) into your app and configure the settings as described below.

## Installing the pixel {#setup}

1. In the AppMetrica interface, go to **{{ tracking }}** and click **{{ create-tracker}}**.

    Leave **{{ pre-installing }}** and **{{ this-is-a-remarketing-campaign }}** disabled.

    Enter the name of the tracker.

2. Choose your app in the **{{ application }}** drop-down list.

3. Choose **Yandex.Direct** in the **{{ media-source }}** drop-down list.

    You can't select any other media source: the pixel only works with Yandex Direct. If you need to choose a different media source to optimize your Yandex Direct campaign, contact [support](../troubleshooting/feedback-new.md), making sure to attach your tracker ID.

4. Under **SmartLink**, add the platforms that you plan to advertise to the **{{ app-store }}** list.

    For each platform, add a link to your app's page in that store in the **{{ destination-url }}** field.

    Use **Fallback** to enter a destination URL for all other types of traffic. For example, you could send the user to a promo page if they clicked on the URL from a non-mobile device. If you select only **Fallback**, this will redirect all users to the specified destination URL.

5. Under **{{ attribution-settings }}**, set up attribution for each **{{ clicks-impressions }}** type. We recommend setting the maximum possible period: 10 days for clicks and 24 hours for impressions.

    Enable **{{ reattribution }}** if needed. With reattribution, you can account for installs made by those who previously installed your app but then deleted it. In this case, reinstallation counts as a new install and is attributed to the campaign.

    By default, one device can't have more than one attributed install within a 180-day period. If reattribution is disabled, new installs on a device that previously had attributed installs are registered as organic installs.

6. The **{{ postback-settings }}** section should be skipped: conversions for goals from your Yandex Direct Library are transmitted automatically.

7. Under **{{ tracking-url }}**, copy the tracking URL for clicks as well as the **Impression URL**: the latter is the AppMetrica pixel.

    {% note info "Impression URL" %}

    The impression URL must include the `&rnd=%aw_random%` parameter. If it's missing, make sure to add it yourself.

    {% endnote %}

9. Open your Yandex Direct account.

    Go to **Library** → **Add app**. In the **App from AppMetrica** field, specify the app you need. If you don't see this field, check your access rights.

    {% note warning "Access rights" %}

    If you're launching an ad campaign under a username different from the the one you registered with AppMetrica, grant access to AppMetrica for this username. Go to **{{ settings }}** → **{{ manage-access }}**. Select either the **Read/Edit** or **Read only** access level. Other access levels won't be sufficient.

    {% endnote %}

    Go to **Campaigns** and create an ad campaign. Paste the tracking URL from AppMetrica in the **Link in ad** field and the **Impression URL** from AppMetrica in the **Impression tag** field.

10. Launch the ad campaign. Now you have access to enhanced statistics in AppMetrica.

## Frequently asked questions {#faq}

{% cut "What's the difference between Yandex Metrica for Display Ads and AppMetrica?" %}

These are analytics tools designed for different objectives. Yandex Metrica for Display Ads helps with web traffic analytics, while AppMetrica handles mobile app analytics. In our case, they don't overlap in any way,

and we recommend using both pixels together.

{% endcut %}

{% cut "Can I use the AppMetrica pixel to set up Web+App integration?" %}

No. The AppMetrica pixel only works if the `device_id` (`GAID`/`OAID`/`IDFA`) is known at the time of impression. If the `device_id` can't be accessed, such integration is impossible.

{% endcut %}

## Learn more {#learn-more}

- [Display ads in Yandex Direct](https://yandex.ru/support/direct/{{ locale }}/branding)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
