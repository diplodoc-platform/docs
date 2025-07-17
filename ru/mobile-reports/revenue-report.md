# In-app и Ad Revenue

Отчет **In-app и Ad Revenue** отображает основные метрики, которые связаны с доходами вашего приложения от in-app покупок или рекламной монетизации.

Чтобы собирать статистику по выручке, настройте отправку в приложении. Подробнее в разделе [{#T}](../data-collection/about-revenue.md#send-revenue).

## Задачи, которые поможет решить отчет {#resolve-tasks}

- оценить успешность введения новых возможностей с помощью метрики [ARPU](*ARPU);
- оценить реакцию пользователей на изменение цен с помощью метрики [ARPPU](*ARPPU);
- оценить популярные продукты в приложении;
- оценить географию покупок с помощью группировки по городам;
- оценить доходность отдельных рекламных сетей и блоков.

## Общие настройки {#how-to}

Выберите период времени и сегмент аудитории. По умолчанию отчет показывает данные за неделю с группировкой по дням. Время в отчете — начало сессии на устройстве пользователя, приведенное к часовому поясу, который указан в настройках приложения.

{% note info "" %}

{% include notitle [period](_includes/period.md) %}

{% endnote %}

{% include notitle [segments](_includes/segments.md) %}

В отчете можно настроить [группировки](#group) и [метрики](#metrics).

## Настройка графика с выбором метрик {#metrics-in-graph}

{% include notitle [metrics-in-graph](_includes/metrics-in-graph.md) %}

## Выбор группировок и метрик {#groups-metrics}

{% include notitle [groups-metrics](_includes/groups-metrics.md) %}

### Группировки {#group}

{% include notitle [audience-group](_includes/audience-group.md) %}

{% include notitle [geo-group](_includes/geo-group.md) %}

{% include notitle [total-revenue-group](_includes/total-revenue-group.md) %}

{% include notitle [in-app-revenue-group](_includes/in-app-revenue-group.md) %}

{% include notitle [ad-revenue-group](_includes/ad-revenue-group.md) %}

{% include notitle [param-events-group](_includes/param-events-group.md) %}

{% include notitle [date-event-group](_includes/date-event-group.md) %}

{% include notitle [app-group](_includes/app-group.md) %}

{% include notitle [profile-attributes](_includes/profile-attributes.md) %}

Для группировок по **региону**, **стране** и **payload** доступен подробный режим отображения таблицы (drilldown). Для переключения воспользуйтесь кнопкой ![](../../_images/tab-flat-tree.png =60x).

### Метрики {#measure}

{% include notitle [total-revenue-metrics](_includes/total-revenue-metrics.md) %} 

{% include notitle [in-app-revenue-metrics](_includes/in-app-revenue-metrics.md) %} 

{% include notitle [in-app-purchase-metrics](_includes/in-app-purchase-metrics.md) %} 

{% include notitle [ad-revenue-metrics](_includes/ad-revenue-metrics.md) %} 

{% include notitle [event-params-metrics](_includes/event-params-metrics.md) %} 

{% note info "Учет валидированного Revenue" %}

При включенной валидации все метрики In-App Revenue cчитаются по валидированным покупкам и покупкам, отправленным без параметров для валидации. По невалидным покупкам считаются метрики **Невалидная выручка** и **Пользователи с невалидной выручкой**.

{% endnote %}

В интерфейсе отчета также отображается следующее:

- Цветовое отображение показателей на графике. Позволяет включить и выключить отображение показателя на графике.
    
     {% note info "" %}
    
     Элемент не доступен при группировке по дате.
    
     {% endnote %}
    
- Выбор режима отображения таблицы ![](../../_images/tab-flat-tree.png =60x)

<!-- ![](../../_images/revenue-report-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 800px;"} -->

## Экспорт данных {#export}

{% include notitle [export-api](_includes/export-api.md) %}

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*ARPU]: {{ arpu }}

[*ARPPU]: {{ arppu }}
