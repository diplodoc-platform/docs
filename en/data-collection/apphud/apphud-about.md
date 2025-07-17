# AppMetrica & Apphud

AppMetrica is integrated with [Apphud](https://docs.apphud.com/docs/what-is-apphud), one of the market leader solutions for in-app subscription and purchases tracking data. Apphud has 99.9% accuracy on app revenue tracking, which ensures that all possible purchase scenarios will be taken into account. 

Why is this important:

-  Save Development Resources: No complex integrations with third-party solutions. Easy connection of the Apphud module to AppMetrica can be set up in a [few steps](#enable-apphud).

- Data Accuracy: Precise subscription tracking data for every purchase scenario, tailored to the specific store or operating system. You always have the most up-to-date insights.

- Revenue Data Available in other reports: segment your audience by paying capacity and other purchase parameters, discover channels and geos that bring you the most paying users and much more in [In-app and Ad Revenue](../../mobile-reports/revenue-report.md), [Events](../../mobile-reports/events-report.md), [Audience](../../mobile-reports/audience-report.md) and [User Acquisition](../../mobile-reports/user-acquisition-report.md) reports. 

Features:

- App Store & iOS

   - Full refunds support, including updates with refund amount.
   - Family shared subscriptions support - transactions shared with other users via Family are not counted.
   - Correct count of App Store commissions.
   - Paid Introductory & Promotional Offers support.
   - Subscription Offer Codes Support.
   - Purchase Automatic recovery in SDK.

- Google Play & Android

   - Support of subscriptions with multiple base plans.
   - Complicated scenarios support, e.g. Free Trial + Paid Discount + Regular Price.
   - All offers types support: free trial, discount, fix price & absolute discount.

## How to enable Apphud {#enable-apphud}

Tracking via Apphud is a paid feature available with the Custom and Pro [plans](../../common/pricing/uae-currency.md#pro-upgrade). This option comes with a free `MTR limit of $10,000`.

{% note warning "" %}

1. Tracking via Apphud may be unavailable in some regions.
2. Apphud only works with Google Play and the App Store. It doesn't collect data from other app stores, such as Huawei AppGallery.

{% endnote %}

1. Activate Apphud under **{{ organization }}** → **{{ tariff }}**.

   - If you are on the Free plan, upgrade to the Custom or Pro plan and complete the required information. Once upgraded, the option and the free limit are activated automatically.
   - If you already have the Custom or Pro plan, the option and the free limit are activated automatically.

2. Update the AppMetrica SDK. AppMetrica supports tracking via Apphud starting from version [7.6.0 for Android](../../sdk/android/analytics/quick-start.md) and [5.9.0 for iOS](../../sdk/ios/analytics/quick-start.md).
3. Disable automatic collection of purchase and subscription data from Google Play or the App Store in the AppMetrica SDK.

   {% list tabs %}

   - Android

      {% list tabs %}

      - Kotlin

         ```kotlin translate=no
         val config = AppMetricaConfig.newConfigBuilder(API_KEY)
                      .withRevenueAutoTrackingEnabled(false)
                      .build()
                  AppMetrica.activate(context, config)
         ```

      - Java

         ```java translate=no
         AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_KEY)
                      .withRevenueAutoTrackingEnabled(false)
                      .build();
                  AppMetrica.activate(context, config);
         ```

      {% endlist %}

   - iOS

      {% list tabs %}

      - Swift

         ```swift translate=no
         let configuration = AppMetricaConfiguration(apiKey: "API_KEY")!
         configuration.revenueAutoTrackingEnabled = false
         AppMetrica.activate(with: configuration)
         ```

      - Objective-C

         ```obj-c translate=no
         AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithAPIKey:@"API_KEY"];
         configuration.revenueAutoTrackingEnabled = NO;
         [AMAAppMetrica activateWithConfiguration:configuration];
         ```

      {% endlist %}

   {% endlist %}

4. Disable manual collection of purchase data (if configured) from Google Play or the App Store.

   Try searching for `AppMetrica#reportRevenue(Revenue)` calls in your code and removing them. For instructions on how to enable manual collection, see the relevant sections for [Android](../../sdk/android/analytics/android-operations.md#send-revenue-key) and [iOS](../../sdk/ios/analytics/ios-operations.md#send-revenue-key).

5. If you're using the [POST API](../../mobile-api/post/about.md) to [send in-app revenue data](../../mobile-api/post/post-revenue.md) for Google Play and App Store purchases and subscriptions, disable this option.

   {% note info %}

   We recommend disabling all data collection (both manual and automatic) to prevent duplicate data in reports.

   {% endnote %}


6. Integrate the Apphud module into your app code.

   {% list tabs %}

   - Android

      The version of your Apphud module must match the version of your AppMetrica SDK.

      ```kotlin translate=no
      dependencies {
        // AppMetrica SDK
        implementation("io.appmetrica.analytics:{{ io-appmetrica-analytics-analytics }}")
        // AppMetrica SDK Apphud module
        // You should use the same versions for AppMetrica and Apphud modules
        implementation("io.appmetrica.analytics:analytics-apphud:{{ io-appmetrica-analytics-analytics }}")
      }
      ```

   - iOS

      {% list tabs %}

      - Cocoapods

         ```ruby translate=no
         pod 'AppMetricaApphudAdapter', '~> {{ apphud-adapter-ios }}'
         ```

      - SPM

         ```swift translate=no
         dependencies: [
             .package(
                 url: "https://github.com/appmetrica/appmetrica-sdk-apphud-adapter-ios",
                 from: "{{ apphud-adapter-ios }}"
             )
         ]
         ```

      {% endlist %}

   {% endlist %}

7. Enter your app details under **{{ settings }}** → **{{ tracking-apphud }}** in the AppMetrica interface.

   {% list tabs %}

   - Android app

      - Google Play package name.
      - JSON service account.

         To track subscription status updates, create and upload a service account JSON file to AppMetica. For information on how to create a JSON file, see the [Apphud documentation](https://docs.apphud.com/docs/google-play-service-credentials).

      - Real-time Google developer notifications.

         Once you upload the JSON file, a string will appear in the interface. Copy this string to **Google Play Console** → **Your App** → **Monetization Setup**. For more information, see the [Google documentation](https://developer.android.com/google/play/billing/getting-ready#configure-rtdn).

      - Google Play Reduced Service Fee.

         If you're registered for the [Google Play Reduced Service Fee](https://support.google.com/googleplay/android-developer/answer/11131145) program, specify your enrollment dates.

      ![](../../../_images/android-app-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 700px;"}

   - iOS app

      - Bundle ID.
      - App Store Apple ID.

         You can find it under **[App Store Connect](https://appstoreconnect.apple.com/)** → **Apps** → **App Information**.
      - App Store Shared Secret.

         {% cut "How to get an App Store Shared Secret" %}

         1. Open App Store Connect, go to [Apps](https://appstoreconnect.apple.com/apps), and select your app.
         2. Go to **Subscriptions** from the **Features** menu on the left.
         3. On the page, find the **App-Specific Shared Secret** section and click **Manage**.
         4. Create and copy a **Shared Secret**.
         5. In the AppMetrica interface, go to **{{ settings }}** → **{{ tracking-apphud }}** → **{{ iOS-app }}**.
         6. Insert the **Shared Secret** for the app in the **App Store Shared Secret** field.

         {% endcut %}

      - Apple Small Business Program.

         If you're registered for the [Apple Small Business Program](https://developer.apple.com/app-store/small-business-program), specify your enrollment dates.

      - App Store server notifications.

         - App Store Server API (StoreKit 2). In-app purchase key.
            A private key from App Store Connect that you need to upload to AppMetrica. For information on how to generate an in-app purchase key, see the [Apphud documentation](https://docs.apphud.com/docs/app-store-credentials).

      - URL for App Store Server Notifications V1 or V2.

         Once you upload the In-App Purchase Key, a string will appear in the interface. This is a URL for configuring App Store Server Notifications.

         {% cut "How to set up App Store server notifications" %}

         1. Copy the URL for App Store server notifications.
         2. Open App Store Connect, go to [Apps](https://appstoreconnect.apple.com/apps), and select your app.
         3. Go to **App Information** from the **General** menu on the left.
         4. At the bottom of the page that opens, find the **App Store Server Notifications** section and click **Edit** next to **Production Server URL**.
         5. In the **Production Server URL** field, enter the URL from AppMetrica.
         6. In the form below, select **Version 2 Notifications** and click **Save**.

         {% endcut %}

         ![](../../../_images/url-apple-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 700px;"}

      - Issuer ID.

         Issuer ID from App Store Connect. You can find it under **App Store Connect** → **Users and Access** → **Keys** → **App Store Connect API**.

      ![](../../../_images/ios-app-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 700px;"}

   {% endlist %}

## How to disable Apphud {#disable-apphud}

1. In the AppMetrica interface, go to **{{ organization }}** → **{{ tariff }}**.
2. In the box with your pricing plan, click **{{ settings-button }}**.
3. Find the **{{ apphud-inapp }}** option in the list and select **{{ disabled }}** next to it.

   ![](../../../_images/apphud-off-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 700px;"}

4. Click **{{ save }}**.
5. To disable the Apphud module, remove its dependencies from your app's code.

<!-- ## Личный кабинет в Apphud {#account-apphud}

ЖДЕМ APPHUD

через восстановление пароля -->

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}

