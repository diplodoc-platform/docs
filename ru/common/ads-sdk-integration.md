# Интеграция с Yandex Ads SDK

Вы можете использовать аналитические возможности AppMetrica, не инициализируя SDK AppMetrica отдельно, если у вас установлен Yandex Mobile Ads SDK версии 7.6.0 или выше, или один из плагинов:

- Unity Ads SDK версии 7.10.0 и выше; 
- React Ads SDK версии 7.10.0 и выше;
- Flutter Ads SDK версии 7.9.0 и выше.

Также вам доступны автоматически собираемые события взаимодействия с рекламой.

Основные возможности:

1. Автоматическое отслеживание [базовых событий](../data-collection/index.md): установок, стартов и завершений сессий, диплинков, in-app покупок.

    Cобытия начнут отслеживаться автоматически при инициализации Yandex Mobile Ads SDK в приложении. Для этого активируйте интеграцию в интерфейсе AppMetrica. Обновлять код приложения не потребуется.

2. Автоматическое отслеживание событий взамодействия с рекламой Yandex Mobile Ads SDK: запросы рекламы, ответы, показы, клики.

    Данные начнут автоматически поступать в AppMetrica для приложений, которые синхронизированы с Yandex Mobile Ads SDK.

    Если вы инициализируете AppMetrica SDK в приложении самостоятельно, данные начнут поступать автоматически при условии, что в приложении также инициализирован Yandex Mobile Ads SDK и сделана синхронизация с Yandex Mobile Ads в настройках приложения AppMetrica.

## Если вы уже используете AppMetrica в приложении {#already-using}

1. Обновите платформу Yandex Mobile Ads SDK до версии 7.6.0 и выше, или нужный вам плагин:

    - Unity Ads SDK — до версии [7.10.0](https://ads.yandex.com/helpcenter/{{locale}}/dev/unity/changelog-unity#2025) и выше;
    - React Ads SDK — до версии [7.10.0](https://ads.yandex.com/helpcenter/{{locale}}/dev/react-native/changelog-react-native#2025) и выше;
    - Flutter Ads SDK — до версии {% if locale=="ru" %}[7.9.0](https://ads.yandex.com/helpcenter/ru/dev/flutter/changelog-flutter#versiya-790-12-fevralya,-2025){% elsif locale=="en" %}[7.9.0](https://ads.yandex.com/helpcenter/en/dev/flutter/changelog-flutter#version-790-february-12,-2025){% else %}7.9.0{% endif %} и выше.

1. В разделе **{{ settings }}** выберите **{{ syncing-the-ads-sdk }}** и добавьте связь с приложением Yandex Mobile Ads:

    - Используйте тот же Yandex ID, на котором приложение [зарегистрировано](https://appmetrica.yandex.com/application/new) в Yandex Mobile Ads.

    - Убедитесь, что вы прошли [проверку владением приложением]({{ helpcenter-quickstart-step3 }}).

1. Новые данные о взамодействии с рекламой Yandex Mobile Ads SDK появятся в отчете **{{ report-events }}** в течение нескольких минут. Такие события не учитываются в [лимитах на события](limits.md#limit-events).

При необходимости вы можете отключить сбор данных с помощью метода [setAppAdAnalyticsReporting](https://yastatic.net/s3/doc-binary/src/dev/mobile-ads/ru/javadoc/com/yandex/mobile/ads/common/MobileAds.html#setAppAdAnalyticsReporting(java.lang.Boolean)) для Android и [setAppAdAnalyticsReportingEnabled](https://yastatic.net/s3/doc-binary/src/dev/mobile-ads/ru/jazzy/Classes/MobileAds.html#/c:@M@YandexMobileAds@objc(cs)YMAMobileAds(cm)setAppAdAnalyticsReportingEnabled) для iOS в конфигурации Yandex Mobile Ads SDK или удалить связку в настройках синхронизации.

## Если вы ранее не использовали AppMetrica {#not-using}

Активируйте интеграцию при регистрации в интерфейсе ApppMetrica:

1. Обновите платформу Yandex Mobile Ads SDK до версии 7.6.0 и выше, или нужный вам плагин:

    - Unity Ads SDK — до версии [7.10.0](https://ads.yandex.com/helpcenter/{{locale}}/dev/unity/changelog-unity#2025) и выше;
    - React Ads SDK — до версии [7.10.0](https://ads.yandex.com/helpcenter/{{locale}}/dev/react-native/changelog-react-native#2025) и выше;
    - Flutter Ads SDK — до версии {% if locale=="ru" %}[7.9.0](https://ads.yandex.com/helpcenter/ru/dev/flutter/changelog-flutter#versiya-790-12-fevralya,-2025){% elsif locale=="en" %}[7.9.0](https://ads.yandex.com/helpcenter/en/dev/flutter/changelog-flutter#version-790-february-12,-2025){% else %}7.9.0{% endif %} и выше.

1. Убедитесь, что вы прошли [проверку владением приложением]({{ helpcenter-quickstart-step3 }}).

1. Зарегистрируйтесь в AppMetrica с помощью Yandex ID, на котором приложение [зарегистрировано](https://appmetrica.yandex.com/application/new) в Yandex Mobile Ads.

    На шаге 1 отобразится нотификация о возможности привязки приложения Yandex Ads SDK. Если её нет — возможно, используется другой логин или приложение не прошло верификацию.

1. На 3 шаге **{{ syncing-the-ads-sdk }}** укажите, из каких приложений с Ads SDK собирать статистику в AppMetrica.

    Рекомендуется выбрать все платформы (например, iOS и Android) для одного приложения. Больше приложений можно будет добавить на шаге 5.

1. После завершения регистрации статистика начнет собираться в AppMetrica в течение нескольких минут. Обновлять код приложения не нужно.

1. Если вы хотите передавать в AppMetrica [дополнительные данные](../data-collection/index.md), например кастомные [события](../data-collection/about-events.md) — используйте соответствующие методы. Инициализировать AppMetrica не требуется.

1. Если вы хотите использовать возможности расширенной конфигурации AppMetrica — [инициализируйте AppMetrica](../common/quick-start.md#integration-sdk) самостоятельно, используя API Key, указанный в разделе **{{ settings }}** → **{{ main }}**.

## Автоматические события Yandex Mobile Ads SDK {#auto-events}

Доступные события и их параметры:

- `ad_request`: запрос рекламы приложением

  - `ad_type`: тип рекламы, например, `banner`, `interstitial`, `native`, `rewarded`;
  - `block_id`: идентификатор рекламного места;
  - `sdk_version`: версия Yandex Mobile Ads SDK;

- `ad_attempt`: успешный запрос за рекламой в рекламную сеть

  - `ad_type`: тип рекламы, например, `banner`, `interstitial`, `native`, `rewarded`;
  - `block_id`: идентификатор рекламного места;
  - `sdk_version`: версия Yandex Mobile Ads SDK;
  - `ad_network`: рекламная сеть, которая показывает рекламу;

- `ad_filled_request`: запрос, успешно завершившийся подбором рекламы

  - `ad_type`: тип рекламы, например, `banner`, `interstitial`, `native`, `rewarded`;
  - `block_id`: идентификатор рекламного места;
  - `sdk_version`: версия Yandex Mobile Ads SDK;
  - `ad_network`: рекламная сеть, которая показывает рекламу;
  - `banner_id`: идентификатор баннера;

- `ad_impression`: показ рекламы

  - `ad_type`: тип рекламы, например, `banner`, `interstitial`, `native`, `rewarded`;
  - `block_id`: идентификатор рекламного места;
  - `sdk_version`: версия Yandex Mobile Ads SDK;
  - `ad_network`: рекламная сеть, которая показывает рекламу;
  - `banner_id`: идентификатор баннера;
  - `ad_revenue`: доход за показ в валюте рекламной сети;
  - `currency`: валюта рекламной сети;
  - `precision`: точность значения `ad_revenue`. Допустимые значения: `publisher_defined` — значение с учетом порога CPM из интерфейса медиации; `estimated` — значение с учетом автостратегий;

- `ad_click`: клик по рекламе

  - `ad_type`: тип рекламы, например, `banner`, `interstitial`, `native`, `rewarded`;
  - `block_id`: идентификатор рекламного места;
  - `sdk_version`: версия Yandex Mobile Ads SDK;
  - `ad_network`: рекламная сеть, которая показывает рекламу;
  - `banner_id`: идентификатор баннера;

- `ad_reward`: начисление вознаграждения за просмотр рекламы типа rewarded

  - `ad_type`: тип рекламы, например, `banner`, `interstitial`, `native`, `rewarded`;
  - `block_id`: идентификатор рекламного места;
  - `sdk_version`: версия Yandex Mobile Ads SDK;
  - `ad_network`: рекламная сеть, которая показывает рекламу.

## Узнайте больше {#learn-more}  

- [Как использовать возможности расширенной конфигурации AppMetrica SDK?](../troubleshooting/troubleshooting.md#yads-sdk-extended)
- [Нужно ли что-то менять в интеграции, если вы уже используете AppMetrica SDK в приложении?](../troubleshooting/troubleshooting.md#yads-sdk-already-using)
- [Как отключить автоматические события Yandex Ads SDK?](../troubleshooting/troubleshooting.md#yads-sdk-disable-auto)
- [Как инициализировать AppMetrica SDK по логике, отличной от инициализации Yandex Mobile Ads SDK?](../troubleshooting/troubleshooting.md#yads-sdk-other-logic)

{% include notitle [feedback](../_includes/feedback-button.md) %}
