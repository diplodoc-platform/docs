# Migrating to version 2.0.0

## Running two versions of AppMetrica Push SDK in parallel {#two-versions}

Two versions of the AppMetrica Push SDK can concurrently run in one app.

{% note alert %}

We don't recommend that you use several AppMetrica Push SDK versions in one app, because this can lead to anomalies in reports. In other words, you shouldn't activate `AppMetricaPush` while using the `AppMetricaPush` prefab from the older version. While that won't cause crashes or failures in the app, it will distort and disrupt the statistics. When migrating to the new plugin version, make sure you don't have the `Assets/AppMetricaPush` directory. The new plugin version is provided via UPM and saved to `Library/PackageCache/io.appmetrica.analytics.push@hash`.

{% endnote %}

## Migration guide {#about-migration}

This guide contains examples that show the differences between the plugin versions `1.1.0` and `2.0.0`. This section only covers methods that do not have backward compatibility.

To migrate to the new version, follow these steps:

1. Remove the previous plugin version.
2. Add the new plugin version using UPM. For more information, see the [section on enabling the plugin](#integration).
3. Replace the prefab with activation via [RuntimeInitializeOnLoadMethodAttribute](https://docs.unity3d.com/ScriptReference/RuntimeInitializeOnLoadMethodAttribute.html). For more information, see the [section on replacing the prefab](#init-change).
4. In the project code, replace the classes and methods that have been renamed or only changed their package. For more information, see the [section on renamings](#rename).

### Enabling AppMetrica Push Unity plugin 2.0.0 {#integration}

The plugin is enabled via the [Unity Package Manager](https://docs.unity3d.com/Manual/Packages.html).

Add the following dependencies to [Packages/manifest.json](https://docs.unity3d.com/Manual/upm-manifestPrj.html):

```json translate=no
{
  "dependencies": {
      "io.appmetrica.analytics.push": "https://github.com/appmetrica/push-unity-plugin.git#v2.0.0"
  }
}
```

### Replacing the prefab {#init-change}

1. Create a static method with the `[RuntimeInitializeOnLoadMethod(RuntimeInitializeLoadType.BeforeSceneLoad)]` attribute and activate AppMetricaPush using the `AppMetricaPush.Activate()` method.

   > **Example:**
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

2. Remove the `AppMetricaPush` prefab from your scenes.

## Renaming the API {#rename}

{% note info %}

To work with AppMetricaPush, use static methods from the `AppMetricaPush` class. To do this, replace `AppMetricaPush.Instance` with `AppMetricaPush` and import `Io.AppMetricaPush`.

{% endnote %}

* Removed the `IYandexAppMetricaPush` interface and transferred its methods to the `AppMetricaPush` class.
    * Renamed the `Initialize` method as `Activate`.
