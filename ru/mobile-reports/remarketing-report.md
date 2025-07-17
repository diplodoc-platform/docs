# Remarketing

Отчет Remarketing содержит информацию о [ремаркетинг-кампаниях](*ремаркетинг-кампаниях), которые направлены на повторное привлечение аудитории. Для отслеживания ремаркетинг-кампаний существует специальный тип трекера. Подробнее в разделе [Создание ремаркетинг-трекера](../mobile-tracking/add-remarketing-tracker.md).

В отчете отображаются данные о возврате пользователей в приложение ([re-engagement](*re-engagement)), а также о совершенных ими целевых событиях. Re-engagement засчитывается при запуске приложения после перехода по трекинг-ссылке или re-engagement deeplink.

Отчет позволяет выбрать определенных пользователей с помощью [сегментирования](segmentation.md). 

Для отчета доступен только [пользовательский уровень](segmentation.md#users-segment) фильтров сегментации.

{% cut "Как выглядит отчет" %}

![](../../_images/remarketing-report-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

{% endcut %}

## Период отчета {#period}

Отчет строится за определенный период времени. По умолчанию задан недельный период.

{% include [period](_includes/period.md) %}

## Данные по deeplinks {#deeplinks}

Вы можете отображать в отчете данные по всем [deeplinks](*deeplink) или только по [re-engagement](*re-engagement) deeplinks. 

![](../../_images/remarketing-report-deeplinks-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

Обычный deeplink фиксирует метрики только в момент первого открытия. Re-engagement deeplink отслеживает действия пользователя в нескольких сессиях, пока другая кампания не сменит его статус. 

{% note info "" %}

Установки, полученные в результате ремаркетинг-кампании, доступны в отчете [User Acquisition](user-acquisition-report.md).

{% endnote %}

Выбор влияет на расчет метрик в блоке [Основные показатели](#main-metrics). Остальные метрики рассчитываются только для re-engagement deeplinks.

## Группировки {#group}

{% include notitle [origins-group](_includes/origins-group.md) %} 

{% include notitle [audience-group](_includes/audience-group.md) %}

{% include notitle [geo-group](_includes/geo-group.md) %}

{% include notitle [installs-group](_includes/installs-group.md) %}

{% include notitle [reengagement-group](_includes/reengagement-group.md) %} 

{% cut "Атрибуты профиля" %}

{% include notitle [profile-attributes-system](_includes/profile-attributes-system.md) %} 

{% include notitle [profile-custom-group](_includes/profile-custom-group.md) %} 

{% endcut %}

Отчет позволяет просмотреть список трекеров партнера при нажатии в отчете на название партнера (при группировке по партнеру). При группировке по трекеру по нажатию на название трекера откроется список всех параметров трекера.

## Метрики {#measure}

{% note info "" %}

Метрики из блока [Основные показатели](#main-metrics) рассчитываются в зависимости от переключателя [{#T}](#deeplinks).

Остальные метрики рассчитываются только для re-engagement deeplinks.

{% endnote %}

Для анализа доступны следующие показатели: 

{#main-metrics}

{% cut "Основные показатели" %} 

- **Клики**. Количество кликов, которые совершили пользователи по трекинговой ссылке или re-engagement deeplink.
- **Пользователи**. Количество пользователей, которые перешли по трекинговой ссылке или re-engagement deeplink.
- **Конверсия клика в deeplink**. 
- **Deeplinks**. 

{% endcut %}

{% include notitle [conversion-metrics](_includes/conversion-metrics.md) %} 

{% cut "Использование" %}

- **Сессии**. Количество сессий пользователей за все время с момента re-engagement.
- **Лояльные пользователи**. {{ loyal-users }}
- **Retention**. {{ retention }}

{% endcut %}

{% cut "Метрики по событиям" %}

- **Cобытия**. Общее число событий, которые произошли в приложении.
- **Пользователи с событием**. Число пользователей, в приложениях которых произошли события.
- **Событий на пользователя**. Отношение количества событий к сумме всех пользователей приложения.
- **Конверсия в достижение события пользователем**. 

{% endcut %}

{% include notitle [total-revenue-metrics](_includes/total-revenue-metrics.md) %} 

{% include notitle [in-app-revenue-metrics](_includes/in-app-revenue-metrics.md) %} 

{% include notitle [in-app-purchase-metrics](_includes/in-app-purchase-metrics.md) %} 

{% include notitle [ad-revenue-metrics](_includes/ad-revenue-metrics.md) %} 

{% include notitle [ecommerce-metrics](_includes/ecommerce-metrics.md) %} 

В интерфейсе отчета также доступно:

- Цветовое отображение показателей на графике. Вы можете включить и выключить отображение показателя на графике.
- Выбор источника данных для графика. Выберите показатель, который будет отображаться на графике: клики, re-engagements или конверсия.

## События {#events}

В отчет можно добавить до 5 событий, чтобы наблюдать информацию о событии в разрезе источника трафика. Отправка события должна быть настроена при [инициализации SDK](../common/quick-start.md).

Для показа информации по событию:

1. Выберите одну из метрик группы **Метрики по событиям**.

1. Нажмите на ссылку **Выберите значение** — откроется список настроенных событий.

1. Отметьте нужные события и нажмите **Применить**.

{% cut "Как добавить кастомные события" %}

![](../../_images/remarketing-events-{{locale}}.png)

{% endcut %}

## Экспорт данных {#export}

{% include notitle [export](_includes/export-api.md) %}

## См. также {#learn-more}

- [Как включить отправку данных о местоположении пользователей?](../troubleshooting/troubleshooting.md#region)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*ремаркетинг-кампаниях]: Рекламная кампания, которая направлена на возвращение пользователей в установленное приложение. Подробнее о создании ремаркетинг-кампании в разделе [Создание ремаркетинг-трекера](../mobile-tracking/add-remarketing-tracker.md).

[*deeplink]: {{ deeplink }}

[*re-engagement]: {{ re-engagement }}
