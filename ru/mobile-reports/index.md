# Отчеты

[Веб-интерфейс AppMetrica](http://appmetrika.yandex.{{ domain }}/) позволяет просматривать статистику использования мобильного приложения. Для сбора статистики необходимо [подключить AppMetrica SDK в приложении](../common/quick-start.md).

Чтобы перейти к статистике, в меню выберите **{{ reports }}** и нажмите на нужный отчет. 

Отчеты разделены по группам в соответствии с тематикой. Кроме тематических групп есть сводные:

- **{{ all-reports }}** — алфавитный список отчетов.
- **{{ saved }}** — отчеты, [сохраненные](save-reports.md) вами и другими пользователями. Рядом с отчетом отображается аватар пользователя, который его сохранил. При наведении указателя мыши на аватар отображается логин пользователя.
- **{{ popular }}** — отчеты, которые вы просматриваете чаще всего. Для каждого пользователя формируется свой список популярных отчетов. В начале работы, пока персональный список еще не сформирован, отображается набор отчетов по умолчанию.

{% note info "" %}

Если у вас есть идеи или пожелания, как улучшить отчет, напишите нам. Форма обратной связи доступна из любого отчета — нажмите значок ![](../../_images/icon-feedback.svg) в правом верхнем углу страницы отчета.

{% endnote %}

Данные, которые отображены в отчетах, можно экспортировать с помощью [API отчетов](../mobile-api/api_v1/intro.md). API-запрос можно скопировать из интерфейса отчета, например, [отчета по аудитории](audience-report.md).

Отчеты в AppMetrica:

- Маркетинг

  - [User Acquisition](user-acquisition-report.md)
  - [User Acquisition SKAdNetwork](user-acquisition-skadnetwork.md)
  - [Ремаркетинг](remarketing-report.md)
  - [Push-кампании](push-campaign.md)
  - [Конверсии](conversions-report.md)

- Продукт

  - [События](events-report.md)
  - [Воронки](funnels-report.md)
  - [Retention-анализ](retention-report.md)
  - [Когортный анализ](cohort-report.md)  
  - [Вовлеченность](engagement-report.md)
  - [Аудитория](audience-report.md)
  - [Профили](profile-report.md)
  - [Список профилей](profile-list.md)  

- Монетизация

  - [In-app и Ad Revenue](revenue-report.md)
  - [Ecommerce](ecommerce-report.md)

- Технологии

  - Версии приложения
  - Операционные системы
  - Производители
  - Модели устройств
  - Тип устройства
  - Язык интерфейса
  - Экраны
  - Root-статус
  - Версии SDK
  - KitVersion
  - Операторы
  - Тип соединения

- Крэши и ошибки

  - [Крэши](crashes-and-errors.md)
  - [Ошибки](crashes-and-errors.md)  
  - [ANRs](anr.md)  

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
