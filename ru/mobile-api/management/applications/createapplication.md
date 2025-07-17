# Добавление приложения

Добавляет приложение в AppMetrica.

## Формат запроса {#request-format}

```
POST {{ api-url }}/management/v1/applications
```

### Тело запроса {#request-body}

```json translate=no
{
  "application": {
    "name": "string",
    "category": int,
    "time_zone_name": "string",
    "hide_address": bool,
    "gdpr_agreement_accepted": bool
  }
}
```

#|
|| `name` | Название приложения. ||
|| `category` | Идентификатор категории приложения.

Чтобы получить список всех категорий, воспользуйтесь методом [Список категорий](get-categories.md). ||
|| `time_zone_name` | Часовой пояс для расчета статистики. ||
|| `hide_address` | Статус запрета на сохранение полных IP-адресов пользователей из ЕС.

Возможные значения:
- `true` — запрет включен.
- `false` — запрет выключен. ||
|| `gdpr_agreement_accepted` | Статус принятия [Договора об обработке данных](https://yandex.ru/legal/metrica_agreement/).

Возможные значения:
- `true` — договор принят.
- `false` — договор отклонен. ||
|#

## Формат ответа {#response-body}

```json translate=no
{
  "application": {
    "name": "string",
    "time_zone_name": "string",
    "hide_address": bool,
    "gdpr_agreement_accepted": bool,
    "category": int,
    "use_universal_links": bool,
    "id": int,
    "uid": int,
    "owner_login": "string",
    "api_key128": "string",
    "import_token": "string",
    "permission": "string",
    "time_zone_offset": int,
    "create_date": "YYYY-MM-DD"
  }
}
```

#|
|| `name` | Название приложения. ||
|| `time_zone_name` | Часовой пояс для расчета статистики. ||
|| `hide_address` | Статус запрета на сохранение полных IP-адресов пользователей из ЕС.

Возможные значения:
- `true` — запрет включен.
- `false` — запрет выключен. ||
|| `gdpr_agreement_accepted` | Статус принятия [Договора об обработке данных](https://yandex.ru/legal/metrica_agreement/).

Возможные значения:
- `true` — договор принят.
- `false` — договор отклонен. ||
|| `category` | Идентификатор категории приложения.

Чтобы получить список всех категорий воспользуйтесь методом [Список категорий](get-categories.md). ||
|| `use_universal_links` | Статус использования Universal Link.

Возможные значения:
- `true` — использование Universal Link включено.
- `false` — использование Universal Link выключено. ||
|| `id` | Идентификатор приложения. ||
|| `uid` | Идентификатор пользователя, который добавил приложение. ||
|| `owner_login` | Логин владельца приложения. ||
|| `api_key128` | API key. ||
|| `import_token` | Post API key. ||
|| `permission` | Права доступа.

Возможные значения:

- `view` — права на чтение;
- `edit` — права на чтение/редактирование;
- `agency_view` — права на чтение для агентства;
- `agency_edit` — права на чтение/редактирование для агентства;
- `own` — владелец приложения;

Подробнее о правах доступа в разделе [Управление доступом](../../../common/access.md). ||
|| `time_zone_offset` | Смещение часового пояса относительно UTC в секундах. ||
|| `create_date` | Дата добавления приложения. ||
|#

## Пример {#example}

{% list tabs %}

- cURL

  ```bash translate=no
  curl -X POST \
    '{{ api-url }}/management/v1/applications' \
    -H 'Content-Type: application/json' \
    -H 'Authorization: OAuth <your_token>' \
    -d '{
      "application": {
          "name": "string",
          "category": 85,
          "time_zone_name": "Asia/Yekaterinburg",
          "hide_address": true,
          "gdpr_agreement_accepted": true
      }
  }'
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../../intro/authorization.md#get-oauth-token).

- HTTP

  ```http translate=no
  POST /management/v1/applications HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Content-Type: application/json
  Authorization: OAuth <your_token>
  
  {
    "application": {
      "name": "string",
      "category": 85,
      "time_zone_name": "Asia/Yekaterinburg",
      "hide_address": true,
      "gdpr_agreement_accepted": true
    }
  }
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../../intro/authorization.md#get-oauth-token).

{% endlist %}

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
