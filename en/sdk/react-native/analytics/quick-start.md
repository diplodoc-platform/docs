# Installation and initialization

AppMetrica React Native is a plugin for the [React Native](https://reactnative.dev/) platform. It includes the AppMetrica SDK support for Android and iOS.

The minimum supported version of React Native is 0.59.

The plugin accesses native Android/iOS libraries, so to use it with Expo, you need to follow the [instructions for libraries](https://docs.expo.dev/workflow/using-libraries/#determining-third-party-library-compatibility) that integrate with native components.

This section describes the steps to enable and initialize AppMetrica React Native:

## Step 1. Integrate the AppMetrica React Native plugin {#integration}

{% list tabs %}

- React Native CLI

    1. Install the AppMetrica React Native plugin in your project:

        {% list tabs %}

        - yarn

            ```bash translate=no
            yarn add @appmetrica/react-native-analytics
            ```

        - npm

            ```bash translate=no
            npm install @appmetrica/react-native-analytics
            ```

        {% endlist %}

    2. For React Native version 0.59 and below, run the following console command to link AppMetrica to your project:

        ```bash translate=no
        react-native link @appmetrica/react-native-analytics
        ```

    3. If you're working on an iOS project, execute this command in the console:

        ```bash translate=no
        npx pod-install
        ```

    4. Rebuild your app:

        ```bash translate=no
        # Android:
        npx react-native run-android
        # iOS:
        npx react-native run-ios
        ```

- Expo

    1. The plugin uses native Android and iOS libraries. To use native code, create a development build. [Learn more](https://docs.expo.dev/workflow/using-libraries/#determining-third-party-library-compatibility).

        ```bash translate=no
        npx expo install expo-dev-client
        ```

    2. Install the AppMetrica React Native plugin in your project:

        ```bash translate=no
        npx expo install @appmetrica/react-native-analytics
        ```

    3. Rebuild your app:

        ```bash translate=no
        # Android:
        npx expo run:android
        # iOS:
        npx expo run:ios
        ```

{% endlist %}

## Step 2. Initialize the AppMetrica library {#initialization}

1. Import the library in the source code of your project:

    ```javascript translate=no
    import AppMetrica from '@appmetrica/react-native-analytics';
    ```

    In this case, use `AppMetrica` in the source code for working with the library.

2. Initialize the AppMetrica library using the `activate()` method:

    ```javascript translate=no
    AppMetrica.activate({
      apiKey: 'Your API key',
      sessionTimeout: 120,
      logs: true
    });
    ```

    {% cut "What is an API key?" %}

    {{ api-key }}

    {% endcut %}

3. Send an event to test the library:

    ```javascript translate=no
    // Sends a custom event message and additional parameters (optional).
    AppMetrica.reportEvent('My event');
    AppMetrica.reportEvent('My event', { foo: 'bar' });

    // Send a custom error event.
    AppMetrica.reportError('My error')
    ```

Example of a project with the integrated AppMetrica SDK on [GitHub](https://github.com/yandexmobile/react-native-appmetrica/tree/master/example).

## Learn more {#learn-more}

- [Sending E-commerce events](react-native-operations.md#send-ecommerce)
- [Sending Revenue data](react-native-operations.md#send-revenue)
- [Sending Ad Revenue data](react-native-operations.md#send-adrevenue)
- [Integration examples](https://github.com/yandexmobile/react-native-appmetrica/tree/master/example)
- [How to enable user location sending](../../../troubleshooting/troubleshooting.md#region)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
