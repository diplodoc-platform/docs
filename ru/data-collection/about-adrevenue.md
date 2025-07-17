# Ad Revenue

Один из типов монетизации мобильного приложения — показ рекламы внутри приложения (Ad Revenue). В AppMetrica можно передавать данные о выручке от показов рекламы. 

## Зачем нужны данные по Ad Revenue {#resolve-tasks}

- Для оценки доходности приложения в целом — от in-app покупок и до рекламной монетизации.
- Для поиска рекламных блоков, форматов и экранов, которые приносят лучшие результаты.
- Для оценки User Acquisition — находите партнеров, которые приносят наибольший доход, и оценивайте эффективность их трафика.
- Для поиска самых прибыльных сегментов пользователей.
- Для оптимизации пользовательских сценариев и роста рекламной монетизации.

## Как рассчитывается Ad Revenue {#calculation}

Данные передаются от SDK для каждого показа рекламного объявления с выручкой от этого события (Impression level Revenue Data).

Все события рекламной выручки в AppMetrica привязываются к пользователям и на основе этих данных рассчитываются метрики для Ad Revenue:

| **Метрика** | **Описание** |
| ----------- | ----------- |
| Ad Revenue события | Количество событий с рекламной выручкой (Ad Revenue) за период отчета. |
| Ad Revenue | Суммарная выручка от рекламной монетизации за период отчета. |
| Ad ARPU | Отношение выручки приложения от рекламной монетизации за период отчета к количеству пользователей приложения за этот же период. Подробнее о [конвертации валют](#currency). |
| eCPM | Отношение суммарной выручки от рекламной монетизации к количеству событий с рекламной выручкой (Ad Revenue) за период отчета, умноженное на 1000. |
| Пользователи с Ad Revenue |Количество пользователей с событиями рекламной выручки (Ad Revenue) за период отчета. |
| Ad Revenue событий на пользователя | Отношение количества событий с рекламной выручкой (Ad Revenue) к количеству пользователей за период отчета. |
| Сессий с Ad Revenue | Количество сессий, в рамках которых были совершены события с рекламной выручкой (Ad Revenue) за период отчета. |
| Ad Revenue событий на сессию | Отношение количества событий с рекламной выручкой (Ad Revenue) к общему количеству сессий за период отчета. |
| % пользователей c Ad Revenue | Отношение количества пользователей с событиями c рекламной выручкой (Ad Revenue) ко всем пользователям за период отчета. |

С учетом данных по Ad Revenue рассчитываются метрики по суммарному доходу:

| **Метрика** | **Описание** |
| ----------- | ----------- |
| Total Revenue | Суммарная выручка от рекламной монетизации, in-app покупок и подписок в приложении за период отчета. Подробнее о [конвертации валют](#currency). |
| Total ARPU | Отношение общей выручки приложения от рекламной монетизации, in-app покупок и подписок за период отчета к количеству пользователей приложения за этот же период. Подробнее о [конвертации валют](#currency). |

## Источники данных {#src-data}

В AppMetrica поддержаны различные способы интеграции с сервисами рекламной монетизации и медиации.

### AppLovin MAX

- Android: [Упрощенная интеграция](../sdk/android/analytics/android-operations.md#send-adrevenue-simple-integration-applovin-max)
- iOS: [Самостоятельная настройка](../sdk/ios/analytics/ios-operations.md#send-adrevenue)
- Flutter: [Самостоятельная настройка](../sdk/flutter/analytics/flutter-operations.md#send-adrevenue)
- Unity: [Упрощенная интеграция](../sdk/unity/analytics/unity-operations.md#adrevenue-autocollection)

### Digital Turbine

- Android: [Упрощенная интеграция](../sdk/android/analytics/android-operations.md#send-adrevenue-simple-integration-digital-turbine)
- iOS: [Самостоятельная настройка](../sdk/ios/analytics/ios-operations.md#send-adrevenue)
- Flutter: [Самостоятельная настройка](../sdk/flutter/analytics/flutter-operations.md#send-adrevenue)
- Unity: [Самостоятельная настройка](../sdk/unity/analytics/unity-operations.md#adrevenue-autocollection)

### Google AdMob

- Android: [Упрощенная интеграция](../sdk/android/analytics/android-operations.md#send-adrevenue-simple-integration-google-admob)
- iOS: [Самостоятельная настройка](../sdk/ios/analytics/ios-operations.md#send-adrevenue)
- Flutter: [Самостоятельная настройка](../sdk/flutter/analytics/flutter-operations.md#send-adrevenue)
- Unity: [Самостоятельная настройка](../sdk/unity/analytics/unity-operations.md#send-adrevenue)

### ironSource

- Android: [Автоматическая интеграция](../sdk/android/analytics/android-operations.md#send-adrevenue-automatic-integration-ironsource)
- iOS: [Самостоятельная интеграция](../sdk/ios/analytics/ios-operations.md#send-adrevenue)
- Flutter: [Самостоятельная настройка](../sdk/flutter/analytics/flutter-operations.md#send-adrevenue)
- Unity: [Самостоятельная настройка](../sdk/unity/analytics/unity-operations.md#adrevenue-autocollection)

### Mobile Ads

- Android: [Самостоятельная настройка](../sdk/android/analytics/android-operations.md#send-adrevenue-manual-integration)
- iOS: [Самостоятельная интеграция](../sdk/ios/analytics/ios-operations.md#send-adrevenue)
- Flutter: [Самостоятельная настройка](../sdk/flutter/analytics/flutter-operations.md#send-adrevenue)
- Unity: [Самостоятельная настройка](../sdk/unity/analytics/unity-operations.md#send-adrevenue)

Вы можете передавать данные любого другого сервиса рекламной монетизации, который предоставляет Impression level Revenue Data.

## Где в AppMetrica доступны метрики по Ad Revenue {#metrics}

**Отчет [In-app и Ad Revenue](../mobile-reports/revenue-report.md)**

:   В отчете Revenue вы можете оценить общий доход приложения, доход от разных типов монетизации (рекламной и in-app), доход по разным рекламным сетям и разным типам объявлений.

**Отчеты [User Acquisition](../mobile-reports/user-acquisition-report.md) и [Remarketing](../mobile-reports/remarketing-report.md)**

:   В этих отчетах вы можете оценить эффективность источников привлечения и возвращения трафика с точки зрения ARPU и других метрик рекламной и in-app монетизации. Обратите внимание, метрики в этом отчете считаются суммарно за весь период жизни пользователя.

**[Когортный анализ](../mobile-reports/cohort-report.md)**

:   В когортном отчете вы сможете оценить какой доход вы получаете от пользователей с течением времени и ARPU на интересующий вас день.

**[Воронки](../mobile-reports/funnels-report.md)**

:   В воронках вы можете оценить какая доля пользователей доходит до просмотра рекламы в целом или, например, доходит до просмотра рекламы с вознаграждением.

**Сегментация**

:   Для построения каждого отчета вы можете выбрать только тех пользователей, которые, например, взаимодействовали с рекламными объявлениями определенной рекламной сети или определенного рекламного формата.

## Конвертация валюты {#currency}

Вы можете передавать Ad Revenue в разных валютах. Список всех поддерживаемых валют см. в разделе [Поддерживаемые валюты](currency-codes.md).

Выручка от Ad Revenue конвертируется во все валюты отчета: USD, EUR, RUB. Для конвертации валюты используется курс, который предоставляют более 15 источников, включая Европейский центральный банк.

Конвертация происходит по курсу, который был днем ранее. Например, если Ad Revenue событие было в день N, то выручка конвертируется по курсу дня N − 1. Конвертация в валюты EUR и RUB происходит относительно USD.

## Отладка отправки Ad Revenue {#test-send}

В AppMetrica нет возможности сегментировать Ad Revenue на "тестовые" и "не тестовые". Если для отладки сбора данных о рекламной монетизации вы используете основной API key, то тестовые события будут попадать в общую статистику. Поэтому, чтобы отладить отправку Ad Revenue, используйте отправку статистики на дополнительный API key с помощью репортера. Подробнее в разделе [{#T}](#send-adrevenue).

## Отправка событий Ad Revenue {#send-adrevenue}

Примеры отправки события Ad Revenue на платформах:

- [Android](../sdk/android/analytics/android-operations.md#send-adrevenue)
- [iOS](../sdk/ios/analytics/ios-operations.md#send-adrevenue)
- [Flutter](../sdk/flutter/analytics/flutter-operations.md#send-adrevenue) 
- [React Native](../sdk/react-native/analytics/react-native-operations.md#send-adrevenue)
- [Unity](../sdk/unity/analytics/unity-operations.md#send-adrevenue)

{% if locale == "ru" %}

## Узнать больше {#learn-more}

- [Рекламная монетизация: как анализировать доход от рекламы в AppMetrica](https://appmetrica.yandex.ru/about/blog/ad-revenue-release)

{% endif %}


{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
