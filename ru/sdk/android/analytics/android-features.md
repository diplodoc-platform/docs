# Особенности библиотеки AppMetrica

Библиотека AppMetrica состоит из двух частей: клиентской и сервисной. При этом в них есть особенности, которые необходимо учитывать при инициализации:

- Клиентская часть — обеспечивает предварительную валидацию данных и передачу их сервисной части. Экземпляр клиентской части создается для каждого процесса в приложении.

- Сервисная часть — отвечает за хранение и отправку данных на сервер. Запускается в основном процессе приложения. Поэтому отчет о крэше сразу сохраняется в файл и отправляется при следующем запуске.

## Рекомендации по инициализации {#recommendations}

- Если в приложении есть несколько процессов, где вы хотите использовать AppMetrica, инициализируйте библиотеку с одинаковой конфигурацией для каждого процесса. Иначе конфигурация может зависеть от того, какой из процессов запустится раньше.

   {% note info "" %}

   Для отправки данных можно использовать репортеры. Их можно инициализировать с разной конфигурацией. Подробнее в разделе [Отправка статистики на дополнительный API key](android-operations.md#reporter-different-apikey).

   {% endnote %}

- Инициализируйте библиотеку AppMetrica в методе [Application.onCreate()](https://developer.android.com/reference/android/app/Application.html#onCreate%28%29). Так библиотека будет инициализирована в каждом процессе.

- Учитывайте, что экземпляр [ContentProvider](https://developer.android.com/intl/ru/reference/android/content/ContentProvider.html) создается до экземпляра [Application](https://developer.android.com/intl/ru/reference/android/app/Application.html). Если вы инициализируете библиотеку в методе `Application.onCreate()`, отправить данные из метода `ContentProvider.onCreate()` не получится.

- Не добавляйте в метод `Application.onCreate()` код, который не должен выполняться больше одного раза. Такой код выполняйте при создании других компонентов или вынесите в отдельный [Service](https://developer.android.com/intl/ru/reference/android/app/Service.html).

- Избегайте длительных операций в методе `Application.onCreate()` и не инициализируйте в нем другие библиотеки. Время выполнения этого метода напрямую влияет на скорость запуска первого `Activity`, `Service` или `Receiver`.

## Узнайте больше {#learn-more}

<!-- - [Пример интеграции библиотеки ССЫЛКА НУЖНА](ССЫЛКА) -->
- [Как включить отправку данных о местоположении пользователей?](../../../troubleshooting/troubleshooting.md#region)
- [Как проверить, что у меня установлены последние версии Android-библиотек?](../../../troubleshooting/troubleshooting.md#newest-android-version)
- [Почему в отчетах не отображаются новые установки?](../../../troubleshooting/troubleshooting.md#no-installs)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
