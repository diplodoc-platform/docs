# Удаление приложения

Удаляет указанное приложение.

## Формат запроса {#request}

```
DELETE {{ api-url }}/management/v1/application/{id}
```

#|
|| `id` | Идентификатор приложения. ||
|#

## Пример запроса {#example}

{% list tabs %}

- cURL

  ```bash translate=no
  curl -X DELETE \
    '{{ api-url }}/management/v1/application/1111' \
    -H 'Authorization: OAuth <your_token>'
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../../intro/authorization.md#get-oauth-token).

- HTTP

  ```http translate=no
  DELETE /management/v1/application/1111 HTTP/1.1
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
