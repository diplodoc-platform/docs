# Удаление отпечатка сертификата приложения

{{ fingerptints-delete }}

## Формат запроса {#request-format}

```
DELETE {{ api-url }}/management/v1/application/{id}/events_certs_fingerprints/android/{fingerprint_id}
```

#|
|| `id` | Идентификатор приложения. ||
|| `fingerprint_id` | Идентификатор отпечатка сертификата. Список идентификаторов можно получить с помощью операции [Информация об отпечатках сертификатов приложения](fingerprints-android-get.md). ||
|#

## Формат ответа {#output-structure}

```json translate=no
{
    "success": boolean
}
```

#|
|| `success` |  Статус операции. ||
|#

## Пример {#example}

Запрос:

```bash translate=no
curl -X DELETE '{{ api-url }}/management/v1/application/8888/events_certs_fingerprints/android/24' \
-H 'Authorization: OAuth oauth_token'
```

Ответ:

```json translate=no
{
    "success": true
}
```

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
