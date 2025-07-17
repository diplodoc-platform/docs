# Сценарии использования

## Создание группы {#create}

Для отправки сообщения необходимо указать уникальное имя группы. Каждая отправка обязательно принадлежит какой-либо созданной группе. Это позволяет объединять отправки в отчете.

Для создания группы выполните запрос [`POST /push/v1/management/groups`](post-groups.md):

```
curl -X POST \
  '{{ push-api-url }}/push/v1/management/groups' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: OAuth <your_token>' \
  -d '{"group":{"app_id":XXXXXX,"name":"the_name_of_the_group"}}'
```

где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../intro/authorization.md#get-oauth-token).

В случае успешного запроса будет получен ответ вида:

```
{
  "group": {
    "id": XXXXXX,
    "app_id": XXXXXX,
    "name": "the_name_of_the_group"
  }
}
```

Полученный `group_id` необходимо использовать для дальнейших отправок push-сообщений.

## Отправка push-сообщения {#send-push}

Для отправки сообщения необходимо указать идентификатор группы и тег отправки. Несколько отправок могут иметь одинаковый тег. Тег может быть произвольной строкой, отображается в отчетах на втором уровне.

Для отправки сообщения выполните запрос [`POST /push/v1/send-batch`](post-send-batch.md):

```
curl -X POST \
  '{{ push-api-url }}/push/v1/send-batch' \
  -H 'Authorization: OAuth <your_token>' \
  -H 'Content-Type: application/json' \
  -d '{
  "push_batch_request": {
    "group_id": XXXXXX,
      "tag": "some_tag",
      "batch": [
      {
        "messages": {
          "android": {
            "silent": false,
            "content": {
              "title": "Sample android title",
              "text": "Sample android text",
              "icon": "46",
              "icon_background": "#FFFFFFFF",
              "banner": "http://example.png",
              "data": "foobarbaz",
              "priority": -2,
              "collapse_key": 2001,
              "vibration": [0, 500],
              "led_color": "#FFFFFF",
              "led_interval": 50,
              "led_pause_interval": 50,
              "time_to_live": 180
            }
          },
          "iOS": {
            "silent": false,
            "content": {
              "text": "Sample iOS text",
              "badge": "0",
              "data": "foobarbaz",
              "sound": "disable"
            }
          }
        },
        "devices": [
          {
            "id_type": "ios_ifa",
            "id_values": ["8003C3CF-A3BC-4DDD-B6DF-1DD......"]
          },
          {
            "id_type": "google_aid",
            "id_values": ["8e4dd44b-82ec-43d0-a5de-321......"]
          }
        ]
      }
    ]
  }'
```

где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../intro/authorization.md#get-oauth-token).

{% note info %}

Описание полей запроса приведены в разделе [Отправка push-сообщений](post-send-batch.md).

{% endnote %}

В случае успешного запроса будет получен ответ вида:

```
{
  "push_response": {
  "transfer_id": XXXXXX
  }
}
```

Полученный `transfer_id` используется для проверки статуса отправки.

## Проверка статуса отправки {#check-transfer}

Для проверки статуса отправки используется идентификатор отправки `transferId`.

{% note info %}

Вы также можете отслеживать отправку по заданному значению поля `client_transfer_id`. Подробнее в разделе [Отправка push-сообщений](post-send-batch.md).

{% endnote %}

Для отправки сообщения выполните запрос [`GET /push/v1/status/{transferId}`](get-status-id.md):

```
curl -X GET \
  '{{ push-api-url }}/push/v1/status/XXXXXX' \
  -H 'Authorization: OAuth <your_token>'
```

где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../intro/authorization.md#get-oauth-token).

Будет получен ответ вида:

```
{
  "transfer": {
    "creation_date": "2017-11-03T18:29:25+03:00",
    "id": XXXXXX,
    "status": "failed",
    "tag": "some_tag",
    "group_id": XXXXXX,
    "errors": [
      "Invalid push credentials for platform android"
    ]
  }
}
```

{% note info %}

Описание полей ответа приведены в разделе [Проверка статуса отправки по transferId](get-status-id.md).

{% endnote %}

## Получение отчета по push-кампании {#report}

Для получения отчета по отправленным push-сообщениям необходимо использовать [API отчетов](../api_v1/intro.md).

Для получения информации по отправке push-сообщений используйте запрос следующего типа

```
curl -X GET \
  '{{ api-url }}/stat/v1/data?limit=10&date1=today&date2=today&ids=XXXXXX&metrics=ym:pc:users&dimensions=ym:pc:group,ym:pc:tag,ym:pc:transfer'
  -H 'Authorization: OAuth <your_token>'
```

где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../intro/authorization.md#get-oauth-token).

В случае успешного запроса будет получен ответ вида:

```
{
  "dimensions": [
    {
      "id": "1",
      "name": "the_name_of_the_group"
    },
    {
      "name": "some_tag"
    },
    {
      "name": "99"
    }
  ],
  "metrics": [
      1
  ]
}
...
```

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
