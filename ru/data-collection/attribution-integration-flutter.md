# Импорт атрибуций на Flutter

Чтобы настроить интеграцию, вызовите метод получения атрибуции на клиенте, далее вызовите метод отправки атрибуции `AppMetrica.reportExternalAttribution`.

## AppsFlyer {#appsflyer}

Настройте отправку атрибуции в AppMetrica SDK для [AppsFlyer](https://pub.dev/packages/appsflyer_sdk):

{% list tabs group=instructions %}

- Dart

  ```dart translate=no
  AppsFlyerOptions appsFlyerOptions = AppsFlyerOptions(
    afDevKey: "afDevKey",
  );
  AppsflyerSdk appsflyerSdk = AppsflyerSdk(appsFlyerOptions);
  appsflyerSdk.onInstallConversionData((appsFlyerAttribution){
    AppMetrica.reportExternalAttribution(AppMetricaExternalAttribution.appsflyer(appsFlyerAttribution));
  });
  appsflyerSdk.initSdk(
    registerConversionDataCallback: true
  );
  ```

{% endlist %}

## Adjust {#adjust}

Настройте отправку атрибуции в AppMetrica SDK для [Adjust](https://pub.dev/packages/adjust_sdk):

{% list tabs group=instructions %}

- Dart

  ```dart translate=no
  AdjustConfig adjustConfig = AdjustConfig("", AdjustEnvironment.sandbox);
  adjustConfig.attributionCallback = (AdjustAttribution adjustAttribution) {
    AppMetrica.reportExternalAttribution(AppMetricaExternalAttribution.adjust(adjustAttribution));
  };
  Adjust.start(adjustConfig);
  ```

{% endlist %}

Подробнее о методах отслеживания атрибуции в [документации Adjust](https://dev.adjust.com/en/sdk/flutter/).

## Kochava {#kochava}

Настройте отправку атрибуции в AppMetrica SDK для [Kochava](https://pub.dev/packages/kochava_tracker):

{% list tabs group=instructions %}

- Dart

  ```dart translate=no
  KochavaTracker.instance.registerAndroidAppGuid("");
  KochavaTracker.instance.retrieveInstallAttribution().then((kochavaAttribution) =>
    AppMetrica.reportExternalAttribution(AppMetricaExternalAttribution.kochava(kochavaAttribution))
  );
  KochavaTracker.instance.start();
  ```

{% endlist %}

Подробнее о методах отслеживания атрибуции в [документации Kochava](https://support.kochava.com/sdk-integration/flutter-sdk-integration/).

## Tenjin {#tenjin}

Настройте отправку атрибуции в AppMetrica SDK для [Tenjin](https://pub.dev/packages/tenjin_plugin):

{% list tabs group=instructions %}

- Dart

  ```dart translate=no
  TenjinSDK.instance.getAttributionInfo().then((tenjinAttribution) =>
    AppMetrica.reportExternalAttribution(AppMetricaExternalAttribution.tenjin(tenjinAttribution))
  );
  ```

{% endlist %}

## Airbridge {#airbridge}

Настройте отправку атрибуции в AppMetrica SDK для [Airbridge](https://pub.dev/packages/airbridge_flutter_sdk):

{% list tabs group=instructions %}

- Dart

  ```dart translate=no
  Airbridge.attribution.setAttributionListener((airbridgeAttribution) {
    AppMetrica.reportExternalAttribution(AppMetricaExternalAttribution.airbridge(airbridgeAttribution));
  });
  ```

{% endlist %}

Подробнее о методах отслеживания атрибуции в [документации Airbridge](https://help.airbridge.io/en/developers/flutter-sdk).

## Singular {#singular}

Настройте отправку атрибуции в AppMetrica SDK для [Singular](https://pub.dev/packages/singular_flutter_sdk):

{% list tabs group=instructions %}

- Dart

  ```dart translate=no
  SingularConfig singularConfig = SingularConfig("", "");
  singularConfig.deviceAttributionCallback = (Map<String, dynamic> singularAttribution) {
    AppMetrica.reportExternalAttribution(AppMetricaExternalAttribution.singular(singularAttribution));
  };
  Singular.start(singularConfig);
  ```

{% endlist %}

Подробнее о методах отслеживания атрибуции в [документации Singular](https://support.singular.net/hc/en-us/articles/4408894547227-Singular-SDK-Integration-for-Flutter).

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
