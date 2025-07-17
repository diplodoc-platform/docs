# Редактирование доступа

Изменяет ранее выданные права доступа.

## Формат запроса {#request-format}

```
PUT {{ api-url }}/management/v1/application/{id}/grant
```
#|
|| `id` | Идентификатор приложения. ||
|#

### Тело запроса {#request-body}

```json translate=no
{
  "grant": {
    "user_login": "string",
    "perm": "string",
    "partners": [ int, int ],
    "event_labels": ["string", "string"]
  }
}
```
#|
|| `user_login` | Адрес электронной почты на Яндексе (логин) пользователя, которому предоставляется доступ. ||
|| `perm` | Уровень доступа.

Возможные значения:

- `view` — права на чтение;
- `edit` — права на чтение/редактирование;
- `agency_view` — права на чтение для агентства;
- `agency_edit` — права на чтение/редактирование для агентства.

Подробнее об уровнях доступа см. в разделе [{#T}](../../../../common/access.md).
||
|| `partners` | Идентификаторы рекламных партнеров, для которых предоставляется доступ. Чтобы получить список всех партнеров, воспользуйтесь методом [{#T}](list-partners.md).

Обязательное поле при выдаче доступов `agency_view` и `agency_edit`.

{% note info %}

Если выдается агентский уровень доступа, необходимо указать хотя бы один идентификатор рекламного партнера.

{% endnote %}

||
|| `event_labels` | Целевые события, по которым агентства смогут просматривать статистику.

Дополнительное поле при выдаче доступов `agency_view` и `agency_edit`.

||
|#

## Формат ответа {#response-body}

```json translate=no
{
  "grant" : {
    "user_login" : "string",
    "user_uid" : int,
    "perm" : "string",
    "comment" : "string",
    "partners" : [ int, int ],
    "event_labels" : [ "string", "string" ]
  }
```
#|
|| `user_login` | Адрес электронной почты на Яндексе (логин) пользователя, которому предоставляется доступ. ||
|| `user_uid` | Идентификатор пользователя, которому предоставляется доступ. ||
|| `perm` | Уровень доступа.

Возможные значения:

- `view` — права на чтение;
- `edit` — права на чтение/редактирование;
- `agency_view` — права на чтение для агентства;
- `agency_edit` — права на чтение/редактирование для агентства.

Подробнее о уровнях доступа в разделе [Управление доступом](../../../../common/access.md). ||
|| `comment` | Комментарий. ||
|| `partners` | Идентификаторы рекламных партнеров, для которых предоставляется доступ. Чтобы получить список всех партнеров, воспользуйтесь методом [{#T}](list-partners.md). ||
|| `event_labels` | Целевые события, по которым агентства смогут просматривать статистику. ||
|#

## Пример {#example}

{% list tabs %}

- cURL

  ```bash translate=no
  curl -X PUT \
    '{{ api-url }}/management/v1/application/1111/grant' \
    -H 'Content-Type: application/json' \
    -H 'Authorization: OAuth <your_token>' \
    -d '{
    "grant": {
      "user_login": "user_login",
      "perm": "agency_view",
      "partners": [ 145375, 148711 ],
      "event_labels": ["Оформление покупки", "Переход в корзину"]
    }
  }'
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../../../intro/authorization.md#get-oauth-token).

- HTTP

  ```http translate=no
  PUT /management/v1/application/1111/grant HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Content-Type: application/json
  Authorization: OAuth <your_token>

  {
    "grant": {
      "user_login": "user_login",
      "perm": "agency_view",
      "partners": [ 145375, 148711 ],
      "event_labels": ["Оформление покупки", "Переход в корзину"]
    }
  } 
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../../../intro/authorization.md#get-oauth-token).

{% endlist %}

{{ feedback }}

<a href="../../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../../_includes/feedback-button.md) %}

