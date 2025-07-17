# Атрибуты профиля

Передает параметры пользователя.

Пример использования: вы можете передавать параметры пользователя в Post API, чтобы дополнить профиль пользователей и использовать эти данные в сегментации по аудитории. Например, добавить атрибут о том, что пользователь участник программы лояльности.

Свойства событий можно передавать в параметрах запроса или в теле. При передаче данных в теле, к URL запроса необходимо добавить `.csv`. Подробнее в разделе [Пример запроса](#sample).

Для привязки события к пользователю, необходимо использовать одно из следующих полей при запросе:

- `profile_id`
- `appmetrica_device_id`

{% note alert %}

Post API содержит ограничения на загрузку данных. Подробнее в разделе [Ограничения](restrictions.md).

{% endnote %}

## Формат запроса

```
POST {{ api-url }}/logs/v1/import/profiles
  ? post_api_key=<string>
  & application_id=<int>
  & profile_id=<string>
  & attributes=<>
```

#|
|| `post_api_key`* | {{ post_api_key }} ||
|| `application_id`* | {{ application_id }} ||
|| `profile_id`* | {{ post-profile_id }}

{% note alert %}

Не передавайте значение вместе с параметром `appmetrica_device_id`. Сервер принимает только один из параметров.

{% endnote %}

||
|| `attributes`* | Набор значений пользовательских атрибутов в формате `{key:value}`. Value может принимать тип string, number, bool, counter. Если для профиля уже записано значение переданного атрибута — оно будет перезаписано на новое. Предшествующие значения атрибута не сохранятся. Подробнее о [пользовательских атрибутах профилей](../../data-collection/profile-attributes.md).

{% note alert %}

Чтобы собирать собственные атрибуты профилей, необходимо добавить их в настройках приложения. Для этого на странице приложения нажмите в разделе **Настройки** нажмите **Атрибуты профилей**.

{% endnote %}
||
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
  POST /logs/v1/import/profiles.csv?post_api_key=0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ012 HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Connection: close
  
  application_id,profile_id,attributes
  1234567890,1234567890abcdef,"{""string_attribute_name"":""string_value"",""number_attribute_name"":1234,""bool_attribute_name"":true,""counter_attribute_name"":-1}"
  ```

- Передача данных в параметрах запроса

  ```http translate=no
  POST /logs/v1/import/profiles?post_api_key=0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ012&application_id=1234567890&profile_id=1234567890abcdef&attributes={"string_attribute_name":"string_value","number_attribute_name":1234,"bool_attribute_name":true,"counter_attribute_name":-1} HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Content-Length: 0
  Connection: close
  ```

{% endlist %}

С помощью Post API можно изменить только [собственные](../../data-collection/profile-attributes.md#custom) пользовательские атрибуты. Чтобы передать [предопределенные](../../data-collection/profile-attributes.md) атрибуты, используйте AppMetrica SDK. Подробнее см. в разделе [{#T}](../../data-collection/about-profiles.md#profile-settings).

## Другие методы Post API {#other-methods}

- [Загрузка событий](post-import-events.md)
- [Загрузка событий In-app Revenue](post-revenue.md)
- [Загрузка событий Ad Revenue](post-adrevenue.md)
- [Загрузка событий Ecommerce](post-ecommerce.md)

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
