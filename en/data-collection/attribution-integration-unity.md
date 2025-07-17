# Importing attributions on Unity

To set up integration, call the attribution retrieval method on the client, then call the attribution sending method `AppMetrica.ReportExternalAttribution`.

## AppsFlyer {#appsflyer}

1. [Register](https://dev.appsflyer.com/hc/docs/conversion-data-unity) `IAppsFlyerConversionData` when initializing AppsFlyer.
2. Set up the sending of attribution data (the `AppMetrica.ReportExternalAttribution` method) in the AppMetrica SDK from `IAppsFlyerConversionData`.

{% list tabs group=instructions %}

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

1. [Register](https://dev.adjust.com/en/sdk/unity/v4/features/attribution/) `Action<AdjustAttribution>` using the `AdjustConfig.setAttributionChangedDelegate` method.
2. Set up the sending of attribution data (the `AppMetrica.ReportExternalAttribution` method) in the AppMetrica SDK from `Action<AdjustAttribution>`.

```csharp translate=no
var adjustConfig = new AdjustConfig("token", AdjustEnvironment.Production);
adjustConfig.setAttributionChangedDelegate(attribution => {
    AppMetrica.ReportExternalAttribution(ExternalAttributions.Adjust(attribution));
});
Adjust.start(adjustConfig);
```

## Kochava {#kochava}

1. Register `Action<KochavaTrackerInstallAttribution>` using the `KochavaTracker.GetInstallAttribution` method.
2. Set up the sending of attribution data (the `AppMetrica.ReportExternalAttribution` method) in the AppMetrica SDK from `Action<KochavaTrackerInstallAttribution>`.

```csharp translate=no
KochavaTracker.Instance.GetInstallAttribution(currentInstallAttribution => {
    AppMetrica.ReportExternalAttribution(ExternalAttributions.Kochava(currentInstallAttribution.Raw.ToString()));
});
```

## Tenjin {#tenjin}

1. Register `Tenjin.AttributionInfoDelegate` using the `BaseTenjin.GetAttributionInfo` method.
2. Set up the sending of attribution data (the `AppMetrica.ReportExternalAttribution` method) in the AppMetrica SDK from `Tenjin.AttributionInfoDelegate`.

```csharp translate=no
var tenjinSdk = Tenjin.getInstance("apiKey");
tenjinSdk.Connect();

tenjinSdk.GetAttributionInfo(attributionInfoData => {
    AppMetrica.ReportExternalAttribution(ExternalAttributions.Tenjin(attributionInfoData));
});
```

## Airbridge {#airbridge}

1. Register the `OnAttributionResultReceived` callback using the `AirbridgeUnity.SetOnAttributionReceived` method.
2. Set up the sending of attribution data (the `AppMetrica.ReportExternalAttribution` method) in the AppMetrica SDK from `OnAttributionResultReceived`.

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

1. Register `SingularDeviceAttributionCallbackHandler`.
2. Set up the sending of attribution data (the `AppMetrica.ReportExternalAttribution` method) in the AppMetrica SDK from `OnSingularDeviceAttributionCallback`.

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
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
