# Загрузка событий Ad Revenue

Передает данные о выручке от показов рекламы.

Пример использования: вы можете передавать через Post API рекламный доход от просмотров рекламы с привязкой к к каждому пользователю приложения.

События покупок, полученные через Post API, используются в расчете всех метрик, также они доступны в воронках и когортах.

Свойства событий можно передавать в параметрах запроса или в теле. При передаче данных в теле, к URL запроса необходимо добавить `.csv`. Подробнее в разделе [Пример запроса](#sample).

Для привязки события к пользователю, необходимо использовать одно из следующих полей при запросе:

- `profile_id`
- `appmetrica_device_id`

{% note alert %}

Post API содержит ограничения на загрузку данных. Подробнее в разделе [Ограничения](restrictions.md).

{% endnote %}

## Формат запроса

```
POST {{ api-url }}/logs/v1/import/adrevenue
  ? post_api_key=<string>
  & application_id=<int>
  & profile_id=<string>
  & appmetrica_device_id=<int>
  & event_timestamp=<int>
  & revenue=<decimal>
  & currency=<enum>
  & ad_type=<enum>
  & [ad_network=<string>]
  & [ad_unit_id=<int>]
  & [ad_unit_name=<string>]
  & [ad_placement_id=<int>]
  & [ad_placement_name=<string>]
  & [precision=<enum>]
  & [payload=<string>]
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
|| `event_timestamp`* | {{ event_timestamp }} ||
|| `revenue`* | {{ post-revenue }} ||
|| `currency`* | {{ post-currency }} [Список доступных валют](../../data-collection/currency-codes.md). ||
|| `ad_type`* | {{ post-ad_type }} ||
|| `ad_network` | {{ post-ad_network }} ||
|| `ad_unit_id` | {{ post-ad_unit_id }} ||
|| `ad_unit_name` | {{ post-ad_unit_name }} ||
|| `ad_placement_id` | {{ post-ad_placement_id }} ||
|| `ad_placement_name` | {{ post-ad_placement_name }} ||
|| `precision` | {{ post-precision }} ||
|| `payload` | {{ post-payload }} ||
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
  POST /logs/v1/import/adrevenue.csv?post_api_key=0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ012 HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Content-Length: 540i
  Connection: close
  
  application_id,profile_id,appmetrica_device_id,event_timestamp,revenue,currency,ad_type,ad_network,ad_unit_id,ad_unit_name,ad_placement_id,ad_placement_name,precision,payload,session_type,ios_ifa,ios_ifv,google_aid,windows_aid,os_name,os_version,device_manufacturer,device_model,device_type,device_locale,app_version_name,app_package_name,connection_type,operator_name,mcc,mnc,device_ipv6
  1234567890,1234567890abcdef,1757762239877245682,1689943892,0.0001,usd,banner,some_network_name,0987654321,some_unit_name,12345000,some_placement_name,estimated,"{""key"":""value_1""}",foreground,123456abcde,54321edcba,098765abcde,567890abcde,ios,16.6,Apple,iPhone14Pro,phone,en_US,some_version_name,some_package_name,wifi,MegaFon,250,2,2a02:6b8::40c:6676:baff:fea6:53d8
  ```
  
- Передача данных в параметрах запроса
  
  ```http translate=no
  POST /logs/v1/import/adrevenue.csv?post_api_key=0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ012&application_id=1234567890&profile_id=1234567890abcdef&appmetrica_device_id=1757762239877245682&event_timestamp=1689943892&revenue=0.0001&currency=usd&ad_type=banner&ad_network=some_network_name&ad_unit_id=0987654321&ad_unit_name=some_unit_name&ad_placement_id=12345000&ad_placement_name=some_placement_name&precision=estimated&payload="{""key"":""value_1""}"&session_type=foreground&ios_ifa=123456abcde&ios_ifv=54321edcba&google_aid=098765abcde&windows_aid=567890abcde&os_name=ios&os_version=16.6&device_manufacturer=Apple&device_model=iPhone14Pro&device_type=phone&device_locale=en_US&app_version_name=some_version_name&app_package_name=some_package_name&connection_type=wifi&operator_name=MegaFon&mcc=250&mnc=2&device_ipv6=2a02:6b8::40c:6676:baff:fea6:53d8 HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Content-Length: 0
  Connection: close
  ```

{% endlist %}

## Другие методы Post API {#other-methods}

- [Загрузка событий](post-import-events.md)
- [Загрузка событий In-app Revenue](post-revenue.md)
- [Загрузка событий Ecommerce](post-ecommerce.md)
- [Атрибуты профиля](post-profile-attributes.md)

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
