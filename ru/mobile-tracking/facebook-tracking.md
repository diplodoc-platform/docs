# Трекинг кампаний Facebook^*^ для Android

AppMetrica отслеживает рекламные кампании Facebook[*](*stop) на Android через [Google Play Install Referrer](technology.md).

Для отслеживания необходимо указать **Install Referrer Decryption Key** (уникальный ключ дешифровки Facebook для расшифровки данных по атрибуции) в настройках трекера для партнера Facebook[*](*stop). Для всех рекламных кампаний одного приложения достаточно создать один трекер. Он будет отслеживать все установки через Install Referrer.

Ниже описаны этапы настройки трекера для отслеживания рекламных кампаний Facebook[*](*stop):

## Шаг 1. Получите Install Referrer Decryption Key {#step1}

1. Войдите в аккаунт [Facebook for Developers](https://developers.facebook.com/), для которого есть доступ к отслеживаемому приложению.
2. Перейдите в раздел [Мои приложения](https://developers.facebook.com/apps/) и выберите приложение, для которого необходимо настроить отслеживание.
3. Для выбранного приложения перейдите в раздел {% if locale == 'ru' %}**Настройки** → **Основные**{% endif %}{% if locale == 'en' %}**Settings** → **Basic**{% endif %}.
4. Внизу страницы, в секции с Android приложением, скопируйте **Install Referrer Decryption Key**.

## Шаг 2. Создайте трекер в AppMetrica {#step2}

[Создайте трекер](add-tracker.md) в интерфейсе AppMetrica. При создании обратите внимание на следующие поля:

1. В разделе **Описание кампании** в поле **Партнер** выберите Facebook[*](*stop).
2. В разделе **Настройка целевой ссылки** по умолчанию выбран способ отслеживания **Instal Referrer**, — это наиболее точный способ отслеживания. Не рекомендуется изменять указанный способ.
3. В разделе **Настройка целевой ссылки** в поле **Install Referrer Decryption Key** добавьте ключ, полученный в кабинете Facebook for Developers.

\* Сервис, запрещенный на территории РФ.

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*stop]: \* Сервис, запрещенный на территории РФ.
