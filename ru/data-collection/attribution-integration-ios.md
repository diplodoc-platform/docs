# Импорт атрибуций на iOS

{% note info "" %}

Импорт атрибуций доступен с версии SDK AppMetrica iOS 5.2.0.

{% endnote %}

Чтобы настроить импорт, вызовите метод получения атрибуции на клиенте, далее вызовите метод отправки атрибуции `reportExternalAttribution` класса AppMetrica / AMAAppMetrica в SDK АppMetrica.

## AppsFlyer {#appsflyer}

Чтобы интегрировать AppsFlyer для атрибуции в свой проект, убедитесь, что для проектов SwiftUI добавлена поддержка AppDelegate.

1. [Инициализируйте](https://dev.appsflyer.com/hc/docs/integrate-ios-sdk) AppsFlyer обычным способом.
2. [Используйте метод](https://dev.appsflyer.com/hc/docs/conversion-data-ios) `onConversionDataSuccess` для получения атрибуции.
3. Настройте отправку атрибуции (метод `reportExternalAttribution`) в AppMetrica SDK.

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

Чтобы интегрировать Adjust для атрибуции в свой проект, убедитесь, что для проектов SwiftUI добавлена поддержка AppDelegate.

1. [Инициализируйте](https://dev.adjust.com/en/sdk/ios/) Adjust обычным способом.
2. Adjust использует объект [ADJAttribution](https://dev.adjust.com/en/sdk/ios/features/attribution) для обработки атрибуции. Преобразуйте его в `Dictionary` с помощью метода `dictionary()` и передайте в AppMetrica.
3. Настройте отправку атрибуции (метод `reportExternalAttribution`) в AppMetrica SDK.

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

Для Kochava используйте его метод поиска атрибуции в рамках обратного вызова, вызывая свойство `rawDictionary` для результата, полученного из метода `attribution.retrieveResult` синглтона.

1. [Инициализируйте](https://support.kochava.com/sdk-integration/ios-sdk-integration/ios-using-the-sdk/) Kochava обычным способом.
2. Kochava имеет свой механизм получения атрибуции через callback. Вызовите свойство `rawDictionary` в `result` из метода `attribution.retrieveResult`. Передайте полученный словарь в AppMetrica.
3. Настройте отправку атрибуции (метод `reportExternalAttribution`) в AppMetrica SDK.

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

1. [Инициализируйте](https://docs.tenjin.com/docs/ios-sdk) Tenjin обычным способом.
2. Получите экземпляр TenjinSDK с вашим ключом API, далее вызовите `getAttributionInfo(_:)`.
3. Настройте отправку атрибуции (метод `reportExternalAttribution`) в AppMetrica SDK.

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

1. [Инициализируйте](https://help.airbridge.io/en/developers/ios-sdk) Airbridge обычным способом.
2. [Задайте свойство](https://help.airbridge.io/en/developers/ios-sdk#attribution-result-callback-setup) `attributionCallback` для объекта `ABSetting`, полученного из `AirBridge.setting()`. В качестве параметра передайте словарь атрибуции.
3. Настройте отправку атрибуции (метод `reportExternalAttribution`) в AppMetrica SDK.

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

1. [Инициализируйте](https://support.singular.net/hc/en-us/articles/12054824479387-iOS-SDK-Integration-Guide) Singular обычным способом.
2. Инициализируйте `SingularConfig` с вашим ключом API и секретом.
3. Назначьте callback `deviceAttributionCallback` для обработки данных атрибуции.
4. Настройте отправку атрибуции (метод `reportExternalAttribution`) в AppMetrica SDK.

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

{% if locale == "ru" %}

## Узнать больше {#learn-more}

- [Обзор на 360°: обогатите аналитику в AppMetrica данными из трекеров](https://appmetrica.yandex.ru/about/blog/appmetrica-analytics-with-mmp-insights)

{% endif %}

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
