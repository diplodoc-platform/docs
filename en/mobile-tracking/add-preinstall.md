# Creating a tracker for pre-installs

Pre-installs are apps installed on a device without direct user involvement. AppMetrica supports a number of methods to track pre-installed apps.

## Creating a tracker for apps pre-installed by the device manufacturer {#apk}

{% note alert %}

To get accurate statistics on pre-installed app activations, do not use the tracking URL from the created tracker. Create a separate tracker for each media source.

{% endnote %}

### Step 1. Creating a tracker in the AppMetrica interface {#apk-web}

1. In the AppMetrica interface, go to **Tracking** → **Create tracker**.

2. Under **Campaign details**, fill in the following fields:

   - **Pre-installing**: Enable this option to track pre-installs.
   - **PAI**: Keep this option disabled. Learn more about [creating a tracker for PAI pre-installs](#pai).
   - **Tracker name**: A name for the tracker. After being created, the tracker is available in the list with the specified name.
   - **Application**: Select the app you want to track.
   - **Media Source**: The media source to attribute clicks, installs, and conversions to.
      If the media source isn't in the list, you can [add](add-partner.md) it. After being added, the new source will be saved in the list.

### Step 2. Obtaining tracking_ID {#tracking-id}

1. [Find the created tracker in the list](https://appmetrika.yandex.{{ domain }}/campaign/list) and open it. Use the ID you see on the page as tracking_ID when [setting up the AppMetrica SDK](#apk-sdk-setting).

![](../../_images/tracking-id-{{ locale }}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

### Step 3. Configuring the AppMetrica SDK {#apk-sdk-setting}

{% list tabs %}

- Android

   Tracking pre-installed apps is available when using the [extended configuration of the AppMetrica library](../sdk/android/analytics/android-operations.md). To set parameters for tracking pre-installed apps, follow these steps:

   1. Create an object with the necessary tracking parameters:

      ```java translate=no
      public class MyApp extends Application {
            @Override
            public void onCreate() {
                super.onCreate();
                // Creating an instance of a constructor for app pre-installation information.
                PreloadInfo.Builder preloadInfoBuilder = PreloadInfo.newBuilder(tracking_ID);
                // Creating an instance of information about app pre-installation.
                PreloadInfo preloadInfo = preloadInfoBuilder.build();
      ```

   2. Create the extended configuration of the AppMetrica library and enter parameters for tracking pre-installed apps. Then perform library initialization in the app, using the extended configuration.

      ```java translate=no
      public class MyApp extends Application {
            @Override
            public void onCreate() {
                super.onCreate();
                // Creating an extended library configuration.
                AppMetricaConfig.Builder configBuilder = AppMetricaConfig.newConfigBuilder(API_key);
                // Setting necessary parameters (for example, enabling logging).
                configBuilder.setLogEnabled();
                // ...
                // Setting tracking parameters for pre-installed apps.
                configBuilder.setPreloadInfo(preloadInfo);
                // Creating an extended configuration instance.
                AppMetricaConfig extendedConfig = configBuilder.build();
                // Initializing the AppMetrica SDK.
                AppMetrica.activate(getApplicationContext(), extendedConfig);
            }
      }
      ```

      Initialize the AppMetrica SDK this way for all the app processes.

   3. Use the method of the `AppMetrica` class to enable tracking user activity:

      ```java translate=no
      ...
      AppMetrica.enableActivityAutoTracking(this);
      ```

- iOS

   Tracking pre-installed apps is available when using the [extended configuration of the AppMetrica library](../sdk/ios/analytics/ios-operations.md). To set information for tracking pre-installed apps, follow these steps:

   - Objective-C

      1. Create an object with the necessary tracking parameters:

         ```objectivec translate=no
         AMAAppMetricaPreloadInfo *preloadInfo = [[AMAAppMetricaPreloadInfo alloc] initWithTrackingIdentifier:@"tracking_ID"];
         ```

      2. Create the extended configuration of the AppMetrica library and set information in it for tracking pre-installed apps. Then perform library initialization in the app, using the extended configuration.

         ```objectivec translate=no
         // Creating an extended library configuration.
         AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithApiKey:@"API_key"];
         // Setting up the configuration.
         configuration.preloadInfo = preloadInfo;
         // ...
         // Initializing the AppMetrica SDK.
         [AMAAppMetrica activateWithConfiguration:configuration];

         ```

   - Swift

      1. Create an object with the necessary tracking parameters:

         ```swift translate=no
         let preloadInfo = AppMetricaPreloadInfo.init(trackingIdentifier: "tracking_ID")
         ```

      2. Create the extended configuration of the AppMetrica library and set information in it for tracking pre-installed apps. Then perform library initialization in the app, using the extended configuration.

         ```swift translate=no
         // Creating an extended library configuration.
         let configuration = AppMetricaConfiguration.init(apiKey: "API key")
         // Setting up the configuration
         configuration?.preloadInfo = preloadInfo
         // ...
         // Initializing the AppMetrica SDK.
         AppMetrica.activate(with: configuration!)
         ```

{% endlist %}

| Parameter | Description |
| -------- | -------- |
| `API_key` | A unique app ID issued in the AppMetrica web interface at [app registration](https://appmetrica.yandex.{{ domain }}/application/new). |
| `tracking_ID` | A numeric tracker ID that is shown in the AppMetrica interface when creating a tracker. |

## Creating a tracker for PAI pre-installs {#pai}

1. In the AppMetrica interface, go to **Tracking** → **Create tracker**.

2. Under **Campaign details**, fill in the following fields:

   - **Pre-installing**: Enable this option to track pre-installs.
   - **PAI**: Enable this option if you are creating a tracker for PAI pre-installs. Learn more about [PAI pre-installs](preinstalled-app-attr.md#pai).
   - **Tracker name**: A name for the tracker. After being created, the tracker is available in the list with the specified name.
   - **Application**: Select the app you want to track.
   - **Media Source**: The media source to attribute clicks, installs, and conversions to.
      If the media source isn't in the list, you can [add](add-partner.md) it. After being added, the new source will be saved in the list.

3. In the section below, fill in the **utm_campaign** field. This parameter is used to count pre-installs of the PAI type. Enter the value obtained from the manufacturer or generate a parameter value and pass it to the manufacturer.

## See also

- [Tracking pre-installed apps](preinstalled-app-attr.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
