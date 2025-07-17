# Параметры postback

Ниже представлено описание деталей поддержки postback в AppMetrica.

## Общая информация {#general}

AppMetrica позволяет задавать postback для трекера и указывать, в какой момент отправить postback. AppMetrica поддерживает:

- postback об установке приложения ([install postback](postback-quota.md#install-postback));
- postback о заданном событии в приложении, произошедшем после установки ([event postback](postback-quota.md#event-postback));
- postback при получении из приложения ecommerce-события ([ecommerce postback](postback-quota.md#ecommerce-postback));
- postback при получении из приложения события об inapp-покупках ([purchase postback](postback-quota.md#inapp-postback));
- postback при получении из приложения события о показе рекламы ([adrevenue postback](postback-quota.md#adrevenue-postback)).

Применяются следующие правила:

- Postback отправляется при появлении заданного события или атрибуции установки. Задержка при отправке составляет около 5 минут.
- При получении HTTP-статуса `200 OK` отправка считается успешной.
- Если получен другой HTTP-статус, AppMetrica переотправляет postback в течении 24 часов. Переотправка производится каждые 5-10 минут.
- Event postback посылается о событиях, произошедших не более чем через 6 месяцев после установки.

## Передача параметров tracking URL {#trackingurl-params}

AppMetrica позволяет передавать любые [параметры tracking URL](tracking-specification.md) в постбэке — укажите в postback URL или postback body (для метода POST) имя параметра из tracking URL в фигурных скобках: `{parameter_name}`.

Например, в tracking URL передаются следующие параметры:

```
https://redirect.appmetrica.yandex.com/serve/123456?custom_parameter=value1&another_param=value2
```

Чтобы передать параметры `value1` и `value2` в `postback URL` следует написать:

```
https://endpoint.myadnetwork.com?some_parameter={custom_parameter}&another_param={another_param}
```

Для передачи параметров `value1` и `value2` методом POST в теле запроса следует написать:

```
{
  "some_parameter": "{custom_parameter}",
  "another_param": "{another_param}"
}
```

## Список макросов для postback {#macros}

AppMetrica поддерживает список системных макросов, которые могут быть использованы в postback URL или postback body (для метода POST). Список содержит макросы для информации об устройстве, атрибуцированном клике или показе и приложении. Если AppMetrica не может определить значение параметра для макроса, то параметр будет пустым.

### Информация о кликах, установках и событиях {#events}

`{adwords_link_id}` — ID связи Google Ads и AppMetrica. Подробнее в разделе [Настройка трекинга кампаний Google Ads](adwords-settings.md).

`{click_id}` — уникальный ID клика/показа. Макрос недоступен для неатрибуцированных постбеков.

`{match_type}` — каким образом клик/показ был ассоциирован с установкой. Возможные значения: `referrer` | `fingerprint` | `identifier`.

`{attributed_touch_type}` — тип рекламного взаимодействия. Возможные значения: `click` | `impression`.

`{transaction_id}` — идентификатор данного наступления события или установки. Например, если то же самое устройство генерирует то же самое событие, то `transaction_id` изменится.

`{click_user_agent}` — User-agent клика/показа.

`{click_datetime}` — {% if locale == 'ru' %}[UTC](https://ru.wikipedia.org/wiki/Всемирное_координированное_время){% endif %}{% if locale == 'en' %}[UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time){% endif %} дата и время клика/показа в формате RFC3339.

`{click_timestamp}` — время клика/показа в формате UNIX timestamp в секундах.

`{click_timezone}` — временная зона клика/показа в формате разницы с UTC в секундах.

`{click_ipv6}` — IP-адрес в момент клика/показа в формате IPv6. Например, 2a02:6b8::40c:6676:baff:fea6:53d8, ::ffff:5.255.232.147.

`{conversion_datetime}` — UTC дата и время конверсии (события на устройстве) в формате RFC3339.

`{conversion_timestamp}` — время конверсии (события на устройстве) в формате UNIX timestamp в секундах.

`{conversion_timezone}` — временная зона (местоположения пользователя) для конверсии. В формате разницы с UTC в секундах.

`{conversion_event_name}` — имя события для учета конверсии.

`{conversion_event_json}` — вложенные атрибуты события в формате {% if locale == 'ru' %}[JSON](http://www.json.org/json-ru.html){% endif %}{% if locale == 'en' %}[JSON](http://www.json.org/){% endif %}.

`{install_datetime}` — UTC дата и время установки в формате RFC3339.

`{install_timestamp}` — время установки в формате UNIX timestamp в секундах.

`{install_timezone}` — временная зона (местоположения пользователя) для установки. В формате разницы с UTC в секундах.

`{install_ipv6}` — IP-адрес в момент установки в формате IPv6 (например, 2a02:6b8::40c:6676:baff:fea6:53d8, ::ffff:5.255.232.147).

`{start_datetime}` — UTC дата и время старта сессии в формате RFC3339.

`{start_timestamp}` — время старта сессии в формате UNIX timestamp в секундах.

`{start_timezone}` — временная зона старта сессии в формате разницы с UTC в секундах.

`{session_id}` — идентификатор сессии. Уникален только в пределах конкретного приложения, `appmetrica_device_id`, конкретной установки и типа сессии (foreground/background).

### Информация об устройстве {#device}

`{adwords_rdid}` — Google AID для Android или IFA для iOS. Если Google AID или IFA отсутствуют — передается `"00000000-0000-0000-0000-000000000000"`.

`{appmetrica_device_id}` — уникальный идентификатор устройства, который устанавливает AppMetrica.

`{profile_id}` — идентификатор профиля. Подробнее в разделе [Профиль пользователя](../data-collection/about-profiles.md).

`{limit_ad_tracking}` — ограничение трекинга рекламы на устройстве. Может принимать значения: 1 — если пользователь отключил идентификатор рекламы, 0 — если не отключил. Если на устройстве доступно несколько идентификаторов (например, Google AID и Huawei OAID), то принимает значение 0, если доступен хотя бы один.

`{google_aid}` — Google AID устройства в формате, в котором получен с устройства.

`{ios_ifa}` — IFA устройства в формате, в котором получен с устройства.

`{ios_ifv}` — IFV для приложения в формате, в котором получен с устройства.

`{oaid}` — Huawei OAID устройства в формате, в котором получен с устройства.

`{windows_aid}` — Windows AID в формате, в котором получен с устройства.

`{device_manufacturer}` — производитель устройства, определяется сервисом AppMetrica (например, Apple или Samsung).

`{device_model}` — модель устройства, определяется сервисом AppMetrica (например, Galaxy S6).

`{device_type}` — тип устройства, определяется сервисом AppMetrica. Возможные значения: `PHONE` | `TABLET` | `PHABLET` | `TV`.

`{device_locale}` — язык устройства.

`{os_name}` — операционная система. Возможные значения: `ios` | `android` | `windows`.

`{os_version}` — версия операционной системы на устройстве пользователя.

`{operator_name}` — имя оператора сотовой связи.

`{mcc}` — мобильный код страны.

`{mnc}` — код мобильной сети.

### Информация о приложении и операционной системе {#app}

`{app_version_name}` — версия приложения; в виде, как указана разработчиком.

`{app_package_name}` — имя пакета для Android или `Bundle ID` для iOS (например, `ru.yandex.metro`).

`{appmetrica_sdk_version}` — версия библиотеки AppMetrica, которая была интегрирована в приложение.

`{store_app_id}` — идентификатор приложения в Google Play или App Store.

### Макросы для ad revenue событий {#adrevenue}

`{price}` — доход от показа.

`{currency}` — валюта дохода от показа.

### Макросы для любых покупок {#purchases}

`{price}` — цена покупки или товара.

`{currency}` — валюта покупки.

`{product_id}` — `product_id` покупки. Для inapp покупок — указанный при создании покупки в App Store или Google Play. Для Ecommerce — `product_id` товара.

`{order_id}` — идентификатор заказа.

### Макросы только для inapp покупок {#inapp}

`{inapp_transaction_id}` — уникальный идентификатор покупки.

`{inapp_validated}` — провалидирована ли покупка в App Store или Google Play.

`{inapp_receipt}` — информация о покупке от App Store или Google Play.

### Макросы только для Ecommerce покупок {#ecommerce}

`{ecom_revenue}` — полный доход от оформленной покупки.

`{ecom_quantity}` — количество единиц конкретного товара.

`{ecom_product_name}` — название товара.

`{ecom_promocodes}` — примененные промокоды.

`{ecom_type}` — тип ecommerce-события. Возможные значения:

  - `1` — показ экрана.
  - `2` — показ карточки товара в списке.
  - `3` — карточка товара.
  - `4` — добавление в корзину.
  - `5` — удаление из корзины.
  - `6` — начало оформления заказа.
  - `7` — покупка.

`{ecom_category_path_1}` — категория товара.

`{ecom_category_path_2}` — категория товара.

`{ecom_category_path_3}` — категория товара.

`{ecom_category_path_4}` — категория товара.

`{ecom_category_path_5}` — категория товара.

`{ecom_category_path_6}` — категория товара.

`{ecom_category_path_7}` — категория товара.

`{ecom_category_path_8}` — категория товара.

`{ecom_category_path_9}` — категория товара.

`{ecom_category_path_10}` — категория товара.

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
