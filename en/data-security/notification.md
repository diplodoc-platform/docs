# Notice about collecting statistics

You can notify your app users that statistics will be collected, and initialize the SDK with disabled statistics sending before getting consent. This section describes the steps to disable and enable statistics collection:

{% list tabs group=instructions %}

- Android

   To initialize a library with statistics sending option disabled, pass the value `false` into the `withStatisticsSending(boolean value)` method when creating an extended library configuration.

   ```java translate=no
   // Creating an extended library configuration.
   AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_key)
           // Disabling sending statistics.
           .withStatisticsSending(false)
           .build();
   // Initializing the AppMetrica SDK.
   AppMetrica.activate(getApplicationContext(), config);
   ```

   After the user has confirmed to send statistics (for example, in the application settings or in the agreement on the first start of the app), you should call the `AppMetrica.setStatisticsSending(Context context, boolean enabled` method to enable it:

   ```java translate=no
   // Checking the status of the boolean variable. It shows the user confirmation.
   if (flag) {
       // Enabling sending statistics.
       AppMetrica.setStatisticsSending(getApplicationContext(), true);
   }
   ```

- iOS (Objective-C)

   To initialize a library with statistics sending option disabled, set the value `NO` for the `statisticsSending` property of the `YMMYandexMetricaConfiguration` configuration.

   ```objectivec translate=no
   // Creating an extended library configuration.
   YMMYandexMetricaConfiguration *configuration = [[YMMYandexMetricaConfiguration alloc] initWithApiKey:@"API_key"];
   // Disabling sending statistics.
   configuration.statisticsSending = NO;
   // Initializing the AppMetrica SDK.
   [YMMYandexMetrica activateWithConfiguration:configuration];
   ```

   After the user has confirmed to send statistics (for example, in the application settings or in the agreement on the first start of the app), you should call the `+setStatisticsSending:` method of the `YMMYandexMetrica` class to enable it.

   ```objectivec translate=no
   // Checking the status of the boolean variable. It shows the user confirmation.
   if (flag) {
       // Enabling sending statistics.
       [YMMYandexMetrica setStatisticsSending:YES];
   }
   ```

- iOS (Swift)

   To initialize a library with statistics sending option disabled, set the value `NO` for the `statisticsSending` property of the `YMMYandexMetricaConfiguration` configuration.

   ```swift translate=no
   // Creating an extended library configuration.
   let configuration = YMMYandexMetricaConfiguration.init(apiKey: "API key")
   // Disabling sending statistics.
   configuration?.statisticsSending = false
   // Initializing the AppMetrica SDK.
   YMMYandexMetrica.activate(with: configuration!)
   ```

   After the user has confirmed to send statistics (for example, in the application settings or in the agreement on the first start of the app), you should call the `setStatisticsSending(_:)` method of the `YMMYandexMetrica` class to enable it.

   ```swift translate=no
   // Checking the status of the boolean variable. It shows the user confirmation.
   if flag {
       // Enabling sending statistics.
       YMMYandexMetrica.setStatisticsSending(true);
   }
   ```

{% endlist %}

## Alert example {#example-section}

You can use any text to inform users of statistics collection. For example:

> This app uses the AppMetrica analytical service (Yandex Metrica for apps) provided by YANDEX LLC, ulitsa Lva Tolstogo 16, Moscow, Russia 119021 (hereinafter referred to as Yandex) based on the [Terms of Use](https://yandex.com/legal/metrica_termsofuse/).
>
> AppMetrica analyzes app usage data, including the device it is running on, the installation source, calculates conversion, collects statistics of your activity for product analytics, ad campaign analysis, and optimization, as well as for troubleshooting. Information collected in this way cannot identify you.
>
> Depersonalized information about your use of this app collected by AppMetrica tools will be transferred to Yandex and stored on Yandex’s server in the EU and the Russian Federation. Yandex will process this information to assess how you use the app, compile reports for us on our app operation, and provide other services.

## See also

- [GDPR compliance](gdpr.md)
- [ISO/IEC 27001 compliance](iso-27001.md)
- [Masking the IP address](ip-masking.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
