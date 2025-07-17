# Installation and initialization

AppMetrica Push Unity is a plugin for the [Unity3d](http://docs.unity3d.com/) game platform that includes support for the AppMetrica Push SDK for the Android and iOS platforms.

This section describes the steps to enable and initialize the AppMetrica Unity Plugin:

## Step 1. Enable the AppMetrica Unity plugin {#integration-appmetrica}

To enable the AppMetrica Unity plugin, follow the [instructions](../analytics/quick-start.md).

{% note info %}

You must use the AppMetrica Unity plugin version 6.1.0 or higher.

{% endnote %}

## Stage 2. Enable the AppMetrica Push Unity plugin {#integration}

The plugin is enabled via the [Unity Package Manager](https://docs.unity3d.com/Manual/Packages.html).

Add the following dependencies to [Packages/manifest.json](https://docs.unity3d.com/Manual/upm-manifestPrj.html):

```json translate=no
{
  "dependencies": {
    "io.appmetrica.analytics.push": "https://github.com/appmetrica/push-unity-plugin.git#v{{ appmetrica-push-unity-plugin }}"
  }
}
```

## Step 3. Initialize the library {#activate}

You should activate AppMetrica Push using the [RuntimeInitializeOnLoadMethodAttribute](https://docs.unity3d.com/ScriptReference/RuntimeInitializeOnLoadMethodAttribute.html) attribute.

Create a static method with the `[RuntimeInitializeOnLoadMethod(RuntimeInitializeLoadType.BeforeSceneLoad)]` attribute and activate AppMetricaPush using the `AppMetricaPush.Activate()` method.

> Example:
>
> ```csharp translate=no
> using Io.AppMetrica;
> using Io.AppMetrica.Push;
> using UnityEngine;
>
> public static class AppMetricaActivator {
>     [RuntimeInitializeOnLoadMethod(RuntimeInitializeLoadType.BeforeSceneLoad)]
>     private static void Activate() {
>         AppMetrica.Activate(new AppMetricaConfig("APIKey"));
>         AppMetricaPush.Activate();
>     }
> }
> ```

{% note info %}

You must call `AppMetricaPush.Activate()` strictly after `AppMetrica.Activate()`.

{% endnote %}

## Stage 4. Add settings for each native platform {#platforms}

{% list tabs %}

- Android

  1. [Set up](../../android/push/android-settings.md#firebase) the app for using Firebase. [Get and add to AppMetrica](../../android/push/android-settings.md#firebase-key) a server key for using Firebase Cloud Messaging.
  2. To configure AndroidManifest.xml, make changes to the `application` element in `AndroidManifest.xml`:

     ```xml translate=no
     <meta-data android:name="ymp_firebase_default_app_id" android:value="APP_ID"/>
     <meta-data android:name="ymp_gcm_default_sender_id" android:value="number:SENDER_ID"/>
     <meta-data android:name="ymp_firebase_default_api_key" android:value="API_KEY"/>
     <meta-data android:name="ymp_firebase_default_project_id" android:value="PROJECT_ID"/>
     ```

     {{ app-id }}

     {{ sender-id }}

     {{ api-key-push }}

     {{ project-id }}

- iOS

  1. Add the SSL certificate to AppMetrica according to the [instructions](../../ios/push/ios-settings.md).
  2. To receive push notifications, ask the user for permission. We recommend using the [Mobile Notifications](https://docs.unity3d.com/Packages/com.unity.mobile.notifications@2.0/manual/index.html) Unity package and request permission according to the [instructions](https://docs.unity3d.com/Packages/com.unity.mobile.notifications@2.0/manual/iOS.html#authorization-request).

  {% note info %}

  The AppMetrica Push Unity plugin uses <q>swizzling</q>: it intercepts the execution of certain methods of the `UnityAppController` class by using the ObjectiveC runtime. You can find the source code of the swizzling mechanism in the [AMPUAppMetricaPushAppController.m](https://github.com/appmetrica/push-unity-plugin/blob/main/Runtime/Plugins/iOS/AMPUAppMetricaPushAppController.m) file.

  {% endnote %}

{% endlist %}

### See also

- [Configuring an Android application to send push notifications](../../android/push/android-settings.md)
- [Configuring an iOS application to send push notifications](../../ios/push/ios-settings.md)
- [Launching a push campaign](../../../push/marketing.md)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
