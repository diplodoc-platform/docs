# Подключение и инициализация

AppMetrica React Native — это плагин для платформы [React Native](https://reactnative.dev/). Он включает поддержку AppMetrica SDK для Android и iOS.

Минимальная поддерживаемая версия React Native — 0.59.

Чтобы использовать плагин с Expo, нужно выполнить [инструкции для библиотек](https://docs.expo.dev/workflow/using-libraries/#determining-third-party-library-compatibility), работающих с нативной частью, так как плагин обращается к нативным Android/iOS библиотекам.

Ниже описаны этапы подключения и инициализации AppMetrica React Native:

## Шаг 1. Подключите плагин AppMetrica React Native {#integration}

{% list tabs %}

- React Native CLI

    1. Установите плагин AppMetrica React Native в ваш проект:

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

    2. Для React Native версии 0.59 и ниже, выполните следующую консольную команду для связывания AppMetrica с вашим проектом:

        ```bash translate=no
        react-native link @appmetrica/react-native-analytics
        ```

    3. Для проектов на платформе iOS выполните следующую консольную команду:

        ```bash translate=no
        npx pod-install
        ```

    4. Пересоберите ваше приложение:

        ```bash translate=no
        # Android:
        npx react-native run-android
        # iOS:
        npx react-native run-ios
        ```

- Expo

    1. Плагин использует нативные библиотеки Android и iOS. Чтобы использовать нативный код, создайте development build. [Подробнее](https://docs.expo.dev/workflow/using-libraries/#determining-third-party-library-compatibility).

        ```bash translate=no
        npx expo install expo-dev-client
        ```

    2. Установите плагин AppMetrica React Native в ваш проект:

        ```bash translate=no
        npx expo install @appmetrica/react-native-analytics
        ```

    3. Пересоберите ваше приложение:

        ```bash translate=no
        # Android:
        npx expo run:android
        # iOS:
        npx expo run:ios
        ```

{% endlist %}

## Шаг 2. Инициализируйте библиотеку AppMetrica {#initialization}

1. Импортируйте библиотеку в исходном коде вашего проекта:
    
    ```javascript translate=no
    import AppMetrica from '@appmetrica/react-native-analytics';
    ```
    
    В этом случае используйте `AppMetrica` в коде проекта для работы с библиотекой.
    
2. Инициализируйте библиотеку AppMetrica с помощью метода `activate()`:
    
    ```javascript translate=no
    AppMetrica.activate({
      apiKey: 'Your API key',
      sessionTimeout: 120,
      logs: true
    });
    ```

    {% cut "Что такое API key?" %}

    {{ api-key }}

    {% endcut %}
    
3. Отправьте событие, чтобы протестировать работу библиотеки:
    
    ```javascript translate=no
    // Sends a custom event message and additional parameters (optional).
    AppMetrica.reportEvent('My event');
    AppMetrica.reportEvent('My event', { foo: 'bar' });
    
    // Send a custom error event.
    AppMetrica.reportError('My error')
    ```

Пример проекта с интегрированной AppMetrica SDK на [GitHub](https://github.com/yandexmobile/react-native-appmetrica/tree/master/example).

## Узнайте больше {#learn-more}

- [Настройка отправки событий Ecommerce](react-native-operations.md#send-ecommerce)
- [Настройка отправки событий Revenue](react-native-operations.md#send-revenue)
- [Настройка отправки событий Ad Revenue](react-native-operations.md#send-adrevenue)
- [Пример интеграции плагина](https://github.com/yandexmobile/react-native-appmetrica/tree/master/example)
- [Как включить отправку данных о местоположении пользователей](../../../troubleshooting/troubleshooting.md#region) 

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
