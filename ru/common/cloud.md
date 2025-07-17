---
noIndex: true

content: noindex
name: robots
---

# Экспорт данных в Yandex Cloud

{% note alert %}

Подключение экспорта временно не поддерживается для новых пользователей.

{% endnote %}

Если вы пользуетесь [Yandex Cloud](https://cloud.yandex.ru/) и сервисом [Managed Service for ClickHouse](https://cloud.yandex.ru/services/managed-clickhouse), вы можете экспортировать данные из AppMetrica в ваш кластер. Их вы можете использовать, например, для построения собственных отчетов в [Yandex DataLens](https://cloud.yandex.ru/services/datalens).

Данные можно экспортировать в реальном времени — экспорт происходит регулярно.

Ниже описаны этапы настройки экспорта:

## Шаг 1. Проверьте настройки кластера ClickHouse {#check-zookeeper}

1. Убедитесь, что ваш кластер ClickHouse из 2 и более хостов. Это необходимо, чтобы реализовать [репликацию](https://cloud.yandex.ru/docs/managed-clickhouse/concepts/replication).
    Если кластер из одного хоста, добавьте один или несколько хостов.

2. Убедитесь, что в настройках кластера включена опция **Доступ из Метрики и AppMetrica**.
3. _(Опционально)_ Чтобы отчеты можно было строить в Yandex DataLens, убедитесь, что в настройках кластера включена опция **Доступ из DataLens**.

{% note info %}

Опция **Управление пользователями через SQL** в настоящий момент недоступна.

{% endnote %}

## Шаг 2. Создайте сервисный аккаунт и авторизованный ключ {#create-service-account}

1. В консоли Yandex Cloud создайте сервисный аккаунт. При создании выберите роль **editor**.
    
   Подробнее в разделе [Создание сервисного аккаунта](https://cloud.yandex.ru/docs/iam/operations/sa/create) Помощи Yandex Cloud.
    
2. Создайте авторизованный ключ. После создания сохраните секретную часть ключа, например, в текстовый файл. Она нужна, чтобы привязать сервисный аккаунт в AppMetrica.
    
   Подробнее в разделе [Создание авторизованного ключа](https://cloud.yandex.ru/docs/iam/operations/authorized-key/create) Помощи Yandex Cloud.

## Шаг 3. Запустите экспорт {#create-an-export}

{% note alert %}

При запущенном экспорте нельзя менять конфигурацию кластера. Чтобы изменить конфигурацию, остановите все запущенные экспорты, измените конфигурацию и запустите экспорт заново.

{% endnote %}

1. В интерфейсе AppMetrica нажмите **{{data-export}}** → **{{upload-cloud}}**.
2. На странице **Экспорты данных в Yandex Cloud** нажмите кнопку **Запустить новый экспорт**.
3. Привяжите сервисный аккаунт Yandex Cloud. Для этого в поле **Сервисный аккаунт** нажмите кнопку **Создать новый**. В появившемся окне укажите:

    {% cut "Название" %}

    Укажите название.

    {% endcut %}

    {% cut "Идентификатор сервисного аккаунта" %}

    1. В Яндекс Облаке откройте ваш каталог.
    2. Из левого меню перейдите на страницу **Сервисные аккаунты**.
    3. Нажмите на созданный сервисный аккаунт, например, **appmetrica**.
    4. В блоке **Обзор** скопируйте значение поля **Идентификатор**.

    ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/cloud_service-account.png){style="border: solid 1px #cccccc; max-width: 800px;"}

    {% endcut %}

    {% cut "Идентификатор открытого ключа" %}

    5. В Яндекс Облаке откройте ваш каталог.
    6. Из левого меню перейдите на страницу **Сервисные аккаунты**.
    7. Нажмите на созданный сервисный аккаунт, например, **appmetrica**.
    8. В блоке **Авторизованные ключи** скопируйте значение поля **Идентификатор**.

    ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/cloud_open-account.png){style="border: solid 1px #cccccc; max-width: 800px;"}

    {% endcut %}

    {% cut "Закрытый ключ" %}

    Ключ, который вы сохранили при создании авторизованного ключа.
    
    {% endcut %}
    
    {% cut "Идентификатор каталога" %}
    
    9. В Яндекс Облаке откройте консоль.
    10. Скопируйте идентификатор вашего каталога.

    ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/ru/images/common/cloud_console.png){style="border: solid 1px #cccccc; max-width: 800px;"}
    
    {% endcut %}
    
    Затем нажмите **Создать**.
    
4. Выберите интервал дат для экспорта. Если включена опция **В реальном времени**, экспорт происходит регулярно.
5. В поле **Параметры событий** выберите параметры для экспорта.
    
    Подробнее о параметрах событий в разделе [Доступные точки запроса](../mobile-api/logs/endpoints.md#events) Logs API.
    
6. В поле **Кластер** выберите кластер для экспорта. В нем будет создана таблица с экспортируемыми параметрами.
7. Нажмите кнопку **Запустить экспорт**.

{% note info %}

Если вы хотите создать [MaterializedView](https://clickhouse.tech/docs/en/engines/table-engines/special/materializedview/) на базе экспортированной таблицы, перед созданием MaterializedView выполните следующее:

1. Запустите экспорт в кластер. Это создаст пользователя `appmetrica_export_user` с некоторыми правами.
2. В интерфейсе Яндекс Облака перейдите на страницу каталога и выберите сервис **Managed Service for ClickHouse**.
3. Нажмите на имя нужного кластера и выберите вкладку **Пользователи**.
4. Выдайте пользователю `appmetrica_export_user` права на запись в базу данных, в которой планируете создать MaterializedView. Иначе экспорт будет приостановлен.

{% endnote %}

## Возможные проблемы и их решение {#troubleshooting}

{% cut "Ошибка "FAILED_PRECONDITION: operation not permitted when SQL user management is enabled"." %}

В настоящий момент опция **Управление пользователями через SQL** недоступна. Отключите опцию и перезапустите экспорт.

{% endcut %}

## Узнать больше {#learn-more}

- [События](../mobile-reports/events-report.md)
- [Logs API](../mobile-api/logs/about.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
