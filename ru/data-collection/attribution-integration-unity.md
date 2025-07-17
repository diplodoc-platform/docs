# Импорт атрибуций на Unity

Чтобы настроить интеграцию, вызовите метод получения атрибуции на клиенте, далее вызовите метод отправки атрибуции `AppMetrica.ReportExternalAttribution`.

## AppsFlyer {#appsflyer}

1. [Зарегистрируйте](https://dev.appsflyer.com/hc/docs/conversion-data-unity) `IAppsFlyerConversionData` при инициализации AppsFlyer.
2. Настройте отправку атрибуции (метод `AppMetrica.ReportExternalAttribution`) в AppMetrica SDK из `IAppsFlyerConversionData`.

{% list tabs %}

```csharp translate=no
public class AppsFlyerConversionDataListener : IAppsFlyerConversionData {
    public void onConversionDataSuccess(string conversionData) {
        AppMetrica.ReportExternalAttribution(ExternalAttributions.AppsFlyer(conversionData));
    }

    // ...
}

AppsFlyer.initSDK("devkey", "appId", new AppsFlyerConversionDataListener());
```

## Adjust {#adjust}

1. [Зарегистрируйте](https://dev.adjust.com/en/sdk/unity/v4/features/attribution/) `Action<AdjustAttribution>` с помощью метода `AdjustConfig.setAttributionChangedDelegate`.
2. Настройте отправку атрибуции (метод `AppMetrica.ReportExternalAttribution`) в AppMetrica SDK из `Action<AdjustAttribution>`.

```csharp translate=no
var adjustConfig = new AdjustConfig("token", AdjustEnvironment.Production);
adjustConfig.setAttributionChangedDelegate(attribution => {
    AppMetrica.ReportExternalAttribution(ExternalAttributions.Adjust(attribution));
});
Adjust.start(adjustConfig);
```

## Kochava {#kochava}

1. Зарегистрируйте `Action<KochavaTrackerInstallAttribution>` с помощью метода `KochavaTracker.GetInstallAttribution`.
2. Настройте отправку атрибуции (метод `AppMetrica.ReportExternalAttribution`) в AppMetrica SDK из `Action<KochavaTrackerInstallAttribution>`.

```csharp translate=no
KochavaTracker.Instance.GetInstallAttribution(currentInstallAttribution => {
    AppMetrica.ReportExternalAttribution(ExternalAttributions.Kochava(currentInstallAttribution.Raw.ToString()));
});
```

## Tenjin {#tenjin}

1. Зарегистрируйте `Tenjin.AttributionInfoDelegate` с помощью метода `BaseTenjin.GetAttributionInfo`.
2. Настройте отправку атрибуции (метод `AppMetrica.ReportExternalAttribution`) в AppMetrica SDK из `Tenjin.AttributionInfoDelegate`.

```csharp translate=no
var tenjinSdk = Tenjin.getInstance("apiKey");
tenjinSdk.Connect();

tenjinSdk.GetAttributionInfo(attributionInfoData => {
    AppMetrica.ReportExternalAttribution(ExternalAttributions.Tenjin(attributionInfoData));
});
```

## Airbridge {#airbridge}

1. Зарегистрируйте callback `OnAttributionResultReceived` с помощью метода `AirbridgeUnity.SetOnAttributionReceived`.
2. Настройте отправку атрибуции (метод `AppMetrica.ReportExternalAttribution`) в AppMetrica SDK из `OnAttributionResultReceived`.

```csharp translate=no
public class AirbridgeAttribution : MonoBehaviour {
    public void Init() {
        AirbridgeUnity.SetOnAttributionReceived(name);
    }

    public void OnAttributionResultReceived(string jsonString) {
        AppMetrica.ReportExternalAttribution(ExternalAttributions.Airbridge(jsonString));
    }
}
```

## Singular {#singular}

1. Зарегистрируйте `SingularDeviceAttributionCallbackHandler`.
2. Настройте отправку атрибуции (метод `AppMetrica.ReportExternalAttribution`) в AppMetrica SDK из `OnSingularDeviceAttributionCallback`.

```csharp translate=no
public class SingularDeviceAttributionHandler : SingularDeviceAttributionCallbackHandler {
    public void OnSingularDeviceAttributionCallback(Dictionary<string, object> attributionInfo) {
        AppMetrica.ReportExternalAttribution(ExternalAttributions.Singular(attributionInfo));
    }
}

SingularSDK.SetSingularDeviceAttributionCallbackHandler(new SingularDeviceAttributionHandler());
```

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
