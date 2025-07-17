# Состояние потока

{{ status }}

## Формат запроса {#request-format}

```
GET {{ api-url }}/datastream/v1/application/{id}/status
```

#|
|| `id` | Идентификатор приложения. ||
|#

## Формат ответа {#output-structure}

```json translate=no
{
    "status": {
        "streams": [
            {
                "data_type": string,
                "stream_windows": [
                    {
                        "stream_window_timestamp": int,
                        "export_schema_id": int,
                        "payload_bytes": int,
                        "event_count": int,
                        "update_timestamp": int
                    },
                    ...
                ]
            },
            ...
        ],
        "export_fields": [
            {
                "export_schema_id": int,
                "field_names": [
                    "event_datetime",
                    "event_json",
                    "event_name",
                    "event_timestamp",
                    "session_id",
                    "installation_id",
                    "appmetrica_device_id",
                    "city",
                    "connection_type",
                    "country_iso_code",
                    ...
                ]
            },
            ...
        ]
    }
}
```

#|
|| `status` | {{ response-status }} ||
|| `status.streams` | {{ response-streams }} ||
|| `status.streams[i].data_type` | {{ response-data_type }} ||
|| `status.streams[i].stream_windows` | {{ response-stream_windows }} ||
|| `status.streams[i].stream_windows[j].stream_window_timestamp` | {{ response-stream_window_timestamp }} ||
|| `status.streams[i].stream_windows[j].export_schema_id` | {{ response-export_schema_id }} ||
|| `status.streams[i].stream_windows[j].payload_bytes` | {{ response-payload_bytes }} ||
|| `status.streams[i].stream_windows[j].event_count` | {{ response-event_count }} ||
|| `status.streams[i].stream_windows[j].update_timestamp` | {{ response-update_timestamp }} ||
|| `status.export_fields` | {{ response-export_fields }} ||
|| `status.export_fields[i].export_schema_id` | {{ response-export_schema_id }} ||
|| `status.export_fields[i].field_names` | {{ response-field_names }} Подробнее о полях в статье [Типы данных для экспорта](../data-type-fields.md). ||
|#

## Пример {#example}

Запрос:

```bash translate=no
curl -X GET '{{ api-url }}/datastream/v1/application/1111/status' \
-H 'Authorization: OAuth oauth_token'
```

Ответ:

```json translate=no
{
    "status": {
        "streams": [
            {
                "data_type": string,
                "stream_windows": [
                    {
                        "stream_window_timestamp": int,
                        "export_schema_id": int,
                        "payload_bytes": int,
                        "event_count": int,
                        "update_timestamp": int
                    },
                    ...
                ]
            },
            ...
        ],
        "export_fields": [
            {
                "export_schema_id": int,
                "field_names": [
                    "event_datetime",
                    "event_json",
                    "event_name",
                    "event_timestamp",
                    "session_id",
                    "installation_id",
                    "appmetrica_device_id",
                    "city",
                    "connection_type",
                    "country_iso_code",
                    ...
                ]
            },
            ...
        ]
    }
}
```

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
