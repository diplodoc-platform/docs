# Атрибуция ремаркетинг-кампаний

AppMetrica позволяет атрибутировать [ремаркетинг-кампании](*ремаркетинг-кампании). Вы можете использовать ремаркетинг-кампанию для повторного привлечения аудитории, например, чтобы вернуть пользователей в приложение и совершить целевое действие.

AppMetrica атрибутирует возврат пользователей в приложение ([re-engagement](*re-engagement)) и новые установки, если приложение не было установлено ранее. Показатели re-engagement попадают в отчет [Remarketing](../mobile-reports/remarketing-report.md), новых установок — в отчет [User Acquisition](../mobile-reports/user-acquisition-report.md).

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-tracking/remarketing-attribution.png)

AppMetrica сохраняет историю атрибуции: данные об источнике установки не будут перезаписаны. Таким образом, после ремаркетинг-кампании у пользователя есть два источника: источник установки и источник re-engagement. При создании ремаркетинг-трекера есть возможность отключить отправку CPA-постбеков инсталл-партнерам.

Для атрибуции ремаркетинг-кампаний необходимо подготовить приложение и создать ремаркетинг-трекер. Подробнее в разделе [Как создать ремаркетинг-кампанию в AppMetrica](../troubleshooting/troubleshooting.md#remarketing-campaign).

## Узнать больше {#learn-more}

- [Как создать ремаркетинг-трекер](add-remarketing-tracker.md)
- [Отчет Remarketing](../mobile-reports/remarketing-report.md)
- [Структура и параметры трекинг-ссылки](tracking-specification.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*ремаркетинг-кампании]: Рекламная кампания, которая направлена на возвращение пользователей в установленное приложение. Подробнее о создании ремаркетинг-кампании в разделе [Создание ремаркетинг-трекера](add-remarketing-tracker.md).

[*re-engagement]: {{ re-engagement }}.
