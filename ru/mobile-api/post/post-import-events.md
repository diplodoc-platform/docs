# Загрузка событий

Загружает информацию о событиях.

Пример использования: можно передавать в AppMetrica оффлайн события, если пользователь не заходит в приложение, чтобы его совершить. Например, событие полного восстановления энергии в игре или просмотр фильма на Smart TV.

Свойства событий можно передавать в параметрах запроса или в теле. При передаче данных в теле, к URL запроса необходимо добавить `.csv`. Подробнее в разделе [Пример запроса](#sample).

Для привязки события к пользователю, необходимо использовать одно из следующих полей при запросе:

- `profile_id`
- `appmetrica_device_id`

{% note alert %}

Post API содержит ограничения на загрузку данных. Подробнее в разделе [Ограничения](restrictions.md).

{% endnote %}

## Формат запроса

```
POST {{api-url }}/logs/v1/import/events
  ? post_api_key=<string>
  & application_id=<int>
  & profile_id=<string>
  & appmetrica_device_id=<int>
  & event_name=<string>
  & event_timestamp=<int>
  & [event_json=<json>]
  & [session_type=<string>]
  & [ios_ifa=<string>]
  & [ios_ifv=<string>]
  & [google_aid=<string>]
  & [windows_aid=<string>]
  & [os_name=<string>]
  & [os_version=<string>]
  & [device_manufacturer=<string>]
  & [device_model=<string>]
  & [device_type=<string>]
  & [device_locale=<string>]
  & [app_version_name=<string>]
  & [app_package_name=<string>]
  & [connection_type=<string>]
  & [operator_name=<string>]
  & [mcc=<int>]
  & [mnc=<int>]
  & [device_ipv6=<string>]
```

#|
|| `post_api_key`* | {{ post_api_key }} ||
|| `application_id`* | {{ application_id }} ||
|| `profile_id`* | {{ post-profile_id }}

{% note alert %}

Не передавайте значение вместе с параметром `appmetrica_device_id`. Сервер принимает только один из параметров.

{% endnote %}

||
|| `appmetrica_device_id`* | {{ post-appmetrica_device_id }}

{% note alert %}

Не передавайте значение вместе с параметром `profile_id`. Сервер принимает только один из параметров.

{% endnote %}

||
|| `event_name`* | {{ event_name }} ||
|| `event_timestamp`* | {{ event_timestamp }} ||
|| `event_json` | {{ event_json }} Параметры событий могут быть вложенными, например `{"param1":"param2","param1":{"param2":"param3"}}`. ||
|| `session_type` | Тип сессии. Возможные значения:

- `foreground` — в отчете [События](../../mobile-reports/events-report.md) будет увеличиваться метрика **Пользователи**.
- `background` — в отчете [События](../../mobile-reports/events-report.md) будет увеличиваться метрика **Устройства**. Такие события не будут попадать в отчет с группировкой по пользователям и в карточку профиля.

Значение по умолчанию: `background`. ||
|| `ios_ifa` | {{ ios_ifa }} ||
|| `ios_ifv` | {{ ios_ifv }} ||
|| `google_aid` | {{ google_aid }} ||
|| `windows_aid` | {{ windows_aid }} ||
|| `os_name` | {{ os_name }} ||
|| `os_version` | {{ os_version }} ||
|| `device_manufacturer` | {{ device_manufacturer }} ||
|| `device_model` | {{ device_model }} ||
|| `device_type` | {{ device_type }} ||
|| `device_locale` | {{ device_locale }} ||
|| `app_version_name` | {{ app_version_name }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `connection_type` | {{ connection_type }} ||
|| `operator_name` | {{ operator_name }} ||
|| `mcc` | {{ mcc }} ||
|| `mnc` | {{ mnc }} ||
|| `device_ipv6` | {{ device_ipv6 }} ||
|#

## Коды ответа

| Код | Описание |
| ----- | ----- |
| 200 | Данные успешно загружены. |
| 403 | Запрос не содержит заголовка авторизации, либо указан неверный токен. |
| 400 | Запрос не содержит одного или нескольких обязательных параметров. |

## Пример запроса {#sample}

{% list tabs %}

- Передача данных в теле запроса

  ```http translate=no
  POST /logs/v1/import/events.csv?post_api_key=0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ012 HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Content-Length: 540i
  Connection: close
  
  device_model,device_ipv6,device_type,google_aid,app_package_name,operator_name,mnc,application_id,event_json,profile_id,event_name,event_timestamp
  iPhone X,2a02:6b8::40c:6676:baff:fea6:53d8,phone,01234567-890a-bcde-f012-3456789abcde,com.yandex.sample.metrica,MegaFon,2,1111,"{""key"":""value_1""}",1234567890123456789,event_name_1,1234567890
  iPhone X,2a02:6b8::40c:6676:baff:fea6:53d9,phone,fedcba98-7654-3210-fedc-ba9876543210,com.yandex.sample.metrica,MegaFon,2,1111,"{""key"":""value_2""}",9876543210987654321,event_name_2,1234567891
  ```
  
- Передача данных в параметрах запроса

  ```http translate=no
  POST /logs/v1/import/events?post_api_key=0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ012&device_model=iPhone%20X&device_ipv6=2a02%3A6b8%3A%3A40c%3A6676%3Abaff%3Afea6%3A53d8&device_type=phone&google_aid=01234567-890a-bcde-f012-3456789abcde&app_package_name=com.yandex.sample.metrica&operator_name=MegaFon&mnc=2&application_id=1111&event_json=%7B%22key%22%3A%22value%22%7D&profile_id=1234567890123456789&event_name=event_name&event_timestamp=1234567890 HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Content-Length: 0
  Connection: close
  ```

{% endlist %}

## Другие методы Post API {#other-methods}

- [Загрузка событий In-app Revenue](post-revenue.md)
- [Загрузка событий Ad Revenue](post-adrevenue.md)
- [Загрузка событий Ecommerce](post-ecommerce.md)
- [Атрибуты профиля](post-profile-attributes.md)

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
