# Импорт атрибуций на Android

Чтобы настроить импорт, вызовите метод получения атрибуции на клиенте, далее вызовите метод отправки атрибуции `AppMetrica.reportExternalAttribution` в SDK АppMetrica.

## AppsFlyer {#appsflyer}

1. [Зарегистрируйте](https://dev.appsflyer.com/hc/docs/conversion-data-android#appsflyerconversionlistener-overview/) `AppsflyerConversionListener`.
2. Настройте отправку атрибуции (метод `AppMetrica.reportExternalAttribution`) в AppMetrica SDK из `AppsflyerConversionListener`.

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

1. [Зарегистрируйте](https://dev.adjust.com/en/sdk/android/features/attribution/) `OnAttributionChangedListener`.
2. Настройте отправку атрибуции (метод `AppMetrica.reportExternalAttribution`) в AppMetrica SDK из `OnAttributionChangedListener`.

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

1. [Сделайте асинхронный запрос атрибуции вызовом](https://support.kochava.com/sdk-integration/android-sdk-integration/android-using-the-sdk/) `Tracker#retrieveInstallAttribution()`.
2. Настройте отправку атрибуции (метод `AppMetrica.reportExternalAttribution`) в AppMetrica SDK из `RetrievedInstallAttributionListener`.

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

1. Сделайте асинхронный запрос атрибуции вызовом `TenjinSDK#getAttributionInfo.`
2. Настройте отправку атрибуции (метод `AppMetrica.reportExternalAttribution`) в AppMetrica SDK из `AttributionInfoCallback`.

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
  );

  ```

{% endlist %}

## Airbridge {#airbridge}

1. [Зарегистрируйте](https://help.airbridge.io/en/developers/android-sdk#attribution-result-callback-setup) `OnAttributionResultReceiveListener`.
2. Настройте отправку атрибуции (метод `AppMetrica.reportExternalAttribution`) в AppMetrica SDK из `OnAttributionResultReceiveListener`.

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

1. Зарегистрируйте `SingularDeviceAttributionHandler`.
2. Настройте отправку атрибуции (метод `AppMetrica.reportExternalAttribution`) в AppMetrica SDK из `SingularDeviceAttributionHandler`.

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

{% if locale == "ru" %}

## Узнать больше {#learn-more}

- [Обзор на 360°: обогатите аналитику в AppMetrica данными из трекеров](https://appmetrica.yandex.ru/about/blog/appmetrica-analytics-with-mmp-insights)

{% endif %}

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
