# Push-кампании

Отчет отображает статистическую информацию о проводимых push-кампаниях: количество отправленных, доставленных и открытых push-уведомлений.

{% include notitle [segments](_includes/segments.md) %}

Чтобы построить отчет, выберите период времени, сегмент аудитории и необходимую push‑кампанию.

## Период отчета {#period}

Отчет строится за определенный период времени. По умолчанию задан недельный период.

{% include [period](_includes/period.md) %}

## Группировки {#group}

{% cut "Push-кампании" %}

  - **Push-кампания**.
  - **Гипотеза**.
  - **Язык**.
  - **Тип ошибки отправки**.
  - **Транспорт**.
  - **Тип кампании**.
  - **Версия Push SDK**.

{% endcut %}  

{% include notitle [audience-group](_includes/audience-group.md) %}

{% include notitle [geo-group](_includes/geo-group.md) %}

{% include notitle [date-event-group](_includes/date-event-group.md) %}

{% include notitle [app-group](_includes/app-group.md) %}

{% include notitle [profile-attributes](_includes/profile-attributes.md) %}  

Чтобы развернуть отчет по кампании нажмите ![](../../_images/plus.png =30x) в списке названий.

## Метрики {#measure}

{% note alert %}

Если при создании push-кампании не настроено [AB-тестирование](../push/marketing.md#a-b-testing), то вся статистика относится к гипотезе A.

{% endnote %}

{% cut "Push-кампании" %}

- **Отправлено**. Количество отправленных push-уведомлений.
- **Доставлено**. Количество доставленных push-уведомлений. 

    По умолчанию для iOS-устройств push-уведомление считается доставленным, если оно было открыто. Чтобы отслеживать доставку, [настройте сбор статистики](../sdk/ios/push/ios-settings.md) push-уведомлений.

- **Открыто**. Количество открытых push-уведомлений.
- **Конверсия из доставлено в открыто**. Отношение числа доставленных push-уведомлений к открытым.
- **Контрольная выборка**.
- **Ошибка отправки**.
- **Показано (Android)**.
- **Пуши запрещены (Android)**.

{% endcut %}

<!-- ![](../../_images/push-report-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 800px;"} -->

## Экспорт данных {#export}

{% include notitle [export-api](_includes/export-api.md) %}

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*re-engagement]: {{ re-engagement }}
