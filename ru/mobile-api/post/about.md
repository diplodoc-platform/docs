# Post API

Позволяет отправить события с помощью HTTP-запроса в AppMetrica. Эти данные будут отображены в [отчетах AppMetrica](../../mobile-reports/index.md).

Загрузить события можно через параметры запроса или в теле в формате `csv`. Данные, переданные через SDK и API, будут объединены при идентичном значении [profile_id](*profile_id) или [appmetrica_device_id](*appmetrica_device_id).

Загруженные данные записываются к общим, которые были получены от SDK. Синхронизация данных, переданных от Post API, происходит раз в 4 часа.

## Доступ к API {#access}

Для работы с Post API необходимо получить _Post API key_ в разделе **Настройки** вашего приложения.

Полученный токен следует передавать при каждом запросе к API в значении параметра `post_api_key`.

Подробнее в [примере](post-import-events.md).

## Хосты {#hosts}

Запрос выполняется к хосту `{{ api-url }}`. Например:

```httpget translate=no
{{ api-url }}/logs/v1/import/events
```

или

```httpget translate=no
{{ api-url }}/logs/v1/import/events.csv
```

## Ресурсы API {#resources}

- [Загрузка событий](post-import-events.md)
- [Загрузка событий In-app Revenue](post-revenue.md)
- [Загрузка событий Ad Revenue](post-adrevenue.md)
- [Загрузка событий Ecommerce](post-ecommerce.md)
- [Атрибуты профиля](post-profile-attributes.md)

{% if locale == "ru" %}

## Узнать больше {#learn-more}

- [Больше данных в Post API для офлайн событий вашего приложения](https://appmetrica.yandex.ru/about/blog/post_api)

{% endif %}

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}

[*profile_id]: {{ profile_id }}

[*appmetrica_device_id]: Хеш от уникального идентификатора устройства, который устанавливает AppMetrica.
