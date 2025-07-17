# Определение местоположения

AppMetrica умеет определять местоположение устройства. Точность определения зависит от конфигурации, с которой инициализируется библиотека:

**С включенной опцией locationTracking**

:   {% note info "" %}

    Для iOS опция включена по умолчанию.

    {% endnote %}

    Местоположение определяется с точностью до города. Информация доступна в [отчетах](../mobile-reports/index.md) и в [Logs API](../mobile-api/logs/about.md).

    Приложение запрашивает доступ к GPS. Расход заряда аккумулятора может увеличиться.

**С отключенной опцией locationTracking**

:   {% note info "" %}

    Начиная с версии 5.0.0 AppMetrica Android SDK опция `locationTracking` по умолчанию отключена.

    Ниже версии 5.0.0 опция `locationTracking` по умолчанию включена.

    {% endnote %}

    Местоположение определяется по IP-адресу с точностью до страны. Информация доступна в [отчетах](../mobile-reports/index.md), но не доступна в [Logs API](../mobile-api/logs/about.md).

    Приложение не запрашивает доступ к GPS. Расход заряда аккумулятора не увеличивается.

    {% note info "" %}

    Если у вас включена маскировка IP-адреса, местоположение определяется так же с точностью до страны по немаскированной части IP-адреса.

    {% endnote %}

## Определение местоположения {#track-location}

Примеры определения местоположения на платформах:

- [Android](../sdk/android/analytics/android-operations.md#track-location)
- [iOS](../sdk/ios/analytics/ios-operations.md#track-location) 
- [Flutter](../sdk/flutter/analytics/flutter-operations.md#track-location) 
- [React Native](../sdk/react-native/analytics/react-native-operations.md#track-location)
- [Unity](../sdk/unity/analytics/unity-operations.md#track-location)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
