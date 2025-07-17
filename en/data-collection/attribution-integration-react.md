# Importing attributions on React Native

### AppsFlyer

Set up the sending of [attribution data](https://dev.appsflyer.com/hc/docs/rn_integration) in the AppMetrica SDK.

{% list tabs group=instructions %}

- JavaScript

  ```javascript translate=no
  appsFlyer.initSdk(
      {
        devKey: '<YOUR_DEV_KEY>',
        onInstallConversionDataListener: true,
      }
  );

  appsFlyer.onInstallConversionData((appsFlyerAttribution) => {
    if (appsFlyerAttribution.type === 'onInstallConversionDataLoaded') {
      ExternalAttributions.appsflyer(appsFlyerAttribution);
    }
  });
    ```

{% endlist %}

### Adjust {#adjust}

Set up the sending of [attribution data](https://dev.adjust.com/en/sdk/react-native/features/attribution/) in the AppMetrica SDK.

{% list tabs group=instructions %}

- JavaScript

  ```javascript translate=no
  const adjustConfig = new AdjustConfig("<YOUR_APP_TOKEN>", 'production');
  adjustConfig.setAttributionCallback((adjustAttribution) => {   
    ExternalAttributions.adjust(adjustAttribution);
  });
  Adjust.initSdk(adjustConfig);
  ```

{% endlist %}

### Kochava {#kochava}

Set up the sending of [attribution data](https://support.kochava.com/sdk-integration/reactnative-sdk-integration/reactnative-using-the-sdk/) in the AppMetrica SDK.

{% list tabs group=instructions %}

- JavaScript

  ```javascript translate=no
  KochavaTracker.instance.retrieveInstallAttribution().then((kochavaAttribution) => {
      ExternalAttributions.kochava(kochavaAttribution);
  });
  ```

{% endlist %}

### Tenjin {#tenjin}

Set up the sending of [attribution data](https://www.npmjs.com/package/react-native-tenjin) in the AppMetrica SDK.

{% list tabs group=instructions %}

- JavaScript

  ```javascript translate=no
  Tenjin.getAttributionInfo(
      (tenjinAttribution) => {
          ExternalAttributions.tenjin(tenjinAttribution);
      },
      () => {
          console.error('Attribution info failed');
      }
  );
  ```

{% endlist %}

### Airbridge {#airbridge}

Set up the sending of [attribution data](https://help.airbridge.io/en/developers/react-native-sdk) in the AppMetrica SDK.

{% list tabs group=instructions %}

- JavaScript

  ```javascript translate=no
  Airbridge.state.setAttributionListener((airbridgeAttribution) => {
      ExternalAttributions.airbridge(airbridgeAttribution);
  });
  ```

{% endlist %}

### Singular {#singular}

Set up the sending of [attribution data](https://support.singular.net/hc/en-us/articles/360038415852-React-Native-SDK-Integration) in the AppMetrica SDK.

{% list tabs group=instructions %}

- JavaScript

  ```javascript translate=no
  const singularConfig = new SingularConfig(
    '<YOUR_API_KEY>',
    '<YOUR_SECRET_KEY>',
  );
  singularConfig.withDeviceAttributionCallbackHandler(singularAttribution => {
      ExternalAttributions.singular(singularAttribution);
  });
  ```

{% endlist %}

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
