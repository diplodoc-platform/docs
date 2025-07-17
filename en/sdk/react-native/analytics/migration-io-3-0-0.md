# Migrating to version 3.0.0

## Running two versions of AppMetrica SDK in parallel {#two-versions}

You can use two versions of AppMetrica SDK in your app in parallel. This is undesirable. Statistics should
be collected normally, but minor deviations are acceptable. In this case, the app size
may increase slightly because it will include two SDKs instead of one.

{% note alert %}

We strongly advise against running two SDK versions with the same `API_KEY` in the app code. This won't cause the app to
crash or fail, but it will lead to inaccurate and unreliable statistics. When migrating to `@appmetrica/react-native-analytics`
, make sure that the `react-native-appmetrica` plugin isn't mentioned in `package-lock.json` or `yarn.lock`.

{% endnote %}

## Migration guide {#about-migration}

This guide contains examples that show the differences between the plugin versions `2.0.0` and `3.0.0`. This section
covers only the methods that lack backward compatibility.

To migrate to the new version, follow these steps:

1. Replace the `react-native-appmetrica` dependency with `@appmetrica/react-native-analytics`. See an example in the [dependency replacement section](#dependencies).
2. Edit the import statement in your code. The required changes are provide in the [dependency importing section](#import).
3. In the project code, replace the classes and methods that were simply renamed. The required changes are indicated in the [dependency renaming section](#rename).

## Replacing dependencies {#dependencies}

{% list tabs %}

- yarn

   ```bash translate=no
   yarn remove react-native-appmetrica && yarn add @appmetrica/react-native-analytics
   ```

- npm

   ```bash translate=no
   npm uninstall react-native-appmetrica && npm install @appmetrica/react-native-analytics
   ```

{% endlist %}

## Importing dependencies {#import}

```javascript translate=no
import AppMetrica from 'react-native-appmetrica';
```
Replace with:
```sh translate=no
import AppMetrica from '@appmetrica/react-native-analytics';
```

## Renamings {#rename}

- The `requestAppMetricaDeviceId()` method was removed. Use the `requestStartupParams()` method to get the IDs.
- The `setStatisticsSending()` method was renamed to `setDataSendingEnabled()`.
