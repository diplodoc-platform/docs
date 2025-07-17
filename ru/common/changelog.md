# Changelog

## 2025 {#year-2025}

### Июнь 2025 {#june-2025}

- Открыт обучающий курс по AppMetrica для начинающих пользователей в виде [Телеграм-бота](https://t.me/AppMetrica_training_bot).
- Обновлен и улучшен интерфейс [воркспейсов](../mobile-reports/workspaces.md). 
- Добавлена возможность создавать собственные [виджеты](../mobile-reports/widgets.md#custom) с помощью конструктора.
- В [отчеты](../mobile-reports/index.md) добавлена форма обратной связи для отправки пожеланий по улучшению. 
- Реализована возможность [управлять правилами конверсии](../mobile-tracking/conversions.md).
- Изменены [правила отправки RCPA-постбеков](../mobile-tracking/postback-first-target-event-only.md).

### Апрель 2025 {#april-2025}

- Добавлен отчет [Конверсии](../mobile-reports/conversions-report.md).
- Возможность [сравнения двух произвольных сегментов и периодов](../mobile-reports/segment-comparison.md) добавлена в отчеты:
   - [Аудитория](../mobile-reports/audience-report.md)
   - [Вовлеченность](../mobile-reports/engagement-report.md)
   - [Профили](../mobile-reports/profile-report.md)
   - [Ecommerce](../mobile-reports/ecommerce-report.md)
   - [In-app и Ad Revenue](../mobile-reports/revenue-report.md)
- В API управления добавлен метод, который [проверяет доступность Logs API](../mobile-api/management/logs-api-status.md). 

### Март 2025 {#march-2025}

- Теперь трекер автоматически переносится в архив, если в нем не было зафиксировано событий установки приложения или перехода по deeplink в течение 365 дней. Ранее этот срок составлял 180 дней.
- Для интеграции с [Yandex Ads SDK](ads-sdk-integration.md) добавлены требования по минимальным версиям плагинов: 
   - Unity Ads SDK — [7.10.0](https://ads.yandex.com/helpcenter/{{locale}}/dev/unity/changelog-unity#2025) и выше;
   - React Ads SDK — [7.10.0](https://ads.yandex.com/helpcenter/{{locale}}/dev/react-native/changelog-react-native#2025) и выше;
   - Flutter Ads SDK — {% if locale=="ru" %}[7.9.0](https://ads.yandex.com/helpcenter/ru/dev/flutter/changelog-flutter#versiya-790-12-fevralya,-2025){% elsif locale=="en" %}[7.9.0](https://ads.yandex.com/helpcenter/en/dev/flutter/changelog-flutter#version-790-february-12,-2025){% else %}7.9.0{% endif %} и выше. 

### Февраль 2025 {#february-2025}

- Обновлен интерфейс [списка трекеров](../mobile-tracking/index.md#tracker-list).
- В отчете [Remarketing](../mobile-reports/remarketing-report.md#deeplinks) теперь можно выбирать просмотр данных по re-engagement deeplinks или всем deeplinks.
{% if tld == "com" %}- Реализована интеграция AppMetrica с [Apphud](../data-collection/apphud/apphud-about.md).{% endif %}
- Обновлена версия AppMetrica SDK Android до [7.7.0](../sdk/android/changelog-android.md#s-7-7-0).
- Обновлена версия AppMetrica Push SDK iOS до [3.0.2](../sdk/ios/changelog-ios.md#v-push-3-0-2).

### Январь 2025 {#january-2025}

- В отчетах [Аудитория](../mobile-reports/audience-report.md), [Ecommerce](../mobile-reports/ecommerce-report.md), [Вовлеченность](../mobile-reports/engagement-report.md), [Профили](../mobile-reports/profile-report.md), [Push-кампании](../mobile-reports/push-campaign.md) и [Revenue](../mobile-reports/revenue-report.md) добавлена группировка по атрибутам профиля.
- В Data Stream API добавлена возможность экспорта:
   - [конверсий](../mobile-api/datastream/data-type-fields.md#attributed_event) (`attributed_event`);
   - [deeplink](../mobile-api/datastream/data-type-fields.md#deeplinks) (`deeplink`).
- Обновлена версия AppMetrica Push SDK iOS до [3.0.0](../sdk/ios/changelog-ios.md#v-push-3-0-0):
   - Убран режим работы через App Group. Поддерживается только режим работы, при котором события отправляются напрямую в AppMetrica (требуется [настройка](../sdk/ios/analytics/ios-appgroup.md)). 
   - Обновлена зависимость: AppMetrica-5.9.0.
- Добавлена инструкция по настройке трекинга [Единой перфоманс-кампании](../mobile-tracking/yandex-direct-upc-tracking.md) и размещения в формате [Web+App](../mobile-tracking/yandex-direct-web-app-tracking.md) в интеграции с Яндекс Директом. 
- Обновлена версия AppMetrica Push SDK Android до [4.1.1](../sdk/android/changelog-android.md#v-4-1-1).
- Обновлена версия AppMetrica SDK Android до [7.6.0](../sdk/android/changelog-android.md#s-7-6-0).

## 2024 {#year-2024}

### Декабрь, 2024 {#december-2024}

- Обновлена версия AppMetrica SDK Android до [7.5.0](../sdk/android/changelog-android.md#s-7-5-0). Добавлен API для управления доступом к рекламным идентификаторам (GAID, Huawei OAID). Подробнее в [документации](../sdk/android/analytics/android-operations.md#track-adv-identifiers).
- Обновлена версия AppMetrica SDK iOS до [5.9.0](../sdk/ios/changelog-ios.md#v-5-9-0).
- Обновлена версия AppMetrica Gradle Plugin до [1.0.1](../sdk/android/changelog-android.md#c-1-0-1).
- В Data Stream API добавлены [новые поля](../mobile-api/datastream/data-type-fields.md#installations) для выгрузки статуса оценки фрода и обновления установок.

### Ноябрь, 2024 {#november-2024}

- Добавлена возможность [подключения проверки на антифрод](../mobile-tracking/add-tracker.md) при создании или редактировании трекеров.
- Вердикты антифрода FraudScore доступны в отчете [User Acquisition](../mobile-reports/user-acquisition-report.md) в группировке и сегментации по новому параметру **Оценка фрода**. 
- В отчете [Аудитория](../mobile-reports/audience-report.md) добавлены новые метрики:
   - **Неактивные пользователи**
   - **Вернувшиеся пользователи**
   - **Доля неактивных пользователей**
   - **Доля вернувшихся пользователей**
- Обновлена версия AppMetrica SDK Android до [7.3.0](../sdk/android/changelog-android.md#s-7-3-0).
- Обновлена версия AppMetrica Push SDK iOS до [2.2.1](../sdk/ios/changelog-ios.md#v-push-2-2-1).
- Добавлено описание [подключения AppMetrica SDK](../sdk/react-native/analytics/quick-start.md#integration) в приложения на React Native Expo.
- Обновлена версия AppMetrica Gradle Plugin до [1.0.0](../sdk/android/changelog-android.md#c-1-0-0).
- Добавлен новый отчет по [ANR](../mobile-reports/anr.md). Отчет позволяет определить, в каких случаях ANR случается чаще всего.

### Октябрь, 2024 {#october-2024}

- Обновлена версия AppMetrica SDK iOS до [5.8.2](../sdk/ios/changelog-ios.md#v-5-8-2).
- Обновлена версия AppMetrica Push SDK iOS до [2.2.0](../sdk/ios/changelog-ios.md#v-push-2-2-0).
- Обновлена версия AppMetrica SDK Android до [7.2.2](../sdk/android/changelog-android.md#s-7-2-2).
- Обновлена версия AppMetrica SDK React Native до [3.3.0](../sdk/react-native/changelog.md#v-3-3-0).
- Добавлена [интеграция с Yandex Ads SDK](ads-sdk-integration.md): автоматический сбор базовых и рекламных событий.
- В AppMetrica появилась возможность [импорта атрибуций из других SDK](../data-collection/attribution-integration-react.md) для React Native.
- Реализована возможность отправлять [Ad Revenue события](../data-collection/about-adrevenue.md) в рекламные сети с помощью постбеков.

### Сентябрь, 2024 {#september-2024}

- Обновлен интерфейс отчетов.
- Обновлен список метрик в отчете [Remarketing](../mobile-reports/remarketing-report.md):
   - метрика, которая раньше называлась **Deeplinks**, переименована в **Re-engagement Deeplinks** — она отображает количество переходов в рамках ремаркетинг-кампаний;
   - метрика **Re-engagements** переименована в **Re-engagement Users** — отображает количество уникальных пользователей, выполнивших переход в рамках ремаркетинг-кампаний;
   - добавлена новая метрика **Deeplinks** — количество переходов по трекинг-ссылкам партнеров.
- В отчетах добавлена возможность группировки и сегментации по источнику атрибуции:
   - в группировках — **Атрибуты профиля** → **Установка** → **Источник атрибуции**;
   - в сегментах — **Пользователи** → **Установка** → **Источник атрибуции**.
- Обновлена версия AppMetrica SDK Android до [7.2.0](../sdk/android/changelog-android.md#s-7-2-0).
- Обновлена версия AppMetrica SDK iOS до [5.8.0](../sdk/ios/changelog-ios.md#v-5-8-0).
- Обновлена версия AppMetrica Push SDK iOS до [2.1.0](../sdk/ios/changelog-ios.md#v-push-2-1-0).
- В Logs API обновлен ресурс [{#T}](../mobile-api/logs/ref/profiles.md), в версии `profiles_v2` добавлены обязательные параметры `date_since` и `date_until`.
- [Добавлено определение источника атрибуции](../mobile-tracking/auto-create-tracking.md) для deeplinks на основе данных из URL-параметров.
- Обновлена версия AppMetrica Flutter SDK до [3.1.0](../sdk/flutter/changelog.md#v-3-1-0).
- Обновлена версия AppMetrica Flutter Push SDK до [2.0.0](../sdk/flutter/changelog.md#v-push-2-0-0).
- Обновлена версия AppMetrica SDK Unity до [6.3.0](../sdk/unity/changelog.md#v-6-3-0).
- Обновлена версия AppMetrica SDK React Native до [3.2.0](../sdk/react-native/changelog.md#v-3-2-0).

{% cut "Август – январь 2024" %}

#### Август, 2024 {#august-2024}

- В Logs API появился новый тип данных — [E-commerce](../mobile-api/logs/ref/ecommerce_events.md).
- Обновлена версия AppMetrica SDK iOS до [5.7.0](../sdk/ios/changelog-ios.md#v-5-7-0).
- Добавлена [верификация событий](../data-collection/index.md#verification-events) для Android.
- В Data Stream API добавлен новый параметр `certificate_verification_status`, который возвращает результат проверки совпадения целевого отпечатка сертификата с тем, который поступил вместе с событием.
- Обновлена версия AppMetrica SDK Android до [7.1.0](../sdk/android/changelog-android.md#s-7-1-0). Добавлен [API для упрощенной отправки ILRD](../sdk/android/analytics/android-operations.md#send-adrevenue) (Impression Level Revenue Data) из Applovin MAX, Digital Turbine, Google AdMob.
- Обновлена версия AppMetrica Flutter SDK до [3.0.0](../sdk/flutter/changelog.md#v-3-0-0).

#### Июль, 2024 {#july-2024}

- В Logs API появился новый тип данных — [Ad Revenue](../mobile-api/logs/ref/ad_revenue_events.md)
- В Data Stream API появились новые типы данных — [Ad Revenue](../mobile-api/datastream/data-type-fields.md#ad_revenue) и [ecommerce](../mobile-api/datastream/data-type-fields.md#ecommerce).
- В Data Stream API добавлено новое поле экспорта: `district`.
- В AppMetrica введен [лимит на количество профилей](limits.md#limit-profile) для одного устройства — не более 500.
- Обновлена версия AppMetrica SDK Unity до [6.2.0](../sdk/unity/changelog.md#v-6-2-0).
- Обновлена версия AppMetrica Push SDK Android до [4.0.0](../sdk/android/changelog-android.md#v-4-0-0).
- Обновлена версия AppMetrica SDK React Native до [3.1.0](../sdk/react-native/changelog.md#v-3-1-0).

#### Июнь, 2024 {#june-2024}

- Доступны новые [макросы](../mobile-tracking/postback-specification.md): `{start_datetime}`, `{start_timestamp}`, `{start_timezone}`, `{session_id}`, `{profile_id}`, `{ecom_type}`.
- Обновлена версия AppMetrica SDK React Native до [3.0.0](../sdk/react-native/changelog.md#v-3-0-0). Глобальное обновление плагина. Подробнее в [инструкции по миграции](../sdk/react-native/analytics/migration-io-3-0-0.md).
- В Data Stream API появился новый тип данных — [Окончание сессий](../mobile-api/datastream/data-type-fields.md#session_end).
- Обновлена версия AppMetrica SDK iOS до [5.6.0](../sdk/ios/changelog-ios.md#v-5-6-0).
- Обновлена версия AppMetrica SDK Android до [7.0.0](../sdk/android/changelog-android.md#s-7-0-0).

#### Май, 2024 {#may-2024}

- В AppMetrica появилась возможность [импорта атрибуций из других SDK для Flutter](../data-collection/attribution-integration-flutter.md).
- Обновлена версия крэш-плагина до [0.11.0](../sdk/android/changelog-android.md#c-0-11-0).
- Обновлена версия AppMetrica Flutter SDK до [2.1.1](../sdk/flutter/changelog.md#v-2-1-1).
- Обновлена версия AppMetrica Flutter Push SDK до [1.0.0](../sdk/flutter/changelog.md#v-push-1-0-0).
- Обновлена версия AppMetrica SDK Unity до [6.1.0](../sdk/unity/changelog.md#v-6-1-0).
- Обновлена версия AppMetrica Push SDK Unity до [2.0.0](../sdk/unity/changelog.md#p-2-0-0). Глобальное обновление плагина. Подробнее в [инструкции по миграции](../sdk/unity/push/migration-io-2-0-0.md).
- Обновлена версия AppMetrica SDK iOS до [5.4.0](../sdk/ios/changelog-ios.md#v-5-4-0).
- Обновлена версия AppMetrica Push SDK Android до [3.3.0](../sdk/android/changelog-android.md#v-3-3-0).

#### Апрель, 2024 {#april-2024}

- Обновлена версия AppMetrica SDK Android до [6.5.0](../sdk/android/changelog-android.md#s-6-5-0).
- Обновлена версия AppMetrica SDK iOS до [5.2.0](../sdk/ios/changelog-ios.md#v-5-2-0).
- Обновлена версия AppMetrica SDK Unity до [6.0.1](../sdk/unity/changelog.md#v-6-0-1). Глобальное обновление плагина. Подробнее в [инструкции по миграции](../sdk/unity/analytics/migration-io-6-0-0.md).
- В AppMetrica появилась возможность [импорта атрибуций из других SDK](../data-collection/attribution-integration.yaml) для iOS и Unity.
- В Data Stream API появился новый тип данных — [Revenue](../mobile-api/datastream/data-type-fields.md#revenue).
- В Data Stream API добавлены новые поля экспорта: `huawei_oaid`, `country`, `area`, `event_source`, `appmetrica_sdk_version`.
- В Logs API добавлены новые поля экспорта: `is_revenue_autocollected`, `revenue_event_type`, `revenue_inapp_type` для Revenue.
- Обновлена версия AppMetrica Push SDK Android до [3.2.0](../sdk/android/changelog-android.md#v-3-2-0).
- Обновлена версия крэш-плагина до [0.10.0](../sdk/android/changelog-android.md#c-0-10-0).
- Обновлена версия AppMetrica Push SDK iOS до [2.0.0](../sdk/ios/changelog-ios.md#v-push-2-0-0). Обновлены идентификатор библиотеки и API. Библиотека разделена на модули. Подробнее в [инструкции по миграции](../sdk/ios/push/migration-io-push-2-0-0.md).

#### Март, 2024 {#march-2024}

- Добавлен [трекинг кампаний Petal Ads](../mobile-tracking/petalads-settings.md).
- Добавлен новый тип предустановок приложений — PAI (Google Play Auto Install). Подробнее в статье [Предустановка приложений через PAI](../mobile-tracking/preinstalled-app-attr.md#pai).
- [Добавлено определение источника атрибуции](../mobile-tracking/auto-create-tracking.md) для установок на основе данных из URL-параметров.
- Обновлена версия AppMetrica SDK Android до [6.3.0](../sdk/android/changelog-android.md#s-6-3-0).
- Обновлена версия AppMetrica SDK iOS до [5.1.0](../sdk/ios/changelog-ios.md#v-5-1-0).

#### Февраль, 2024 {#february-2024}

- Обновлена версия AppMetrica SDK iOS до [5.0.0](../sdk/ios/changelog-ios.md#v-5-0-0). Обновлены идентификатор библиотеки и API. Пакет `com.yandex.mobile.appmetrica` заменен на `io.appmetrica`. Подробнее в [инструкции по миграции](../sdk/ios/analytics/migration-io-5-0-0.md).
- Добавлена информация по [партнерам](../ad-network/partner-directory/performance-agencies.md) и [интеграциям](../ad-network/integrations/engines-and-environments.md).
- Обновлена версия крэш-плагина до [0.9.0](../sdk/android/changelog-android.md#c-0-9-0).

#### Январь, 2024 {#january-2024}

- Обновлена версия AppMetrica SDK Android до [6.2.1](../sdk/android/changelog-android.md#s-6-2-1).
- В AppMetrica появилась возможность [импорта атрибуций из других SDK](../data-collection/attribution-integration.yaml) для Android.

{% endcut %}

## 2023 {#year-2023}

{% cut "Ноябрь — март 2023" %}

#### Ноябрь, 2023 {#november-2023}

- Появились возможности [атрибуции установок по показам](../mobile-tracking/vta-tracking-specification.md).
- Data Stream API: в экспорт добавлены поля `session_id`, `installation_id`. Доступен новый тип данных — клики и показы.
- В отчетах стало доступно более точное определение географии на базе доступной части IP-адреса.
- Доступны новые [параметры](../mobile-tracking/tracking-specification.md) и [макросы](../mobile-tracking/postback-specification.md) для атрибуции по OAID: `{oaid}`, `{oaid_sha1}`, `{oaid_md5}`.
- Обновлена версия AppMetrica SDK Android [6.1.0](../sdk/android/changelog-android.md#s-6-1-0).

#### Октябрь, 2023 {#october-2023}

- Интерфейсные уведомления об изменения в метриках, доступно два типа: timespent на новых версиях приложения и изменение доли платящих пользователей.

#### Сентябрь, 2023 {#september-2023}

- [Data Stream API](../mobile-api/datastream/about.md): статистика теперь доступна в кабинете организации. Также появилась возможность подключить [оплату за превышение выбранной квоты](../mobile-api/datastream/limits.md).
- В [Post API](../mobile-api/post/about.md) появился ряд новых возможностей: передача inapp-покупок и подписок, рекламной выручки, ecommerce-событий, а также обновление свойств профилей.
- - Обновлена версия AppMetrica SDK Android до [6.0.0](../sdk/android/changelog-android.md#v-6-0-0). Обновлены идентификатор библиотеки, корневой пакет и API. Подробнее в [инструкции по миграции](../sdk/android/analytics/migration-io-6-0-0.md).

#### Август, 2023 {#august-2023}

- Запущены эксперименты [Varioqub](../common/varioqub-app-about.md) — возможность А/Б тестирования и удаленного управление конфигурацией приложения. SDK доступен на iOS и Android.
- Обновлен кабинет организации: появилась возможность гибкой настройки тарифа под необходимые фичи. Можно подключить [воркспейсы](../mobile-reports/workspaces.md) (включая сохраненные отчеты), расширенный план [экспериментов](../common/varioqub-app-about.md) и [Data Stream API](../mobile-api/datastream/about.md).

#### Июль, 2023 {#july-2023}

- Обновлена версия Push SDK Android до [2.3.1](../sdk/android/changelog-android.md#v-2-3-1).
- Обновлен кабинет организации: появилась статистка по подпискам и возможность переноса приложений между организациями.
- Включено [лимитирование кастомных событий](../troubleshooting/limit-events.md) с соответствии с выбранным тарифом.
- В [Data Stream API](../mobile-api/datastream/about.md) добавлены новые параметры: `device_latitude`, `device_longitude`.
- В [воркспейсах](../mobile-reports/workspaces.md) доступны кастомные виджеты когортного и retention-анализа.
- [Подписки](../data-collection/about-subscription.md): теперь на различные события подписок можно настроить постбэки.

#### Июнь, 2023 {#june-2023}

- Обновлена версия Flutter SDK до [1.3.0](../sdk/flutter/changelog.md#v-1-3-0).
- Обновлена версия Flutter Push SDK до [0.3.0](../sdk/flutter/changelog.md#v-push-0-3-0).
- Доступен [кабинет организации](../troubleshooting/troubleshooting.md#value-events): в нем можно увидеть общую статистику, расширить лимиты на кастомные события и подключить дополнительные опции.
- В кабинете организации доступно управление сотрудниками и удобное управление доступами к приложениям организации.
- В расширенных тарифах доступны [воркспейсы](../mobile-reports/workspaces.md) и [сохранение отчетов](../mobile-reports/save-reports.md).

#### Май, 2023 {#may-2023}

- Для бета-тестирования открыта возможность отслеживания статуса и дохода от in-app подписок, которые оформлены в Google Play и App Store. {% if tld == "ru" %}Подробнее об [использовании](../data-collection/about-subscription.md), настройке для [Google Play](../data-collection/subscription-android.md) и [App Store](../data-collection/subscription-ios.md). {% endif %}
- Обновлена версия AppMetrica SDK iOS до [4.5.2](../sdk/ios/changelog-ios.md#v-4-5-2).

#### Апрель, 2023 {#april-2023}

- Обновлена версия крэш-плагина до [0.8.2](../sdk/android/changelog-android.md#c-0-8-2).

#### Март, 2023 {#march-2023}

- Обновлена версия AppMetrica SDK Android [5.3.0](../sdk/android/changelog-android.md#s-5-3-0).
- Обновлена версия AppMetrica SDK iOS до [4.5.0](../sdk/ios/changelog-ios.md#v-4-5-0).

{% endcut %}

## 2022 {#2022}

{% cut "Октябрь — февраль 2022" %}

#### Октябрь, 2022 {#october-2022}

- Обновлена версия Unity SDK до [5.2.0](../sdk/unity/changelog.md#v-5-2-0). Поддержан API AdRevenue.
- В интерфейсе добавлен [дашборд](../mobile-reports/dashboard.md) с ключевыми метриками приложения.
- В [Smart Link](../mobile-tracking/add-tracker.md) добавлена поддержка редиректов в AppGallery и GetApps.
- Обновлена версия Flutter SDK до [1.1.0](../sdk/flutter/changelog.md#v-1-1-0). Поддержан API AdRevenue.

#### Сентябрь, 2022 {#september-2022}

- Обновлена версия Unity SDK до [5.0.1](../sdk/unity/changelog.md#v-5-0-1).
- Обновлена версия AppMetrica SDK Android [5.2.0](../sdk/android/changelog-android.md#s-5-2-0).
- Обновлена версия AppMetrica SDK iOS до [4.4.0](../sdk/ios/changelog-ios.md#v-4-4-0).
- Добавлены новые метрики для отслеживания доходов от рекламной монетизации в отчете [Revenue](../mobile-reports/revenue-report.md).

#### Август, 2022 {#august-2022}

- Обновлена версия AppMetrica Push Unity до [1.1.0](../sdk/unity/changelog.md#p-1-1-0).
- Обновлена версия плагина AppMetrica Push Flutter до [0.2.0](../sdk/flutter/changelog.md#v-push-0-2-0).

#### Июль, 2022 {#july-2022}

- Обновлена версия Push SDK iOS до [1.3.0](../sdk/ios/changelog-ios.md#v-push-1-3-0).
- Обновлена версия Unity SDK до [5.0.0](../sdk/unity/changelog.md#v-5-0-0).
- Обновлена версия Flutter SDK до [1.0.1](../sdk/flutter/changelog.md#v-1-0-1).
- Обновлена версия крэш-плагина до [0.6.2](../sdk/android/changelog-android.md#c-0-6-2).
- Обновлена версия AppMetrica SDK Android [5.0.1](../sdk/android/changelog-android.md#s-5-0-1).

#### Июнь, 2022 {#june-2022}

- Обновлена версия Push SDK Android до [2.2.0](../sdk/android/changelog-android.md#v-2-2-0).

#### Май, 2022 {#may-2022}

{% note info %}

Начиная с версии AppMetrica Android SDK 5.0.0 и выше при переустановке приложения на смартфоне меняется `appmetrica_device_id`. Это обусловлено новыми политиками Google. Подробности в [документации](../troubleshooting/troubleshooting.md#change-device-id).

{% endnote %}

- Обновлена версия AppMetrica SDK Android [5.0.0](../sdk/android/changelog-android.md#s-5-0-0).
- Обновлена версия Unity SDK до [4.3.0](../sdk/unity/changelog.md#v-4-3-0).
- Обновлена версия крэш-плагина до [0.6.1](../sdk/android/changelog-android.md#c-0-6-1).
- Обновлена версия AppMetrica Push Unity до [1.0.0](../sdk/unity/changelog.md#p-1-0-0).

#### Апрель, 2022 {#april-2022}

Обновился отчет [События](../mobile-reports/events-report.md):

- Появился конструктор группировок и метрик;
- Добавлены новые показатели для анализа параметров событий (сумма, среднее, медиана, уникальные значения);
- Обновился фильтр по типу сессий. Теперь по умолчанию в отчете отображаются события из всех сессий. Раньше фоновые сессии учитывались только в показателях по устройствам.

#### Март, 2022 {#march-2022}

- Отчет [In-app и Ad Revenue](../mobile-reports/revenue-report.md) - Обновлен на конструктор: появилась возможность сочетать разные группировки и выводить несколько метрик на график одновременно.
- События, отправленные с помощью [Post API](../mobile-api/post/about.md), теперь отображаются в [карточке профиля](../mobile-reports/profile-list.md#profile-card).
- Обновлена версия Push SDK Android до [2.1.1](../sdk/android/changelog-android.md#v-2-1-1).

#### Февраль, 2022 {#february-2022}

- Обновлена версия AppMetrica SDK Android до [4.2.0](../sdk/android/changelog-android.md#s-4-2-0).
- Обновлена версия AppMetrica SDK iOS до [4.2.0](../sdk/ios/changelog-ios.md#v-4-2-0).
- Обновлена версия Unity SDK до [4.2.0](../sdk/unity/changelog.md#v-4-2-0).
- Обновлена версия Push SDK Android до [2.1.0](../sdk/android/changelog-android.md#v-2-1-0).
- Опубликован Flutter SDK [0.1.0](../sdk/flutter/changelog.md#v-0-1-0).

{% endcut %}

## 2021 {#2021}

{% cut "Декабрь — апрель 2021" %}

#### Декабрь, 2021 {#december-2021}

- Обновлена версия Unity SDK до [4.0.0](../sdk/unity/changelog.md#v-4-0-0).
- Обновлена версия AppMetrica SDK Android до [4.1.1](../sdk/android/changelog-android.md#s-4-1-1).
- Обновлена версия Unity SDK до [4.1.0](../sdk/unity/changelog.md#v-4-1-0).
- Добавлен отчет [Вовлеченность](../mobile-reports/engagement-report.md).

#### Ноябрь, 2021 {#november-2021}

- Добавлен [трекинг](../mobile-tracking/facebook-tracking.md) Facebook* (Сервис, запрещенный на территории РФ) для Android через Google Play Install Referrer.
- В отчеты [Когортный анализ](../mobile-reports/cohort-report.md) и [Retention-анализ](../mobile-reports/retention-report.md) добавлены группировки по географии, полу, возрасту, операционной системе и версии приложения.
- В отчет [Когортный анализ](../mobile-reports/cohort-report.md) добавлены новые метрики: ARPU, количество покупок и количество платящих пользователей.
- Для сегментации добавлены новые параметры для inapp покупок: дата покупки, продукт, сумма, валюта, статус валидации, география и payload.
- Добавлена возможность отправлять [неатрибуцированные постбеки](../mobile-tracking/postback-quota.md).
- Добавлена возможность прикреплять [изображения в Push-уведомление для iOS](../mobile-api/push/file-type.md) через интерфейс AppMetrica.

#### Октябрь, 2021 {#october-2021}

- Обновлена версия Push SDK Android до [2.0.0](../sdk/android/changelog-android.md#v-2-0-0).
- В отчет [Воронки](../mobile-reports/funnels-report.md) добавлены события: установка, старт сессии, открытие deeplink, inapp покупки, push-уведомления, ecommerce события, крэши и ошибки.
- В отчете [Воронки](../mobile-reports/funnels-report.md) добавлена возможность указать окно воронки между первым и последним событием.
- В инструменте [Экспорт данных](../mobile-api/logs/about.md#export-data) добавлено поле выгрузки `profile_id`.

#### Сентябрь, 2021 {#september-2021}

- Добавлено [управление Conversion Value](../mobile-tracking/conversion-value.md).
- Добавлен автоматический сбор данных о [in-app покупках](../data-collection/about-revenue.md) и [открытии deeplink](../data-collection/deeplinks.md) с версией SDK 4.0.
- Обновлена версия Push SDK iOS до [1.1.1](../sdk/ios/changelog-ios.md#v-push-1-1-1).

#### Август, 2021 {#august-2021}

- Добавлены {% if locale == "ru" %}[email-уведомления](https://appmetrica.yandex.ru/blog/ru-email-notifications-about-app-errors-and-crashes){% endif %}{% if locale == "en" %}[email-уведомления](https://appmetrica.yandex.com/about/blog/en-email-notifications-about-app-errors-and-crashes){% endif %} о новых крешах и ошибках в приложении.
- Добавлен [экспорт данных](../common/cloud.md) в Yandex Cloud.
- Добавлена возможность отправлять [push-уведомления с прикрепленными файлами](../sdk/ios/push/ios-push-download-file.md) на iOS.
- Добавлены постбеки на события in-app покупок и новые [дополнительные параметры](../mobile-tracking/postback-specification.md#macros) с информацией про покупки.

#### Июль, 2021 {#july-2021}

- Добавлена [инструкция](../sdk/flutter/index.md) по подключению аналитической функциональности AppMetrica в приложения на Flutter.
- Добавлена возможность создавать и редактировать свои воронки пользователям, с правами доступа «Чтение».
- Добавлен отчет [User Acquisition по SKAdNetwork](../mobile-reports/user-acquisition-skadnetwork.md).
- Устранена возможная причина отклонения публикации приложения в Google Play из-за Implicit PendingIntent (Push SDK, Android 1.12.0).
- Появилась возможность добавлять тестовое устройство для пушей по IDFV и `appmetrica-device_id`.
- Обновлены версии Push SDK (iOS 0.9.2 и 1.0.0, Android 1.13.0).

#### Июнь, 2021 {#june-2021}

- Обновлены версии AppMetrica SDK до iOS 3.16.0/Android 3.21.1 для Unity (Unity 3.8.0).
- Добавлен метод `RequestTrackingAuthorization` для запроса IDFA на iOS (Unity 3.8.0).
- Группировка по периоду в таблице отчетов: UA, Remarketing, Анализ покупок.
- Добавлена поддержка gradle 7 (AppMetrica Build Plugin 0.3.0).
- Добавлена поддержка M1 (AppMetrica SDK, iOS 3.17.0).

#### Май, 2021 {#may-2021}

- Добавлен трекинг [Apple Search Ads](../mobile-tracking/searchads-settings.md) на iOS 14.5+ (AppMetrica SDK, iOS 3.15.1).
- Добавлен метод initWebViewReporting для отправки событий из JS-кода WebView (AppMetrica SDK, iOS 3.16/Android 3.21).
- Поддержан AGP 4.2, исправлены ошибки и повышена стабильность (AppMetrica Build Plugin 0.2.4).

#### Апрель, 2021 {#april-2021}

- Добавлен трекинг через SKAdNetwork (AppMetrica SDK, iOS 3.15).
- Добавлена возможность задавать идентификатор пользовательского профиля во время активации (`YandexMetricaConfig.Builder#withUserProfileID`) или до активации (`YandexMetrica#setUserProfileID`) (AppMetrica SDK, Android 3.20.1).
- Исправлена некорректная обработка deeplink (AppMetrica SDK, Android 3.20.1).

{% endcut %}
