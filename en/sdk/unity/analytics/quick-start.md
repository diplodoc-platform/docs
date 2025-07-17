# Installation and initialization

AppMetrica Unity is a plugin for the [Unity3d](http://docs.unity3d.com/) platform. It includes the AppMetrica SDK support for Android and iOS.

This section describes the steps to enable and initialize the AppMetrica Unity plugin:

## Step 1. Enable the AppMetrica Unity plugin {#integration}

{% list tabs %}

- OpenUPM

  Add the following dependencies to [Packages/manifest.json](https://docs.unity3d.com/Manual/upm-manifestPrj.html):

     ```json translate=no
     {
       "scopedRegistries": [
         {
           "name": "package.openupm.com",
           "url": "https://package.openupm.com",
           "scopes": [
             "com.google.external-dependency-manager",
             "io.appmetrica.analytics"
           ]
         }
       ],
       "dependencies": {
         "com.google.external-dependency-manager": "{{ google-external-dependency-manager }}",
         "io.appmetrica.analytics": "{{ appmetrica-unity-plugin }}"
       }
     }
     ```

- UPM (GitHub)

  1. Follow the [documentation](https://github.com/googlesamples/unity-jar-resolver/tree/master?tab=readme-ov-file#getting-started) to enable External Dependency Manager.

  2. Add AppMetrica Unity Plugin to the dependencies in [Packages/manifest.json](https://docs.unity3d.com/Manual/upm-manifestPrj.html):

     ```json translate=no
     {
       "dependencies": {
         "io.appmetrica.analytics": "https://github.com/appmetrica/appmetrica-unity-plugin.git#v{{ appmetrica-unity-plugin }}"
       }
     }
     ```

{% endlist %}

## Step 2. Initialize the library {#initialization}

We recommend activating AppMetrica with [RuntimeInitializeOnLoadMethodAttribute](https://docs.unity3d.com/ScriptReference/RuntimeInitializeOnLoadMethodAttribute.html).

Create a static method with the `[RuntimeInitializeOnLoadMethod(RuntimeInitializeLoadType.BeforeSceneLoad)]` attribute and activate AppMetrica using the `AppMetrica.Activate()` method.

Example:

```csharp translate=no
using Io.AppMetrica;
using UnityEngine;

public static class AppMetricaActivator {
    [RuntimeInitializeOnLoadMethod(RuntimeInitializeLoadType.BeforeSceneLoad)]
    private static void Activate() {
        AppMetrica.Activate(new AppMetricaConfig("APIKey") {
            FirstActivationAsUpdate = !IsFirstLaunch(),
        });
    }

    private static bool IsFirstLaunch() {
        // Implement logic to detect whether the app is opening for the first time.
        // For example, you can check for files (settings, databases, and so on),
        // which the app creates on its first launch.
        return true;
    }
}
```

## Learn more {#learn-more}

- [Sending E-commerce events](unity-operations.md#send-ecommerce)
- [Sending Revenue data](unity-operations.md#send-revenue)
- [Sending Ad Revenue data](unity-operations.md#send-adrevenue)
- [How do I enable user location sending?](../../../troubleshooting/troubleshooting.md#region)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
