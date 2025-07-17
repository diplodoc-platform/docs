# Importing attributions on iOS

{% note info "" %}

Attribution import is available starting with AppMetrica SDK 5.2.0 for iOS.

{% endnote %}

To set up import, call the attribution retrieval method on the client, then call the attribution sending method `reportExternalAttribution` of the AppMetrica / AMAAppMetrica class in the АppMetrica SDK.

## AppsFlyer {#appsflyer}

To integrate AppsFlyer for attribution into your project, make sure you added support for AppDelegate to SwiftUI projects.

1. [Initialize](https://dev.appsflyer.com/hc/docs/integrate-ios-sdk) AppsFlyer in a regular way.
2. [Use the method](https://dev.appsflyer.com/hc/docs/conversion-data-ios) `onConversionDataSuccess` for attribution retrieval.
3. Set up the sending of attribution data (the `reportExternalAttribution` method) in the AppMetrica SDK.

{% list tabs group=instructions %}

- Swift

  ```swift translate=no
  import AppMetricaCore
  import AppsFlyerLib

  extension AppDelegate: AppsFlyerLibDelegate {
      func onConversionDataSuccess(_ installData: [AnyHashable: Any]) {
          AppMetrica.reportExternalAttribution(installData, from: .appsflyer)
      }
  }
  ```

- Objective-C

  ```objc translate=no
  #import <AppMetricaCore/AppMetricaCore.h>
  #import <AppsFlyerLib/AppsFlyerLib.h>

  @interface AppDelegate ()
  @end

  @implementation AppDelegate

  - (void)onConversionDataSuccess:(NSDictionary *)installData {
      [AMAAppMetrica reportExternalAttribution:installData
                                        source:kAMAAttributionSourceAppsflyer
                                     onFailure:nil];
  }

  @end
  ```

{% endlist %}

## Adjust {#adjust}

To integrate Adjust for attribution into your project, make sure you added support for AppDelegate to SwiftUI projects.

1. [Initialize](https://dev.adjust.com/en/sdk/ios/) Adjust in a regular way.
2. Adjust uses the [ADJAttribution](https://dev.adjust.com/en/sdk/ios/features/attribution) object for attribution data processing. Convert it to `Dictionary` with the `dictionary()` method and pass it to AppMetrica.
3. Set up the sending of attribution data (the `reportExternalAttribution` method) in the AppMetrica SDK.

{% list tabs group=instructions %}

- Swift

  ```swift translate=no
  import AppMetricaCore
  import Adjust

  extension AppDelegate: AdjustDelegate {
      func adjustAttributionChanged(_ attribution: ADJAttribution?) {
          if let attribution = attribution?.dictionary() {
              AppMetrica.reportExternalAttribution(attribution, from: .adjust)
          }
      }
  }
  ```

- Objective-C

  ```objc translate=no
  #import <AppMetricaCore/AppMetricaCore.h>
  #import <Adjust/Adjust.h>

  @interface AppDelegate () <AdjustDelegate>
  @end

  @implementation AppDelegate

  - (void)adjustAttributionChanged:(ADJAttribution *)attribution {
      NSDictionary *attributionDictionary = [attribution dictionary];
      if (attributionDictionary != nil) {
          [AMAAppMetrica reportExternalAttribution:attributionDictionary
                                            source:kAMAAttributionSourceAdjust
                                         onFailure:nil];
      }
  }

  @end
  ```

{% endlist %}

## Kochava {#kochava}

For Kochava, use its attribution search method within a callback by calling the `rawDictionary` property on the result retrieved from the singleton's `attribution.retrieveResult` method.

1. [Initialize](https://support.kochava.com/sdk-integration/ios-sdk-integration/ios-using-the-sdk/) Kochava in a regular way.
2. Kochava features its own attribution retrieval mechanism via a callback. Call the `rawDictionary` property in the `result` from the `attribution.retrieveResult` method. Send the resulting dictionary to AppMetrica.
3. Set up the sending of attribution data (the `reportExternalAttribution` method) in the AppMetrica SDK.

{% list tabs group=instructions %}

- Swift

  ```swift translate=no
  import AppMetricaCore
  import KochavaNetworking
  import KochavaMeasurement
  ```

  ```swift translate=no
  Measurement.shared.attribution.retrieveResult { result in
      if let attribution = result.rawDictionary {
          AppMetrica.reportExternalAttribution(attribution, from: .kochava)
      }
  }

  ```

- Objective-C

  ```objc translate=no
  #import <AppMetricaCore/AppMetricaCore.h>
  @import KochavaNetworking;
  @import KochavaMeasurement;
  ```

  ```objc translate=no
  [KVAMeasurement.shared.attribution retrieveResultWithClosureDidComplete:^(KVAMeasurement_Attribution_Result * _Nonnull result) {
      NSDictionary *attributionDictionary = result.rawDictionary;
      if (attributionDictionary) {
          [AMAAppMetrica reportExternalAttribution:attributionDictionary
                                            source:kAMAAttributionSourceKochava
                                         onFailure:nil];
      }
  }];
  ```

{% endlist %}

## Tenjin {#tenjin}

1. [Initialize](https://docs.tenjin.com/docs/ios-sdk) Tenjin in a regular way.
2. Get a TenjinSDK instance with your API key and then call `getAttributionInfo(_:)`.
3. Set up the sending of attribution data (the `reportExternalAttribution` method) in the AppMetrica SDK.

{% list tabs group=instructions %}

- Swift

  ```swift translate=no
  import AppMetricaCore
  import TenjinSDK
  ```

  ```swift translate=no
  TenjinSDK.getInstance("<SDK_KEY>").getAttributionInfo { (attribution: [AnyHashable : Any]?, error: Error?) in
      if let attribution = attribution {
          AppMetrica.reportExternalAttribution(attribution, from: .tenjin)
      }
  }
  ```

- Objective-C

  ```objc translate=no
  #import <AppMetricaCore/AppMetricaCore.h>
  #import <TenjinSDK/TenjinSDK.h>
  ```

  ```objc translate=no
  [[TenjinSDK getInstance:@"<SDK_KEY>"] getAttributionInfo:^(NSDictionary *attribution, NSError *error) {
      if (attribution) {
          [AMAAppMetrica reportExternalAttribution:attribution
                                            source:kAMAAttributionSourceTenjin
                                         onFailure:nil];
      }
  }];
  ```

{% endlist %}

## Airbridge {#airbridge}

1. [Initialize](https://help.airbridge.io/en/developers/ios-sdk) Airbridge in a regular way.
2. [Set](https://help.airbridge.io/en/developers/ios-sdk#attribution-result-callback-setup) the `attributionCallback` property for the `ABSetting` object retrieved from `AirBridge.setting()`. Pass the attribution dictionary as a parameter.
3. Set up the sending of attribution data (the `reportExternalAttribution` method) in the AppMetrica SDK.

{% list tabs group=instructions %}

- Swift

  ```swift translate=no
  import AppMetricaCore
  import AirBridge
  ```

  ```swift translate=no
  AirBridge.setting().attributionCallback = { (attribution: [String : String]) in
      AppMetrica.reportExternalAttribution(attribution, from: .airbridge)
  }
  ```

- Objective-C

  ```objc translate=no
  #import <AppMetricaCore/AppMetricaCore.h>
  #import <AirBridge/AirBridge.h>
  ```

  ```objc translate=no
  [AirBridge.setting setAttributionCallback:^(NSDictionary<NSString *,NSString *> * _Nonnull attribution) {
      [AMAAppMetrica reportExternalAttribution:attribution
                                        source:kAMAAttributionSourceAirbridge
                                     onFailure:nil];
  }];
  ```

{% endlist %}

## Singular {#singular}

1. [Initialize](https://support.singular.net/hc/en-us/articles/12054824479387-iOS-SDK-Integration-Guide) Singular in a regular way.
2. Initialize `SingularConfig` with your API key and secret.
3. Assign a callback named `deviceAttributionCallback` for attribution data processing.
4. Set up the sending of attribution data (the `reportExternalAttribution` method) in the AppMetrica SDK.

{% list tabs group=instructions %}

- Swift

  ```swift translate=no
  import AppMetricaCore
  import Singular
  ```

  ```swift translate=no
  if let singularConfig = SingularConfig(apiKey: "API_KEY", andSecret: "SECRET") {
      singularConfig.deviceAttributionCallback = { (attribution: [AnyHashable : Any]?) in
          if let attribution = attribution {
              AppMetrica.reportExternalAttribution(attribution, from: .singular)
          }
      }
  }
  ```

- Objective-C

  ```objc translate=no
  #import <AppMetricaCore/AppMetricaCore.h>
  #import <Singular/Singular.h>
  ```

  ```objc translate=no
  SingularConfig *singularConfig = [[SingularConfig alloc] initWithApiKey:@"API_KEY" andSecret:@"SECRET"];
  singularConfig.deviceAttributionCallback = ^(NSDictionary *attribution) {
      if (attribution) {
          [AMAAppMetrica reportExternalAttribution:attribution
                                            source:kAMAAttributionSourceSingular
                                         onFailure:nil];
      }
  };
  ```

{% endlist %}

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
