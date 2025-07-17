# ECommerce

При совершении покупок в приложении пользователи выполняют различные действия (ECommerce-события). Например:

- открытие страницы;
- просмотр карточки и страницы товара;
- добавление и удаление товара из корзины;
- начало и завершение оформления покупки.

AppMetrica позволяет собирать информацию о таких действиях и отслеживать статистику в веб-интерфейсе, в отчете [Ecommerce](../mobile-reports/ecommerce-report.md).

Чтобы собирать статистику по ECommerce-событиям, настройте отправку в приложении. Подробнее в разделе [{#T}](#send-ecommerce).

## Настройка группировок и метрик {#metrics}

Отчет «Анализ покупок» можно настроить под ваши задачи с помощью группировок и метрик. Подробнее о доступных группировках и метриках в разделе [Отчет Ecommerce](../mobile-reports/ecommerce-report.md).

Например, с помощью отчета можно оценить:
- количество просмотров карточки или страницы товара;
- количество добавлений в корзину;
- количество покупок;
- объём выручки, возвратов и продаж со скидкой;
- географию покупок с помощью группировки по городам.

## Отладка отправки ECommerce-событий {#debug}

В AppMetrica нет возможности сегментировать ECommerce-события на «тестовые» и «не тестовые». Если для отладки покупок вы используете основной API key, то тестовые события будут попадать в общую статистику. Поэтому, чтобы отладить отправку ECommerce-событий, используйте отправку статистики на дополнительный API key с помощью репортера. Подробнее см. примеры в разделе [{#T}](#send-ecommerce).

## Отправка ECommerce-событий {#send-ecommerce}

Примеры отправки ECommerce-события на платформах:

- [Android](../sdk/android/analytics/android-operations.md#send-ecommerce)
- [iOS](../sdk/ios/analytics/ios-operations.md#send-ecommerce)
- [Flutter](../sdk/flutter/analytics/flutter-operations.md#send-ecommerce)
- [React Native](../sdk/react-native/analytics/react-native-operations.md#send-ecommerce)
- [Unity](../sdk/unity/analytics/unity-operations.md#send-ecommerce)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
