# Вывод группы из архива

Выводит группу из архивированного состояния.

## Формат запроса

```
POST {{ push-api-url }}/push/v1/management/group/{groupId}/restore
```

#|
|| `groupId` | {{ push-get-id }} ||
|#

## Пример запроса {#example}

{% list tabs %}
 
- cURL
 
  ```bash translate=no
  curl -X POST \
    'https://push.api.appmetrica.yandex.net/push/v1/management/group/XXXXXX/restore' \
    -H 'Authorization: OAuth <your_token>'
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../intro/authorization.md#get-oauth-token).

- HTTP
   
  ```http translate=no
  GET /push/v1/management/group/XXXXXX/restore HTTP/1.1
  Host: push.api.appmetrica.yandex.net
  Authorization: OAuth <your_token>
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../intro/authorization.md#get-oauth-token).

{% endlist %}

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
