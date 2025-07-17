# Список категорий

Возвращает список всех категорий приложений.

## Формат запроса {#request-format}

```
GET {{ api-url }}/management/v1/metadata/application/categories
  ? [lang=<locale>]
```

#|
|| `lang` | Язык возвращаемого результата.

Возможные значения:
- ru — возвращает результат на русском языке;
- en — возвращает результат на английском языке. ||
|#

## Формат ответа {#response-body}

```json translate=no
{
  "data": [
    {
      "id": int,
      "name": "string",
      "type": "string"
    },
    ...
  ]
}
```
#|
|| `data` | Объект, содержащий информацию о категориях. ||
|| `data.id` | Идентификатор категории. ||
|| `data.name` | Название категории.

Чтобы получить название категории на английском, добавьте в запрос параметр `lang=en`. ||
|| `data.type` | Тип категории.

Возможные значения:
- game — категория относится к типу игр.
- common — категория относится к общему типу. ||
|#

## Пример {#example}

{% list tabs %}

- cURL

  ```bash translate=no
  curl -X GET \
    '{{ api-url }}/management/v1/metadata/application/categories?lang=en' \
    -H 'Authorization: OAuth <your_token>'
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../../intro/authorization.md#get-oauth-token).
  

- HTTP

  ```http translate=no
  GET /management/v1/metadata/application/categories?lang=en HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Authorization: OAuth <your_token>
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../../intro/authorization.md#get-oauth-token).
  

{% endlist %}

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
