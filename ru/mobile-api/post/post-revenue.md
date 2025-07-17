# Загрузка событий In-app Revenue

Передает данные о покупках.

Пример использования: вы можете передавать в AppMetrica In-app Revenue события через Post API, если покупки в вашем приложении осуществятся не через Google Play или AppStore и не отслеживаются на клиенте. Если вы отслеживаете данные о подписках внутри приложения самостоятельно или используете сторонний сервис, вы можете передавать данные о подписках через Post API.

События покупок, полученные через Post API, используются в расчете всех метрик, также они доступны в воронках и когортах.

{% note info %}

Revenue события, полученные через Post API не проходят валидацию и всегда считаются валидными.

{% endnote %}

Свойства событий можно передавать в параметрах запроса или в теле. При передаче данных в теле, к URL запроса необходимо добавить `.csv`. Подробнее в разделе [Пример запроса](#sample).

Для привязки события к пользователю, необходимо использовать одно из следующих полей при запросе:

- `profile_id`
- `appmetrica_device_id`

{% note alert %}

Post API содержит ограничения на загрузку данных. Подробнее в разделе [Ограничения](restrictions.md).

{% endnote %}

## Формат запроса

```
POST {{ api-url }}/logs/v1/import/revenue
  ? post_api_key=<string>
  & application_id=<int>
  & profile_id=<string>
  & appmetrica_device_id=<int>
  & revenue_event_type=<string>
  & event_timestamp=<int>
  & price=<decimal>
  & currency=<string>
  & product_id=<string>
  & [quantity=<int>]
  & [payload=<string>]
  & [transaction_id=<int>]
  & [order_id=<int>]
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
|| `revenue_event_type`* | {{ post-revenue_event_type }} ||
|| `event_timestamp`* | {{ event_timestamp }} ||
|| `price`* | {{ post-price }} ||
|| `currency` | {{ post-currency }} [Список доступных валют](../../data-collection/currency-codes.md). ||
|| `product_id` | {{ revenue_product_id }} ||
|| `quantity` | {{ revenue_quantity }} Значение по умолчанию: `1`. ||
|| `payload` | {{ post-payload }} ||
|| `transaction_id` | {{ post-transaction_id }} ||
|| `order_id` | {{revenue_order_id }} ||
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
  POST /logs/v1/import/revenue.csv?post_api_key=0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ012 HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Content-Length: 540i
  Connection: close
  
  appmetrica_device_id,device_model,device_type,google_aid,app_package_name,operator_name,mnc,application_id,account_id,event_timestamp,price,currency,product_id,quantity,transaction_id,order_id,revenue_event_type
  1757762239877245682,iPhone X,phone,01234567-890a-bcde-f012-3456789abcde,com.yandex.sample.metrica,MegaFon,2,1111,1234567890123456789,1689943892,0.0001,usd,some_product1,1,transact1,8101,promo_started
  1757762239877245682,iPhone X,phone,76543210-890a-bcde-f012-3456789abcde,com.yandex.sample.metrica,MegaFon,2,1111,9876543210987654321,1689943892,0.0001,usd,some_product2,2,transact2,1234,expired
  
  ```
  
- Передача данных в параметрах запроса

  ```http translate=no
  POST /logs/v1/import/revenue.csv?post_api_key=0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ012&appmetrica_device_id=1757762239877245682&device_model=iPhoneX&device_type=phone&google_aid=01234567-890a-bcde-f012-3456789abcde&app_package_name=com.yandex.sample.metrica&operator_name=MegaFon&mnc=2&application_id=1111&account_id=1234567890123456789&event_timestamp=1689943892&price=0.0001&currency=usd&product_id=some_product1&quantity=1&transaction_id=transact1&order_id=8101&revenue_event_type=promo_started HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Content-Length: 0
  Connection: close
  ```

{% endlist %}

## Другие методы Post API {#other-methods}

- [Загрузка событий](post-import-events.md)
- [Загрузка событий Ad Revenue](post-adrevenue.md)
- [Загрузка событий Ecommerce](post-ecommerce.md)
- [Атрибуты профиля](post-profile-attributes.md)

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
