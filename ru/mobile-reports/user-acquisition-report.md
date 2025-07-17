# User Acquisition

Отчет User Acquisition содержит информацию об источниках установки приложения. В отчете можно выбрать определенных пользователей с помощью [сегментирования](segmentation.md).

## Период отчета {#period}

Отчёт User Acquisition считается когортно: при выборе периода отчёта вы выбираете установки за этот период, а метрики по этим пользователям рассчитываются за всё время их жизни в приложении.

{% include [period](_includes/period.md) %}

## Группировки и метрики {#groups-annd-metrics}

{% include [groups-metrics](_includes/groups-metrics-old.md) %}

### Группировки {#group}

{% cut "Источники" %}

- **Партнеры**.
- **Трекеры**.
- **Параметр**.
- **Все параметры**.
- **App Installer**.
- **Реатрибуция**. Возможные группировки: [новые установки](*новые установки), [реатрибуции](*реатрибуции) и [не определено](*не_определено).
- **Тип атрибуции**. Возможные значения: Органика / Клик / Показ / Предустановка / Deeplink.
- **Оценка фрода**. 

{% endcut %}

{% include notitle [audience-group](_includes/audience-group.md) %}

{% include notitle [geo-group](_includes/geo-group.md) %}

{% include notitle [date-install-group](_includes/date-install-group.md) %}

{% include notitle [app-group](_includes/app-group.md) %}

{% cut "Атрибуты профиля" %}

{% include notitle [profile-attributes-system](_includes/profile-attributes-system.md) %} 

{% include notitle [profile-custom-group](_includes/profile-custom-group.md) %} 

{% endcut %}

### Метрики {#measure}

{% cut "Основные показатели" %}

- **Клики**. Количество кликов, которые совершили пользователи.
- **Установки**. Общее число устройств с установленным приложением. Чтобы разбить метрику по типам установки (новые, реатрибутированные), используйте группировку **Тип установки**.
- **Показы**. Количество показов.
- **Конверсия клика в установку**
- **CTIT**. Среднее расстояние между кликом/показом (смотря по чему атрибутировались) и установкой.
- **CTR**. Конверсия из показа в клик.
- **IPM**. Количество установок на 1000 показов.
- **Конверсия показа в установку**.
- **Deeplinks**. Число открытий приложения по deeplink.

{% endcut %}

{% include notitle [conversion-metrics](_includes/conversion-metrics.md) %} 

{% cut "Использование" %}

- **Сессии**.
- **Лояльные пользователи**.
- **Retention**.

{% endcut %}

{% cut "Метрики по событиям" %}

- **Cобытиz**.
- **Пользователи с событием**.
- **Событий на пользователя**.
- **Конверсия в достижение события пользователем**.

{% endcut %}

{% include notitle [total-revenue-metrics](_includes/total-revenue-metrics.md) %} 

{% include notitle [in-app-revenue-metrics](_includes/in-app-revenue-metrics.md) %} 

{% include notitle [in-app-purchase-metrics](_includes/in-app-purchase-metrics.md) %} 

{% include notitle [ad-revenue-metrics](_includes/ad-revenue-metrics.md) %} 

{% include notitle [ecommerce-metrics](_includes/ecommerce-metrics.md) %} 

<!-- ![](../../_images/user-acquisition-report-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 800px;"} -->

## Экспорт данных {#export}

{% include notitle [export](_includes/export-api.md) %}

## Частые вопросы {#faq}

{% include notitle [Описание](../_includes/faq.md#ua-events) %}

{% include notitle [Описание](../_includes/faq.md#ua-retention) %}

{% if locale == "ru" %}

## Узнать больше {#learn-more}

- [Обзор на 360°: обогатите аналитику в AppMetrica данными из трекеров](https://appmetrica.yandex.ru/about/blog/appmetrica-analytics-with-mmp-insights)

{% endif %}

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*новые установки]: {{ new-installs }}

[*реатрибуции]: Число устройств, установивших по трекеру с включенной реатрибуцией.

[*Клики]: Количество кликов, которые совершили пользователи.

[*Показы]: Количество показов.

[*CTIT]: Среднее расстояние между кликом/показом (смотря по чему атрибутировались) и установкой.

[*CTR]: Конверсия из показа в клик.

[*IPM]: Количество установок на 1000 показов.

[*Сессии]: Количество сессий пользователей за все время с момента установки.

[*Лояльные пользователи]: {{ loyal-users }}

[*Количество событий]: Общее число событий, которые произошли в приложении.

[*Количество пользователей с событием]: Число пользователей, в приложениях которых произошли события.

[*Конверсия в достижение события]: Доля пользователей с событием, среди пользователей, установивших приложение.

[*Покупки]: {{ purchases }}

[*Платящие пользователи]: {{ paying-users }}

[*Покупок на пользователя]: {{ purchases-per-user }}

[*% платящих пользователей]: {{ percent-per-paying-user }}

[*Невалидная выручка]: {{ invalid-revenue }}

[*Пользователи с невалидной выручкой]: {{ users-with-invalid-revenue }}

[*Выручка]: Доход приложения. Рассчитывается как сумма всех покупок.

[*Ad Revenue события]: {{ ad-revenue-events }}

[*Ad Revenue]: {{ ad-revenue-new }}

[*eCPM]: {{ ecpm }}

[*Пользователи с Ad Revenue]: {{ users-with-ad-revenue }}

[*Ad Revenue событий на пользователя]: {{ ad-revenue-events-per-user }}

[*Сессий с Ad Revenue]: {{ sessions-with-ad-revenue }}

[*Ad Revenue событий на сессию]: {{ ad-revenue-events-per-session }}

[*% пользователей с Ad Revenue]: {{ percent-users-with-ad-revenue }}

[*не_определено]: События, для которых нельзя применить понятие "тип установки". Например: клики.

[*Установки]: Общее число устройств с установленным приложением. Чтобы разбить метрику по типам установки (новые, реатрибутированные), используйте группировку **Тип установки**.

[*Событий на пользователя]: Среднее количество событий на одного пользователя. Рассчитывается как общее число событий, деленное на выбранный показатель (по умолчанию, "Все установки").

[*In-App Revenue]: {{ in-app-revenue }} {{ currency-conversion }}

[*Средний чек]: {{ average-order }} {{ currency-conversion }}

[*In-App ARPU]: {{ arpu }} {{ currency-conversion }}

[*In-App ARPPU]: {{ arppu }} {{ currency-conversion }}

[*Ad ARPU]: {{ ad-arpu }} {{ currency-conversion }}

[*Total Revenue]: {{ total-revenue}} {{ currency-conversion }}

[*Total APRU]: {{ total-arpu }} {{ currency-conversion }}

[*deeplink]: {{ deeplink }}

[*Retention]: Доля пользователей от числа установивших приложение за указанный день/неделю/месяц (нулевой период), вернувшихся в приложение (запустивших его) на определенный день/неделю/месяц после установки. Показатель рассчитывается как отношение числа пользователей, запустивших приложение на N-й день/неделю/месяц к числу пользователей, установивших приложение в нулевой период (это число принимается за 100%). Подробнее в отчете [Retention-анализ](retention-report.md).

[*Deeplinks]: Число открытий приложения по deeplink.

[*Тип атрибуции]: Тип атрибуции, принимает значения Органика / Клик / Показ / Предустановка / Deeplink.

[*Оценка фрода]: Ресурсы с вердиктами уровней `фрод` и `скорее фрод` по {% if tld == "ru" %}[оценке FraudScore](../common/fraud-score.md#assessment){% else %}оценке FraudScore{% endif %}.
