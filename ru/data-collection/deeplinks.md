# Трекинг deeplink

Deeplink — это специальные ссылки, которые позволяют показать пользователю нужный контент в уже установленном приложении. Deeplink могут работать при запуске приложения и в уже открытом приложении.

{% note info "" %}

Для работы с deeplink поддержите их в вашем приложении на [Android](https://developer.android.com/training/app-links/deep-linking#adding-filters) или [iOS](https://developer.apple.com/documentation/xcode/allowing-apps-and-websites-to-link-to-your-content).

{% endnote %}

Начиная с версии SDK iOS/Android 4.0 отслеживание deeplink при открытии приложения работает автоматически. Для включения и выключения автоматического отслеживания используются метод sdk `withAppOpenTrackingEnabled` для Android и свойство `appOpenTrackingEnabled` для iOS. 

Одновременное автоматическое и ручное отслеживание deeplink при открытии приложения не будет дублировать информацию в отчетах. 

## Deeplink внутри приложения {#inside}

Deeplink могут быть использованы не только для запуска приложения, но и для навигации, когда приложение уже открыто.

SDK AppMetrica автоматически не отслеживает deeplink, которые обрабатываются в запущенном приложении. Для отслеживания таких deeplink необходимо дополнительно настроить отслеживание, см. [примеры настройки](#tracking).

## Отслеживание открытий приложения с помощью deeplink {#tracking}

Примеры отслеживания открытий приложения с помощью deeplink на платформах:

- [Android](../sdk/android/analytics/android-operations.md#deeplink)
- [iOS](../sdk/ios/analytics/ios-operations.md#deeplink) 
- [Flutter](../sdk/flutter/analytics/flutter-operations.md#deeplink) 
- [React Native](../sdk/react-native/analytics/react-native-operations.md#deeplink)
- [Unity](../sdk/unity/analytics/unity-operations.md#deeplink)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
