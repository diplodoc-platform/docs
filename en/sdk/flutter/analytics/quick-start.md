# Installation and initialization

To integrate AppMetrica into Flutter, use the [AppMetrica SDK for Flutter](https://pub.dev/packages/appmetrica_plugin) plugin:

## Step 1. Install the AppMetrica SDK for Flutter plugin in your project {#integration}

From the root of the project, run the command:

```bash translate=no
flutter pub add appmetrica_plugin
```

After adding the plugin, you'll see a line with the following dependency in the `pubspec.yaml` file:

```yaml translate=no
dependencies:
   appmetrica_plugin: ^{{ appmetrica-flutter-plugin }}
```

## Step 2. Initialize the library {#initialization}   

1. Add `appmetrica_plugin` import:
   ```java translate=no
   import 'package:appmetrica_plugin/appmetrica_plugin.dart';
   ```

2. Initialize the AppMetrica library using `AppMetrica.activate` and your API key:

   ```bash translate=no
   AppMetrica.activate(AppMetricaConfig("insert_your_api_key_here"));
   ```

3. Send an event using `AppMetrica.reportEvent` to test the operation:

   ```bash translate=no
   AppMetrica.reportEvent('My first AppMetrica event!');
   ```


## Learn more {#learn-more}

- [Sending E-commerce events](flutter-operations.md#send-ecommerce)
- [Sending Revenue data](flutter-operations.md#send-revenue)
- [Sending Ad Revenue data](flutter-operations.md#send-adrevenue)   

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
