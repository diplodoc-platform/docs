# Трекинг кампаний Petal Ads

AppMetrica отслеживает рекламные кампании Petal Ads.

Для отслеживания необходимо связать аккаунты AppMetrica и Petal Ads через идентификатор связи — `Petal Ads Link ID`, по которому происходит атрибуция источника установки.

Ниже описаны этапы настройки для работы с рекламными кампаниями Petal Ads:

## Шаг 1. Получите Petal Ads Link ID {#get-link-id}

1. Откройте интерфейс Petal Ads и перейдите в раздел {% if locale == 'ru' %}**Инструменты** → **События и объекты**{% endif %}{% if locale == 'en' %}**Tools** → **Events and assets**{% endif %}.
2. На странице {% if locale == 'ru' %}**События и объекты**{% endif %}{% if locale == 'en' %}**Events and assets**{% endif %} нажмите {% if locale == 'ru' %}**+Добавление объекта**{% endif %}{% if locale == 'en' %}**+Add asset**{% endif %}.
3. Выберите тип объекта {% if locale == 'ru' %}**Приложение (Для приложений Android)**{% endif %}{% if locale == 'en' %}**App (Applicable to Android apps)**{% endif %} и нажмите {% if locale == 'ru' %}**Далее**{% endif %}{% if locale == 'en' %}**Next**{% endif %}.
4. Выберите приложение из списка, в строке {% if locale == 'ru' %}**Инструмент анализа**{% endif %}{% if locale == 'en' %}**Analytics tool**{% endif %} выберите **AppMetrica** и нажмите {% if locale == 'ru' %}**Отправить**{% endif %}{% if locale == 'en' %}**Submit**{% endif %}.
5. На странице {% if locale == 'ru' %}**События и объекты**{% endif %}{% if locale == 'en' %}**Events and assets**{% endif %} появится добавленный объект и его **Link ID**. Этот **Link ID** используется для создания трекера.

   ![](../../_images/link-id-petal-ads-{{ locale }}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

6. В правой части экрана нажмите кнопку {% if locale == 'ru' %}**+Добавление события**{% endif %}{% if locale == 'en' %}**+Add event**{% endif %}.

   {% note info %}

   Если у вас выбрано {% if locale == 'ru' %}**Умное отслеживание**{% endif %}{% if locale == 'en' %}**Smart tracking**{% endif %}, добавлять событие не нужно.

   Если у вас не выбрано {% if locale == 'ru' %}**Умное отслеживание**{% endif %}{% if locale == 'en' %}**Smart tracking**{% endif %}, каждое событие нужно импортировать на стороне рекламной сети. Для этого нажмите кнопку {% if locale == 'ru' %}**+Добавление события**{% endif %}{% if locale == 'en' %}**+Add event**{% endif %} и выберите событие, соответствующее заданному постбеку.

   {% endnote %}

7. Укажите тип события — {% if locale == 'ru' %}**Активация**{% endif %}{% if locale == 'en' %}**Activation**{% endif %}, источник данных — {% if locale == 'ru' %}**Отслеживание инструментов анализа**{% endif %}{% if locale == 'en' %}**Analytics tool tracking**{% endif %} и нажмите **OK**.

## Шаг 2. Создайте трекер в AppMetrica {#create-tracker}

1. В разделе **Описание кампании** в поле **Партнер** выберите Petal Ads.
2. В появившемся разделе укажите **Petal Ads Link ID**, который был получен в [шаге 1](#get-link-id).
3. _(Опционально)_ Для отслеживания конверсий в интерфейсе Petal Ads, настройте отправку целевых событий в разделе **Настройка постбеков** в AppMetrica. Подробнее о настройке [постбеков](add-tracker.md#step5).

   {% note alert %}

   Для Petal Ads не нужно настраивать **Install postback**.

   {% endnote %}

4. Для партнера Petal Ads добавлены шаблоны постбеков и можно выбрать необходимые.

   ![](../../_images/petal-ads-postback-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
