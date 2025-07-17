# Архивирование группы

Помещает группу в архив.

Отчеты по архивированной группе остаются доступными.

## Формат запроса

```
DELETE {{ push-api-url }}/push/v1/management/group/{groupId}
```

#|
|| `groupId` | {{ push-get-id }} ||
|#

## Пример запроса {#example}

{% list tabs %}

- cURL

  ```bash translate=no
  curl -X DELETE \
    https://push.api.appmetrica.yandex.net/push/v1/management/group/XXXXXX \
    -H 'Authorization: OAuth <your_token>'
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../intro/authorization.md#get-oauth-token).

- HTTP

  ```http translate=no
  DELETE /push/v1/management/group/XXXXXX HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Authorization: OAuth <your_token>
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../intro/authorization.md#get-oauth-token).

{% endlist %}

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
