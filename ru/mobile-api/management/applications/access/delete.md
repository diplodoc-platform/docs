# Удаление доступа

Удаляет ранее выданные права доступа.

## Формат запроса {#request-format}

```
DELETE {{ api-url }}/management/v1/application/{id}/grant?user_login={login}
```
#|
|| `id` | Идентификатор приложения. ||
|| `login` | Адрес электронной почты на Яндексе (логин) пользователя.

{% note alert %}

Если параметр `user_login` не передавать, то удаляется доступ пользователя, выполняющего запрос, то есть отписка от приложения.

{% endnote %}

||
|#

## Пример {#example}

{% list tabs %}

- cURL

  ```bash translate=no
  curl -X DELETE \
    '{{ api-url }}/management/v1/application/1111/grant?user_login=user123' \
    -H 'Authorization: OAuth <your_token>'
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../../../intro/authorization.md#get-oauth-token).

- HTTP

  ```http translate=no
  GET /management/v1/application/1111/grant?user_login=user123' HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Authorization: OAuth <your_token>
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../../../intro/authorization.md#get-oauth-token).

{% endlist %}

{{ feedback }}

<a href="../../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../../_includes/feedback-button.md) %}
