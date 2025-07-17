# Описание ошибок

Данный раздел содержит список кодов ошибок, возвращаемых методами API управления.

## Формат ошибок {#errors_description}

```javascript translate=no
{
    "errors" : [ {
        "error_type" : error_type ,
        "message" : string ,
        "location" : string 
    }, ... ],
    "code" : int ,
    "message" : string 
}
```

#|
|| **Параметры** | **Описание** ||
|| `errors` | Список возникших ошибок. ||
|| `code` | HTTP-статус. ||
|| `message` | Причина. ||
|| `errors.error_type` | Тип ошибки. ||
|| `errors.message` | Причина ошибки. ||
|| `errors.location` | Место возникновения ошибки. ||
|#

## Коды ошибок

| Код ошибки | Описание |
| ----- | ----- |
| backend_error (503) | Ошибка сервера. |
| invalid_parameter (400) | Неверно задан параметр. |
| not_found (404) | Указанный объект не найден. |
| missing_parameter (400) | Не указан необходимый параметр. |
| access_denied (403) | Доступ запрещен. |
| unauthorized (401) | Неавторизованный пользователь. |
| quota (429) | Превышен лимит количества запросов к API. |
| query_error (400) | Запрос слишком сложный. |
| conflict (409) | Нарушение целостности данных. |
| invalid_json (400) | Переданный JSON имеет неверный формат. |

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
