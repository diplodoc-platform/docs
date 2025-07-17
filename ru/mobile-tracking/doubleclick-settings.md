# Трекинг кампаний DoubleClick

AppMetrica отслеживает рекламные кампании DoubleClick с помощью [DoubleClick Floodlight](https://support.google.com/dcm/partner/answer/2823388).

{% note info %}

Данная статья рассчитана на пользователей, которые знакомы с рекламной сетью DoubleClick и ее настройками.

{% endnote %}

Ниже описаны этапы настройки трекинга кампаний, запущенных на платформе DoubleClick.

## Шаг 1. Создайте трекер {#step1}

[Создайте трекер](add-tracker.md) в интерфейсе AppMetrica.

При создании обратите внимание на следующие поля:

1. В разделе **Описание кампании** выберите **DoubleClick** в качестве партнера.
2. В появившемся разделе **DoubleClick**, заполните доступные поля:

   ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-tracking/doubleclick-settings.png){style="border: solid 1px #cccccc; max-width: 800px;"}

    - **src** — идентификатор рекламодателя. Если вы используете **DoubleClick Bid Manager**, возьмите значение `src` из настроек тега Floodlight. Значение можно найти в параметрах рекламного пикселя.
    - **type** — идентификатор группы действий, с которой связана активность в Floodlight.
    - **token** — строка, специфичная для рекламодателя. Передается при каждом запросе к серверу **DoubleClick Bid Manager**.
    - **cat** — тег, используемый серверами Floodlight.

## Шаг 2. Сохраните трекер {#step2}

Сохраните настроенный трекер. Он будет доступен в разделе **Трекеры**.

## См. также

- [Общая информация о Floodlight](https://support.google.com/dcm/partner/answer/2823388)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
