# Importing attributions on Android

To set up import, call the attribution retrieval method on the client, then call the attribution sending method `AppMetrica.reportExternalAttribution` in the АppMetrica SDK.

## AppsFlyer {#appsflyer}

1. [Register](https://dev.appsflyer.com/hc/docs/conversion-data-android#appsflyerconversionlistener-overview/) `AppsflyerConversionListener`.
2. Set up the sending of attribution data (the `AppMetrica.reportExternalAttribution` method) in the AppMetrica SDK from `AppsflyerConversionListener`.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  val appsflyerConversionListener = object : AppsFlyerConversionListener {
	  // ...
      override fun onConversionDataSuccess(value: MutableMap<String, Any>?) {
          AppMetrica.reportExternalAttribution(ExternalAttributions.appsflyer(value))
      }
      // ...
  }

  AppsFlyerLib.getInstance().init(appsflyerKey, appsFlyerConversionListener, context)

  ```

- Java

  ```java translate=no
  AppsFlyerConversionListener appsFlyerConversionListener = new AppsFlyerConversionListener() {
	  // ...
      @Override
      public void onConversionDataSuccess(Map<String, Object> value) {
          AppMetrica.reportExternalAttribution(ExternalAttributions.appsflyer(value));
      }
      // ....
  };

  AppsFlyerLib.getInstance().init(appsflyerKey, appsFlyerConversionListener, context);

  ```

{% endlist %}

## Adjust {#adjust}

1. [Register](https://dev.adjust.com/en/sdk/android/features/attribution/) `OnAttributionChangedListener`.
2. Set up the sending of attribution data (the `AppMetrica.reportExternalAttribution` method) in the AppMetrica SDK from `OnAttributionChangedListener`.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  val config = AdjustConfig(context, adjustToken, adjustEnvironment)

  config.setOnAttributionChangedListener { attribution ->
      AppMetrica.reportExternalAttribution(ExternalAttributions.adjust(attribution))
  }

  Adjust.onCreate(config)

  ```

- Java

  ```java translate=no
  AdjustConfig config = new AdjustConfig(context, adjustToken, adjustEnvironment);

  config.setOnAttributionChangedListener(attribution -> {
      // ...
      AppMetrica.reportExternalAttribution(ExternalAttributions.adjust(attribution));
      // ...
  });

  Adjust.onCreate(config);

  ```

{% endlist %}

## Kochava {#kochava}

1. [Make an asynchronous attribution request by calling ](https://support.kochava.com/sdk-integration/android-sdk-integration/android-using-the-sdk/) `Tracker#retrieveInstallAttribution()`.
2. Set up the sending of attribution data (the `AppMetrica.reportExternalAttribution` method) in the AppMetrica SDK from `RetrievedInstallAttributionListener`.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  Tracker.getInstance().retrieveInstallAttribution { installAttribution ->
      AppMetrica.reportExternalAttribution(ExternalAttributions.kochava(installAttribution.toJson()))
  }
  ```

- Java

  ```java translate=no
  Tracker.getInstance().retrieveInstallAttribution(installAttribution ->        
      AppMetrica.reportExternalAttribution(ExternalAttributions.kochava(installAttribution.toJson()))
  );
  ```

{% endlist %}

## Tenjin {#tenjin}

1. Make an asynchronous attribution request by calling `TenjinSDK#getAttributionInfo`.
2. Set up the sending of attribution data (the `AppMetrica.reportExternalAttribution` method) in the AppMetrica SDK from `AttributionInfoCallback`.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  val tenjinSdk = TenjinSDK.getInstance(context, tenjinToken)
  tenjinSdk.connect()

  tenjinSdk.getAttributionInfo { attribution ->
      // ...
      AppMetrica.reportExternalAttribution(ExternalAttributions.tenjin(attribution))
      // ...
  }

  ```

- Java

  ```java translate=no
  TenjinSDK tenjinSDK = TenjinSDK.getInstance(context, tenjinToken);
  tenjinSDK.connect();

  tenjinSDK.getAttributionInfo(attribution ->
      // ...
      AppMetrica.reportExternalAttribution(ExternalAttributions.tenjin(attribution))
      // ...
  ).

  ```

{% endlist %}

## Airbridge {#airbridge}

1. [Register](https://help.airbridge.io/en/developers/android-sdk#attribution-result-callback-setup) `OnAttributionResultReceiveListener`.
2. Set up the sending of attribution data (the `AppMetrica.reportExternalAttribution` method) in the AppMetrica SDK from `OnAttributionResultReceiveListener`.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  val config = AirbridgeConfig.Builder(airbridgeAppName, airbridgeSdkAppToken)
      .setOnAttributionResultReceiveListener { map ->
        // ...
        AppMetrica.reportExternalAttribution(ExternalAttributions.airbridge(map))
        // ...
    }
    .build()

  Airbridge.init(context, config)

  ```

- Java

  ```java translate=no
  AirbridgeConfig config = new AirbridgeConfig.Builder(airbridgeAppName, airbridgeSdkAppToken)
      .setOnAttributionResultReceiveListener(map -> {
        // ...
        AppMetrica.reportExternalAttribution(ExternalAttributions.airbridge(map));
        // ...
    })
    .build();

  Airbridge.init(application, config);

  ```

{% endlist %}

## Singular {#singular}

1. Register `SingularDeviceAttributionHandler`.
2. Set up the sending of attribution data (the `AppMetrica.reportExternalAttribution` method) in the AppMetrica SDK from `SingularDeviceAttributionHandler`.

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  val config = SingularConfig(SINGULAR_SDK_KEY, SINGULAR_SDK_SECRET)
      .withSingularDeviceAttribution { map ->
        // ...
        AppMetrica.reportExternalAttribution(ExternalAttributions.singular(map))
        // ...
      }

  Singular.init(context, config)

  ```

- Java

  ```java translate=no
  SingularConfig singularConfig = new SingularConfig(SINGULAR_SDK_KEY, SINGULAR_SDK_SECRET)
      .withSingularDeviceAttribution(map -> {
          // ...
          AppMetrica.reportExternalAttribution(ExternalAttributions.singular(map));
          // ...
      });

  Singular.init(context, singularConfig);

  ```

{% endlist %}

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
