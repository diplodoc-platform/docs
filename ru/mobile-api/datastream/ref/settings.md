# Получение настроек

{{ get-settings }}

## Формат запроса {#request-format}

```
GET {{ api-url}}/management/v1/application/{id}/datastream/settings
```

#|
|| `id` | Идентификатор приложения. ||
|#

## Формат ответа {#output-structure}

```json translate=no
{
    "settings": {
        "ui_checkbox_enabled": boolean,
        "export_fields": [
            {
                "data_type": string,
                "enabled": boolean,
                "export_format": string,
                "fields": ["profile_id", "os_name", "event_name", "event_timestamp", ... ],
                "include_events": ["Useful Event 1", "Useful Event 2", ... ],
                "exclude_events": ["Ignored Event 1", "Ignored Event 2", ... ],
                "event_attribution": string
            },
            ...
        ]
    }
}
```

#|
|| `settings` | {{ response-status }} ||
|| `settings.ui_checkbox_enabled` | Признак включения работы всего Data Stream для приложения. ||
|| `settings.export_fields` | Список объектов-настроек экспорта. Один объект настроек соответствует одному типу выгружаемых данных. ||
|| `settings.export_fields[i].data_type` | {{ response-data_type }} ||
|| `settings.export_fields[i].enabled` | Признак включения экспорта для указанного типа данных. ||
|| `settings.export_fields[i].export_format` | {{ response-export_format }} ||
|| `settings.export_fields[i].fields` | {{ response-export_fields }} ||
|| `settings.export_fields[i].include_events` | {{ response-include_events }} ||
|| `settings.export_fields[i].exclude_events` | {{ response-exclude_events }} ||
|| `settings.export_fields[i].event_attribution` | {{ response-event_attribution }} ||
|#

## Пример {#example}

Запрос:

```bash translate=no
curl -X GET '{{ api-url }}/management/v1/application/1111/datastream/settings' \
-H 'Authorization: OAuth oauth_token'
```

Ответ:

```json translate=no
{
    "settings": {
        "ui_checkbox_enabled": true,
        "export_fields": [
            {
                "data_type": "installation",
                "enabled": true,
                "export_format": "csv",
                "fields": ["publisher_name", "publisher_id", "tracker_name", "tracking_id", "click_timestamp"],
                "include_events": [],
                "exclude_events": []
            },
            {
                "data_type": "event",
                "enabled": true,
                "export_format": "csv",
                "fields": ["profile_id", "os_name", "event_name", "event_timestamp"],
                "include_events": ["Useful Event 1", "Useful Event 2"],
                "exclude_events": ["Ignored Event 1", "Ignored Event 2"]
            },
            {
                "data_type": "attributed_event",
                "enabled": true,
                "export_format": "csv",
                "fields": ["attributed_event_type", "event_name", "conversion_id", "conversion_name"],
                "include_events": ["Useful Event 1", "Useful Event 2"],
                "exclude_events": ["Ignored Event 1", "Ignored Event 2"],
                "event_attribution": "last_appmetrica"
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
