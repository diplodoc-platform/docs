# Список приложений

Возвращает информацию о приложениях, доступных пользователю.

## Формат запроса {#request-format}

```
GET {{ api-url }}/management/v1/applications
```

## Формат ответа {#response-body}

```json translate=no
{
  "applications": [
    {
      "name": "string",
      "time_zone_name": "string",
      "hide_address": bool,
      "gdpr_agreement_accepted": bool,
      "category": int,
      "bundle_id": "string",
      "team_id": "string",
      "use_universal_links": bool,
      "universal_link": "string",
      "id": int,
      "uid": int,
      "owner_login": "string",
      "api_key128": "string",
      "import_token": "string",
      "permission": "string",
      "time_zone_offset": int,
      "permission_date": "YYYY-MM-DDThh:mm:ss±hh:mm",
      "create_date": "YYYY-MM-DD"
    },
    ...
  ]
}
```

#|
|| `name` | Название приложения. ||
|| `time_zone_name` | Часовой пояс для расчета статистики. ||
|| `label_id` | Идентификатор папки, в которой находится приложение в веб-интерфейсе. ||
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
|| `bundle_id` | Bundle ID. ||
|| `team_id` | App Prefix или Team ID. ||
|| `use_universal_links` | Статус использования Universal Link.

Возможные значения:
- `true` — использование Universal Link включено.
- `false` — использование Universal Link выключено. ||
|| `universal_link` | Universal Link. ||
|| `id` | Идентификатор приложения. ||
|| `uid` | Идентификатор пользователя, который добавил приложение. ||
|| `owner_login` | Логин владельца приложения. ||
|| `api_key128` | API key. ||
|| `import_token` | Post API key. ||
|| `permission` | Права доступа.

Возможные значения:

- view — права на чтение;
- edit — права на чтение/редактирование;
- agency_view — права на чтение для агентства;
- agency_edit — права на чтение/редактирование для агентства;
- own — владелец приложения;

Подробнее о правах доступа в разделе [Управление доступом](../../../common/access.md). ||
|| `label` | Название папки, в которой находится приложение в веб-интерфейсе. ||
|| `time_zone_offset` | Смещение часового пояса относительно UTC в секундах. ||
|| `permission_date` | Дата выдачи доступа.

Для владельца совпадает с датой добавления приложения. ||
|| `create_date` | Дата добавления приложения. ||
|#

## Пример {#example}

{% list tabs %}

- cURL

  ```bash translate=no
  curl -X GET \
    '{{ api-url }}/management/v1/applications' \
    -H 'Authorization: OAuth <your_token>'
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../../intro/authorization.md#get-oauth-token).

- HTTP

  ```http translate=no
  GET /management/v1/applications HTTP/1.1
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
