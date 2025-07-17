# Импорт атрибуций на React Native

### AppsFlyer

Настройте [отправку атрибуции](https://dev.appsflyer.com/hc/docs/rn_integration) в AppMetrica SDK.

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

Настройте [отправку атрибуции](https://dev.adjust.com/en/sdk/react-native/features/attribution/) в AppMetrica SDK.

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

Настройте [отправку атрибуции](https://support.kochava.com/sdk-integration/reactnative-sdk-integration/reactnative-using-the-sdk/) в AppMetrica SDK.

{% list tabs group=instructions %}

- JavaScript

  ```javascript translate=no
  KochavaTracker.instance.retrieveInstallAttribution().then((kochavaAttribution) => {
      ExternalAttributions.kochava(kochavaAttribution);
  });
  ```

{% endlist %}

### Tenjin {#tenjin}

Настройте [отправку атрибуции](https://www.npmjs.com/package/react-native-tenjin) в AppMetrica SDK.

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

Настройте [отправку атрибуции](https://help.airbridge.io/en/developers/react-native-sdk) в AppMetrica SDK.

{% list tabs group=instructions %}

- JavaScript

  ```javascript translate=no
  Airbridge.state.setAttributionListener((airbridgeAttribution) => {
      ExternalAttributions.airbridge(airbridgeAttribution);
  });
  ```

{% endlist %}

### Singular {#singular}

Настройте [отправку атрибуции](https://support.singular.net/hc/en-us/articles/360038415852-React-Native-SDK-Integration) в AppMetrica SDK.

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
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
