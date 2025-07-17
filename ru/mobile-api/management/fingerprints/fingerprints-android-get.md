# Информация об отпечатках сертификатов приложения

{{ fingerptints-get }}

## Формат запроса {#request-format}

```
GET {{ api-url }}/management/v1/application/{id}/events_certs_fingerprints/android
```

#|
|| `id` | Идентификатор приложения. ||
|#

## Формат ответа {#output-structure}

```json translate=no
{
    "data": {
        "fingerprints": [
            {
                "id": int,
                "fingerprint": string
            }
        ]
    }
}
```

#|
|| `data` | {{ response-status }} ||
|| `data.fingerprints` | {{ fingerprints }} ||
|| `data.fingerprints.id` | {{ fingerprints-id }} ||
|| `data.fingerprints.fingerprint` | {{ fingerprint }} ||
|#

## Пример {#example}

Запрос:

```bash translate=no
curl -X GET '{{ api-url }}/management/v1/application/8888/events_certs_fingerprints/android' \
-H 'Authorization: OAuth oauth_token'
```

Ответ:

```json translate=no
{
    "data": {
        "fingerprints": [
            {
                "id": 4,
                "fingerprint": "A7:89:E5:05:C8:17:A1:22:EA:XXXXXX"
            }
        ]
    }
}

```

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
