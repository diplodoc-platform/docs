# Начало работы

## Шаг 1. Создайте аккаунт и настройте приложение {#create-user}

{% note info %}

Для работы с AppMetrica необходим Яндекс ID. Если у вас его нет, [зарегистрируйтесь](https://passport.yandex.{{ domain }}/passport?mode=register).

{% endnote %}

#|
|| **Действие** | **Роль** | **Примерное время** | **Комментарий** ||
|| Зарегистрируйтесь в AppMetrica и настройте аккаунт |
* Менеджер по продукту
* Разработчик | 10 мин. |
* Заполните информацию о вашей компании и о вашем приложении. 

    Если компания зарегистрирована не в РФ, используйте буквы латинского алфавита.
* Сохраните API key из настроек кабинета, его нужно будет передать вашему разработчику для интеграции SDK.
  
  {% cut "Что такое API key?" %}

  {{ api-key }}

  {% endcut %} ||
|| Выдайте коллегам доступы в кабинет AppMetrica |
* Менеджер по продукту
* Разработчик | 1 мин. на пользователя | AppMetrica имеет разные уровни доступа, ознакомьтесь с ними в статье [Управление доступом](access.md). ||
|#

## Шаг 2. Интегрируйте AppMetrica SDK {#integration-sdk}

#|
|| **Действие** | **Роль** | **Примерное время** | **Комментарий** ||
|| Выберите платформу для интеграции AppMetrica SDK |
* Менеджер по продукту
* Разработчик | 10 мин. | AppMetrica доступна для нативных приложений на [Android](../sdk/android.yaml) и [iOS](../sdk/ios.yaml). Также доступны плагины [Unity](../sdk/unity.yaml) \| [Flutter](../sdk/flutter.yaml) \| [React Native](../sdk/react-native.yaml).

_Рекомендация: используйте один API key для обоих версий вашего приложения._ ||
|| Выберите расширенные настройки SDK |
* Менеджер по продукту
* Разработчик | 30 мин. | Команда AppMetrica рекомендует использовать дополнительные возможности:
* [Импорт атрибуций из других SDK](../data-collection/attribution-integration.yaml).
* Учет новых пользователей при интеграции SDK в действующее приложение ([Android](../sdk/android/analytics/android-operations.md#new-user) \| [iOS](../sdk/ios/analytics/ios-operations.md#new-user)).
* Настройка использования рекламных идентификаторов GAID/IDFA ([Android](../sdk/android/get-ad-id.md) \| [iOS](../mobile-tracking/ios-tracking.md)).
* Настройка использования [deeplink](../sdk/android/analytics/android-operations.md#deeplink) и [Universal link](../sdk/ios/analytics/ios-universal-links.md).

Больше информации можно найти в разделах [Android](../sdk/android.yaml), [iOS](../sdk/ios.yaml), [Unity](../sdk/unity.yaml), [Flutter](../sdk/flutter.yaml), [React Native](../sdk/react-native.yaml).
||
|| Определите, какие базовые события приложения необходимо собирать |
* Менеджер по продукту
* Разработчик | 30 мин. | В AppMetrica есть [разные типы событий](../data-collection/index.md), часть базовых событий собирается автоматически, а часть настраивается вручную разработчиком, например:
* [E-commerce](../data-collection/about-ecommerce.md)
* [AdRevenue](../data-collection/about-adrevenue.md)
* [Ошибки](../data-collection/about-crashes-and-errors.md) ||
|| Определите, какие кастомные события необходимо собирать |
* Менеджер по продукту
* Разработчик | 30 мин. | AppMetrica позволяет собирать статистическую информацию о [собственных событиях приложения](../mobile-reports/events-report.md).

_Рекомендация: ознакомьтесь с [лимитами](../troubleshooting/limit-events.md) на кастомные события._ ||
|| Передайте собранную информацию вашему разработчику |
* Разработчик | 3 часа | Ресурсы для разработчиков, которые могут помочь:
* [Интеграция для Android](../sdk/android/analytics/quick-start.md)
* [Интеграция для iOS](../sdk/ios/analytics/quick-start.md)
* [Интеграция для Unity](../sdk/unity/analytics/quick-start.md)
* [Интеграция для Flutter](../sdk/flutter/analytics/quick-start.md)
* [Интеграция для React Native](../sdk/react-native/analytics/quick-start.md)
* Примеры использования методов на [Android](../sdk/android/analytics/android-operations.md), [iOS](../sdk/ios/analytics/ios-operations.md), [Unity](../sdk/unity/analytics/unity-operations.md), [Flutter](../sdk/flutter/analytics/flutter-operations.md), [React Native](../sdk/react-native/analytics/react-native-operations.md)
* [Настройка сбора данных](../data-collection/index.md) ||
|#

## Дополнительные инструменты {#advanced}

### Интегрируйте AppMetrica Push SDK {integration-push-sdk}

#|
|| **Действие** | **Роль** | **Примерное время** | **Комментарий** ||
|| Выберите платформу для интеграции AppMetrica Push SDK |
* Менеджер по продукту
* Разработчик | 10 мин. | AppMetrica Push SDK доступна для нативных приложений на [Android](../sdk/android.yaml) и [iOS](../sdk/ios.yaml). Также доступны плагины [Unity](../sdk/unity.yaml) \| [Flutter](../sdk/flutter.yaml). ||
|| Ознакомьтесь с [особенностями интеграции](../sdk/android/push/android-other-push-services-settings.md) при использовании с другими push-сервисами |
* Разработчик | 30 мин. | Необходимо научиться перенаправлять сообщения между интегрированными SDK. ||
|| Ознакомьтесь с [возможностями Push API](../mobile-api/push/about.md) |
* Менеджер по продукту
* Разработчик | 20 мин. | AppMetrica позволяет отправлять push-уведомления не только через интерфейс сервиса, но и при помощи API. ||
|#

### Ознакомьтесь с инструментами аналитики от AppMetrica {#appmetrica-analytics}

#### Отчеты {#reports}

[Веб-интерфейс AppMetrica](http://appmetrika.yandex.{{domain}}/) позволяет просматривать статистику использования мобильного приложения.

#|
|| **{{ reports }}** → **{{ report-product }}** | > ||
|| [Вовлеченность](../mobile-reports/engagement-report.md) | Отчет поможет:
* Оценить время, проведенное пользователями в приложении
* Определить среднюю продолжительность сессии
* Оценить частоту использования приложения
* Сравнить показатели вовлеченности разных групп пользователей ||
|| [Retention-анализ](../mobile-reports/retention-report.md) | Отчет поможет оценить:
* Насколько востребованы те или иные функции приложения
* Как обновление приложения повлияло на возвращаемость
* Life Time пользователя в приложении ||
|| [Воронки](../mobile-reports/funnels-report.md) | Отчет поможет:
* Сравнить конверсию в целевое действие на разных версиях приложения
* Оценить динамику конверсии поведенческого сценария
* Оценить какой части аудитории понадобилась та или иная функция приложения ||
|| [Аудитория](../mobile-reports/audience-report.md) | Отчет поможет оценить:
* Какую аудиторию привлекает рекламная кампания
* Как изменения в приложении влияют на приток пользователей из определенного региона ||
|| [Когортный анализ](../mobile-reports/cohort-report.md) | Отчет поможет оценить:
* Качество источников трафика
* Качество аудитории, которая пришла через партнеров
* Количество пользователей, которые совершили событие в выбранной когорте ||
|| [События](../mobile-reports/events-report.md) | Отчет поможет:
* Определить охват и популярность функций приложения
* Сравнить поведение разных групп пользователей
* Оценить частоту использования функций в рамках сессий
* Проанализировать вложенные параметры событий ||
|| [Отчет по профилям](../mobile-reports/profile-report.md) | Отчет отображает распределение пользователей по заднным атрибутам, в том числе, собственным. Это единственный отчет, который считает пользователей исходя из `profile_id` ||
|| **{{ reports }}** → **{{ report-marketing }}** | > ||
|| [User Acquisition](../mobile-reports/user-acquisition-report.md) | Отчет содержит информацию об источниках установки приложения ||
|| [User Acquisition SKAdNetwork](../mobile-reports/user-acquisition-skadnetwork.md) | Отчет содержит информацию об источниках установки приложения, полученных из SKAdNetwork — системы атрибуции кампаний на iOS 14.5+, обеспечивающей приватность пользователей ||
|| [Push-кампании](../mobile-reports/push-campaign.md) | Отчет отображает статистическую информацию о проводимых push-кампаниях: количество отправленных, доставленных и открытых push-уведомлений ||
|| [Remarketing](../mobile-reports/remarketing-report.md) | В отчете отображаются данные о возврате пользователей в приложение (re-engagement), а также о совершенных ими целевых событиях ||
|| **{{ reports }}** → **{{ report-monetization }}** | > ||
|| [Ecommerce](../mobile-reports/ecommerce-report.md) | Отчет отображает какие действия совершают пользователи при совершении покупок ||
|| [In-app и Ad Revenue](../mobile-reports/revenue-report.md) | Отчет поможет оценить:
* Успешность введения новых возможностей с помощью метрики ARPU
* Реакцию пользователей на изменение цен с помощью метрики ARPPU
* Популярные продукты в приложении
* Географию покупок с помощью группировки по городам
* Доходность отдельных рекламных сетей и блоков ||
|| **{{ reports }}** → **{{ report-crashes-and-errors }}** | > ||
|| [Крэши/ошибки](../mobile-reports/crashes-and-errors.md) | Отчет поможет определить, какие крэши/ошибки случаются чаще всего ||
|#

#### API {#api}

- [API управления](../mobile-api/management/intro.md) — позволяет добавлять, редактировать, удалять приложения.
- [API отчетов](../mobile-api/api_v1/intro.md) — позволяет получать статистику приложения.
- [Logs API](../mobile-api/logs/about.md) — позволяет получить неагрегированные данные о приложении.
- [Data Stream API](../mobile-api/datastream/about.md) — позволяет выгружать данные в виде файлов формата CSV или JSON.
- [Post API](../mobile-api/post/about.md) — позволяет загружать информацию о событиях в AppMetrica.
- [Push API](../mobile-api/push/about.md) — позволяет создавать push-кампании.

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
