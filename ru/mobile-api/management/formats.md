# Форматы входных данных и результата

## Формат входных данных {#input}

Входные структуры данных POST- и PUT-методов передаются в теле запроса. Входные структуры совпадают с выходными структурами GET-методов соответствующих ресурсов.

{% note info %}

Чтобы корректно сформировать входную структуру для POST- или PUT-метода, вызовите GET-метод для уже существующего ресурса. Скопируйте полученную структуру и задайте нужные значения полей.

{% endnote %}

POST- и PUT-методы API принимают входные данные в формате JSON.

Формат входных данных указывается в HTTP-заголовке `Content-Type`.

Возможные значения заголовка: `application/x-yametrika+json` или `application/json`.

## Формат результата {#result}

API управления возвращает ответы в кодировке UTF-8. Ответы имеют формат JSON.

Например, в результате выполнения следующего запроса будет получена информация о приложении с идентификатором 1111:

```no-highlight translate=no
GET /management/v1/application/1111 HTTP/1.1
Host: api.appmetrica.yandex.ru
Authorization: OAuth <your_token>
```

где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../intro/authorization.md#get-oauth-token).

Пример ответа:

```no-highlight translate=no
{
    "application": {
        "name": "Examples api.yandex.ru",
        "time_zone_name": "Europe/Moscow",
        "hide_address": false,
        "gdpr_agreement_accepted": false,
        "use_universal_links": false,
        "id": 1111,
        "uid": 178121744,
        "owner_login": "login",
        "time_zone_offset": 10800,
        "create_date": "2016-01-02"
    }
}
```

Для удобства отладки результат может отображаться в отформатированном виде. Для этого в запросе любого типа передайте параметр `pretty` со значением равным `1`:

```no-highlight translate=no
GET /management/v1/application/1111?pretty=1 HTTP/1.1
Host: api.appmetrica.yandex.ru
Authorization: OAuth <your_token>
```

где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../intro/authorization.md#get-oauth-token).

При успешном выполнении DELETE-методов API возвращает HTTP-статус с кодом `200`. Если HTTP-статус содержит другой код, удаление не выполнено.

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
