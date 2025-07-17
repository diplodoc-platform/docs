# Загрузка событий Ecommerce

Передает данные о Ecommerce-событиях.

Пример использования: вы можете передавать все Ecommerce-события через Post API, чтобы в одном месте собирать данные о покупках пользователей не только в приложении, но и, например, в оффлайн магазине или на веб сайте.

Свойства событий можно передавать в параметрах запроса или в теле. При передаче данных в теле, к URL запроса необходимо добавить `.csv`. Подробнее в разделе [Пример запроса](#sample).

Для привязки события к пользователю, необходимо использовать одно из следующих полей при запросе:

- `profile_id`
- `appmetrica_device_id`

{% note alert %}

Post API содержит ограничения на загрузку данных. Подробнее в разделе [Ограничения](restrictions.md).

{% endnote %}

## Формат запроса

```
POST {{ api-url }}/logs/v1/import/ecommerce
  ? post_api_key=<string>
  & application_id=<int>
  & profile_id=<string>
  & appmetrica_device_id=<int>
  & event_timestamp=<int>
  & ecom_event_type=<string>
  & order_id=<string>
  & product_name=<string>
  & cart_item_quantity=<int>
  & [cart_item_price_currency=<string>]
  & [cart_item_price_value=<int>]
  & [cart_item_price_internal_currency=<array>]
  & [cart_item_price_internal_value=<array>]
  & [actual_price_currency=<string>]
  & [actual_price_value=<int>]
  & [actual_price_internal_currency=<array>]
  & [actual_price_internal_value=<array>]
  & [payload=<string>]
  & [product_category_path_1=<string>]
  & [product_category_path_2=<string>]
  & [product_category_path_3=<string>]
  & [product_category_path_4=<string>]
  & [product_category_path_5=<string>]
  & [product_category_path_6=<string>]
  & [product_category_path_7=<string>]
  & [product_category_path_8=<string>]
  & [product_category_path_9=<string>]
  & [product_category_path_10=<string>]
  & original_price_currency=<string>
  & original_price_value=<int>
  & [original_price_internal_currency=<array>]
  & [original_price_internal_value=<array>]
  & [product_payload=<string>]
  & [product_promo_codes=<array>]
  & [product_sku=<string>]
  & [screen_category_path_1=<string>]
  & [screen_category_path_2=<string>]
  & [screen_category_path_3=<string>]
  & [screen_category_path_4=<string>]
  & [screen_category_path_5=<string>]
  & [screen_category_path_6=<string>]
  & [screen_category_path_7=<string>]
  & [screen_category_path_8=<string>]
  & [screen_category_path_9=<string>]
  & [screen_category_path_10=<string>]
  & [screen_name=<string>]
  & [screen_payload=<string>]
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
|| `ecom_event_type`* | {{ post-ecom_event_type }} ||
|| `order_id`* | {{ revenue_order_id }} ||
|| `product_name`* | {{ post-product_name }} ||
|| `cart_item_quantity`* | Количество единиц товара в корзине. ||
|| `cart_item_price_currency` | Валюта цены товара в корзине. Если не указано, используется значение `actual_price_currency`. [Список доступных валют](../../data-collection/currency-codes.md). ||
|| `cart_item_price_value` | Цена товара в корзине. Это итоговая цена с учётом всех акций, промокодов, бонусных баллов и прочих скидок, которые применил пользователь. Если не указано, используется значение `actual_price_value`.||
|| `cart_item_price_internal_currency` | Тип внутренней валюты для товара в корзине. Если не указано, используется значение `actual_price_internal_currency`. ||
|| `cart_item_price_internal_value` | Цена товара в корзине во внутренней валюте. Это итоговая цена с учётом всех акций, промокодов, бонусных баллов и прочих скидок, которые применил пользователь. Если не указано, используется значение `actual_price_internal_value`. ||
|| `actual_price_currency` | Валюта актуальной цены товара. Если не указано, используется значение `original_price_currency`. [Список доступных валют](../../data-collection/currency-codes.md). ||
|| `actual_price_value` | Актуальная цена товара. Это текущая цена на товар с учётом скидок. Если не указано, используется значение `original_price_value`. ||
|| `actual_price_internal_currency` | Внутренняя валюта актуальной цены товара. Если не указано, используется значение `original_price_internal_currency`. ||
|| `actual_price_internal_value` | Актуальная цена товара во внутренней валюте. Это текущая цена на товар с учётом скидок. Если не указано, используется значение `original_price_internal_value`. ||
|| `payload` | {{ post-payload }} ||
|| `product_category_path_1` | Категория товара 1 уровня. ||
|| `product_category_path_2` | Категория товара 2 уровня. ||
|| `product_category_path_3` | Категория товара 3 уровня. ||
|| `product_category_path_4` | Категория товара 4 уровня. ||
|| `product_category_path_5` | Категория товара 5 уровня. ||
|| `product_category_path_6` | Категория товара 6 уровня. ||
|| `product_category_path_7` | Категория товара 7 уровня. ||
|| `product_category_path_8` | Категория товара 8 уровня. ||
|| `product_category_path_9` | Категория товара 9 уровня. ||
|| `product_category_path_10` | Категория товара 10 уровня. ||
|| `original_price_currency`* | Валюта стартовой цены товара. [Список доступных валют](../../data-collection/currency-codes.md). ||
|| `original_price_value`* | Стартовая цена товара без учёта скидок.||
|| `original_price_internal_currency` | Внутренняя валюта стартовой цены товара. ||
|| `original_price_internal_value` | Стартовая цена товара во внтутренеей валюте. ||
|| `product_payload` | {{ post-payload }} ||
|| `product_promo_codes` | Массив применённых промокодов. ||
|| `product_sku` | Индентификатор товара. ||
|| `screen_category_path_1` | Страница категории товаров 1 уровня. ||
|| `screen_category_path_2` | Страница категории товаров 2 уровня. ||
|| `screen_category_path_3` | Страница категории товаров 3 уровня. ||
|| `screen_category_path_4` | Страница категории товаров 4 уровня. ||
|| `screen_category_path_5` | Страница категории товаров 5 уровня. ||
|| `screen_category_path_6` | Страница категории товаров 6 уровня. ||
|| `screen_category_path_7` | Страница категории товаров 7 уровня. ||
|| `screen_category_path_8` | Страница категории товаров 8 уровня. ||
|| `screen_category_path_9` | Страница категории товаров 9 уровня. ||
|| `screen_category_path_10` | Страница категории товаров 10 уровня. ||
|| `screen_name` | Название просмотренной страницы или экрана. ||
|| `screen_payload` | {{ post-payload }} ||
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
  POST /logs/v1/import/ecommerce.csv?post_api_key=0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ012 HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Content-Length: 540i
  Connection: close
  
  application_id,profile_id,appmetrica_device_id,event_timestamp,ecom_event_type,order_id,product_name,cart_item_quantity,cart_item_price_currency,cart_item_price_value,cart_item_price_internal_currency
  cart_item_price_internal_value,actual_price_currency,actual_price_value,actual_price_internal_currency,actual_price_internal_value,payload,product_category_path_1,product_category_path_2,product_category_path_3,product_category_path_4,product_category_path_5,product_category_path_6,product_category_path_7,product_category_path_8,product_category_path_9,product_category_path_10,original_price_currency,original_price_value,original_price_internal_currency,original_price_internal_value,product_payload,product_promo_codes,product_sku,screen_category_path_1,screen_category_path_2,screen_category_path_3,screen_category_path_4,screen_category_path_5,screen_category_path_6,screen_category_path_7,screen_category_path_8,screen_category_path_9,screen_category_path_10,screen_name,screen_payload,session_type,ios_ifa,ios_ifv,google_aid,windows_aid,os_name,os_version,device_manufacturer,device_model,device_type,device_locale,app_version_name,app_package_name,connection_type,operator_name,mcc,mnc,device_ipv6
  1234567890,1234567890abcdef,1234567890abcdef,1757762239877245682,1689943892,ADD_TO_CART,a1b2c3d4,some_product,1,usd,0.5,some_currency,1.43,usd,0.7,some_currency,2,"{""key"":""value_1""}",product_path_1,product_path_2,product_path_3,product_path_4,product_path_5,product_path_6,product_path_7,product_path_8,product_path_9,product_path_10,usd,1.05,some_currency,3,"{""key"":""value_1""}","[promo_code_1,promo_code_2]",012345abc,screen_path_1,screen_path_2,screen_path_3,screen_path_4,screen_path_5,screen_path_6,screen_path_7,screen_path_8,screen_path_9,screen_path_10,some_screen,"{""key"":""value_1""}",foreground,123456abcde,567890abcde,ios,16.6,Apple,iPhone14Pro,phone,en_US,some_version_name,some_package_name,wifi,MegaFon,250,2,2a02:6b8::40c:6676:baff:fea6:53d8
  ```

- Передача данных в параметрах запроса

  ```http translate=no
  POST /logs/v1/import/ecommerce.csv?post_api_key=0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ012&application_id=1234567890&profile_id=1234567890abcdef&appmetrica_device_id=1757762239877245682&event_timestamp=1689943892&ecom_event_type=ADD_TO_CART&order_id=a1b2c3d4&product_name=some_product&cart_item_quantity=1&cart_item_price_currency=usd&cart_item_price_value=0.5&cart_item_price_internal_currency=some_currency&cart_item_price_internal_value=1.43&actual_price_currency=usd&actual_price_value=0.7&actual_price_internal_currency=some_currency&actual_price_internal_value=2&payload="{""key"":""value_1""}"&product_category_path_1=product_path_1&product_category_path_2=product_path_2&product_category_path_3=product_path_3&product_category_path_4=product_path_4&product_category_path_5=product_path_5&product_category_path_6=product_path_6&product_category_path_7=product_path_7&product_category_path_8=product_path_8&product_category_path_9=product_path_9&product_category_path_10=product_path_10&original_price_currency=usd&original_price_value=1.05&original_price_internal_currency=some_currency&original_price_internal_value=3&product_payload="{""key"":""value_1""}"&product_promo_codes="[promo_code_1,promo_code_2]"&product_sku=012345abc&screen_category_path_1=screen_path_1&screen_category_path_2=screen_path_2&screen_category_path_3=screen_path_3&screen_category_path_4=screen_path_4&screen_category_path_5=screen_path_5&screen_category_path_6=screen_path_6&screen_category_path_7=screen_path_7&screen_category_path_8=screen_path_8&screen_category_path_9=screen_path_9&screen_category_path_10=screen_path_10&screen_name=some_screen&screen_payload="{""key"":""value_1""}"&session_type=foreground&ios_ifa=123456abcde&ios_ifv=54321edcba&google_aid=098765abcde&windows_aid=567890abcde&os_name=ios&os_version=16.6&device_manufacturer=Apple&device_model=iPhone14Pro&device_type=phone&device_locale=en_US&app_version_name=some_version_name&app_package_name=some_package_name&connection_type=wifi&operator_name=MegaFon&mcc=250&mnc=2&device_ipv6=2a02:6b8::40c:6676:baff:fea6:53d8 HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Content-Length: 0
  Connection: close
  ```

{% endlist %}

## Другие методы Post API {#other-methods}

- [Загрузка событий](post-import-events.md)
- [Загрузка событий In-app Revenue](post-revenue.md)
- [Загрузка событий Ad Revenue](post-adrevenue.md)
- [Атрибуты профиля](post-profile-attributes.md)

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
