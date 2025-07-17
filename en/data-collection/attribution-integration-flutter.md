# Importing attributions on Flutter

To set up integration, call the attribution retrieval method on the client, then call the attribution sending method `AppMetrica.ReportExternalAttribution`.

## AppsFlyer {#appsflyer}

Set up the sending of attribution data in the AppMetrica SDK for [AppsFlyer](https://pub.dev/packages/appsflyer_sdk):

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

Set up the sending of attribution data in the AppMetrica SDK for [Adjust](https://pub.dev/packages/adjust_sdk):

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

For more information about attribution tracking methods, see the [Adjust documentation](https://dev.adjust.com/en/sdk/flutter/).

## Kochava {#kochava}

Set up the sending of attribution data in the AppMetrica SDK for [Kochava](https://pub.dev/packages/kochava_tracker):

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

For more information about attribution tracking methods, see the [Kochava documentation](https://support.kochava.com/sdk-integration/flutter-sdk-integration/).

## Tenjin {#tenjin}

Set up the sending of attribution data in the AppMetrica SDK for [Tenjin](https://pub.dev/packages/tenjin_plugin):

{% list tabs group=instructions %}

- Dart

  ```dart translate=no
  TenjinSDK.instance.getAttributionInfo().then((tenjinAttribution) =>
    AppMetrica.reportExternalAttribution(AppMetricaExternalAttribution.tenjin(tenjinAttribution))
  );
  ```

{% endlist %}

## Airbridge {#airbridge}

Set up the sending of attribution data in the AppMetrica SDK for [Airbridge](https://pub.dev/packages/airbridge_flutter_sdk):

{% list tabs group=instructions %}

- Dart

  ```dart translate=no
  Airbridge.attribution.setAttributionListener((airbridgeAttribution) {
    AppMetrica.reportExternalAttribution(AppMetricaExternalAttribution.airbridge(airbridgeAttribution));
  });
  ```

{% endlist %}

For more information about attribution tracking methods, see the [Airbridge documentation](https://help.airbridge.io/en/developers/flutter-sdk).

## Singular {#singular}

Set up the sending of attribution data in the AppMetrica SDK for [Singular](https://pub.dev/packages/singular_flutter_sdk):

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

For more information about attribution tracking methods, see the [Singular documentation](https://support.singular.net/hc/en-us/articles/4408894547227-Singular-SDK-Integration-for-Flutter).

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
