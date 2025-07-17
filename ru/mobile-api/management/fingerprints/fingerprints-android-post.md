# Загрузка отпечатка сертификата приложения

{{ fingerptints-post }}

## Формат запроса {#request-format}

```
POST {{ api-url }}/management/v1/application/{id}/events_certs_fingerprints/android/add
```

#|
|| `id` | Идентификатор приложения. ||
|#

### Формат тела запроса {#structure-in}

```json translate=no
{
    "data": {
        "fingerprint": string
    }
}
```

#|
|| `data` | Объект с данными. ||
|| `data.fingerprint` | {{ fingerprint }} ||
|#

## Формат ответа {#output-structure}

```json translate=no
{
  "id": int,
  "fingerprint": string
}
```

#|
|| `id` | {{ fingerprints-id }} ||
|| `fingerprint` | {{ fingerprint }} ||
|#

## Пример {#example}

Запрос:
```bash translate=no
curl -X POST '{{ api-url }}/management/v1/application/1111/events_certs_fingerprints/android/add' \
-H 'Content-Type: application/json' \
-H 'Authorization: OAuth oauth_token' \
-d '{
      "data": {
        "fingerprint": "A7:89:E5:05:C8:17:A1:XXXXX"
      }
    }'
```

Ответ:

```json translate=no
{
  "id": 24,
  "fingerprint": "A7:89:E5:05:C8:17:A1:XXXXX"
}
```

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
