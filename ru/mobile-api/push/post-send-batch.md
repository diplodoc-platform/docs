# Отправка push-сообщений

Отправляет одно или несколько push-сообщений на указанные устройства.

Операция позволяет отправить сообщения с разными свойствами (например, текст, медиа вложение) за один запрос. В каждом запросе может быть указано до 250 000 устройств на которые будут отправлены сообщения.

{% note info %}

Рекомендуем использовать данную операцию вместо устаревшей `POST /push/v1/send`.

{% endnote %}

## Формат запроса {#request_format}

```
POST {{ push-api-url }}/push/v1/send-batch
```

## Тело запроса {#request_body}

```json translate=no
{
  "push_batch_request": {
    "group_id": 1,
    "client_transfer_id": long,
    "tag": "string",
    "batch": [
      {
        "messages": {
          "android": {
            "silent": false,
            "content": {
              "title": "string",
              "text": "string",
              "icon": "string",
              "icon_background": "#AARRGGBB",
              "image": "https://example.com/picture.jpg",
              "banner": "https://example.com/picture.jpg",
              "data": "string",
              "channel_id": "string",
              "priority": -2,
              "collapse_key": 2001,
              "vibration": [0, 500],
              "led_color": "#RRGGBB",
              "led_interval": 50,
              "led_pause_interval": 50,
              "time_to_live": 180,
              "visibility": "public",
              "urgency": "high"
            },
            "open_action": {
              "deeplink": "yandexmaps://?"
            }
          },
          "iOS": {
            "silent": false,
            "content": {
              "title": "string",
              "text": "string",
              "badge": 1,
              "sound": "disable",
              "thread_id": "string",
              "category": "string",
              "mutable_content": 1,
              "expiration": 3600,
              "data": "string",
              "collapse_id": "string",
              "attachments": [
                {
                    "id": "string",
                    "file_url": "string",
                    "file_type": "string"
                },
                ...
              ]
            },
            "open_action": {
              "url": "https://ya.ru"
            }
          }
        },
        "devices": [
          {
            "id_type": "appmetrica_device_id",
            "id_values": ["123456789", "42"]
          },
          {
            "id_type": "ios_ifa",
            "id_values": ["8A690667-6204-4A6A-9B38-85DE016....."]
          },
          {
            "id_type": "google_aid",
            "id_values": ["eb5f3ec8-2e3e-492f-b15b-d21860b....."]
          },
          {
            "id_type": "android_push_token",
            "id_values": ["eFfxdO7uCMw:APA91bF1tN3X3BAbiJXsQhk-..."]
          },
          {
            "id_type": "ios_push_token",
            "id_values": ["F6A79E9F844A24C5FBED5C58A4C71561C180F........."]
          },
          {
            "id_type": "huawei_push_token",
            "id_values": ["0866422030....."]
          },
          {
            "id_type": "huawei_oaid",
            "id_values": ["ecef47f7-fcce-ad....."]
          }
        ]
      },
      {
        "messages": {
        ...
        }
      }
    ]
  }
}
```
#|
|| `push_batch_request` | Запрос на отправку группы push-сообщений ||
|| `push_batch_request.group_id`* | {{ push-get-id }} ||
|| `push_batch_request.client_transfer_id` | Идентификатор отправки, заданный пользователем. Используется для [проверки статуса отправки](get-status-group-id.md).

{% note alert %}

Значение поля `client_transfer_id` должно быть уникальным в указанной группе (`group_id`).

{% endnote %}
||
|| `push_batch_request.tag`* | [Тег отправки](*Тег отправки). ||
|| `push_batch_request.batch` | Массив объектов `messages`. Содержит push-сообщения с их свойствами. ||
|| `push_batch_request.batch.messages` | Push-сообщение. ||
|| `push_batch_request.batch.messages.android` | Платформа устройства. ||
|| `push_batch_request.batch.messages.android.silent` | Признак отправки [silent push-сообщений](*silent push-сообщений). Допустимые значения: `true | false`. ||
|| `push_batch_request.batch.messages.android.content` | Содержание push-сообщения. ||
|| `push_batch_request.batch.messages.android.content.title` | Заголовок push-сообщения. Обязателен для не silent push-сообщений. ||
|| `push_batch_request.batch.messages.android.content.text` | Текст сообщения. Обязателен для не silent push-сообщений. ||
|| `push_batch_request.batch.messages.android.content.icon` | Иконка в строке уведомлений. По умолчанию отображается стандартная иконка приложения. Чтобы поменять иконку задайте идентификатор ресурса иконки в стандартном каталоге `/res/drawable/`. ||
|| `push_batch_request.batch.messages.android.content.icon_background` | Цвет иконки сообщения. Задается в виде строки в формате шестандцатиричного кода `#AARRGGBB`. ||
|| `push_batch_request.batch.messages.android.content.image` | URL картинки, которая будет отображаться в push-уведомлении рядом с текстом уведомления. ||
|| `push_batch_request.batch.messages.android.content.banner` | Ссылка на баннер, отображаемый в push-сообщении. ||
|| `push_batch_request.batch.messages.android.content.data` | Произвольная строка данных. Вы можете передавать любые данные приложению в виде строкового значения. Обработать строку данных можно с помощью соответствующих методов AppMetrica Push SDK. ||
|| `push_batch_request.batch.messages.android.content.channel_id` | Идентификатор канала уведомлений. Если идентификатор не задан — используется канал по умолчанию.
Доступно только для Android 8 и выше. Подробнее о каналах в [документации Android](https://developer.android.com/training/notify-user/channels). ||
|| `push_batch_request.batch.messages.android.content.priority` | Приоритет уведомления. Допустимые значения: диапазон `[-2; 2]`. Платформа определяет сообщения с высоким приоритетом и принимает соответствующие действия: прерывает работу пользователя (отображает сообщение на экране), не уведомляет пользователя о уведомлении. На разных устройствах приоритет интерпретируется по-разному. ||
|| `push_batch_request.batch.messages.android.content.collapse_key` | Идентификатор нотификации. Значение по умолчанию — 0. Не влияет, если нет текущих отображаемых нотификаций данного приложения. Если отображена одна или несколько нотификации, то при совпадении id содержимое нотификации будет обновлено. При отличном от имеющихся id, будет показана новая нотификация. ||
|| `push_batch_request.batch.messages.android.content.vibration` | Паттерн вибрации при получении сообщения. Формат записи: `[пауза мс, длительность вибрации мс, пауза мс, длительность вибрации мс,...]`. ||
|| `push_batch_request.batch.messages.android.content.led_color` | Цвет LED-индикатора. Задается в виде строки в формате шестандцатиричного кода `#RRGGBB`. ||
|| `push_batch_request.batch.messages.android.content.led_interval` | Время загорания LED-индикатора в мс. ||
|| `push_batch_request.batch.messages.android.content.led_pause_interval` | Перерыв между загораниями LED-индикатора в мс. ||
|| `push_batch_request.batch.messages.android.content.time_to_live` | Время в секундах, в течение которого FireBase будет хранить push-сообщение, если устройство вне зоны доступа. ||
|| `push_batch_request.batch.messages.android.content.visibility` | Отображаемость push-сообщения на лок-скрине. Игнорируется с Android 8 и выше (API level 26+), где задаётся на уровне канала. Допустимые значения: `secret`, `private`, `public`. По умолчанию не задаётся. Подробнее о свойстве `visibility` в [документации Android](https://developer.android.com/reference/android/app/Notification#VISIBILITY_PRIVATE) ||
|| `push_batch_request.batch.messages.android.content.urgency` | Срочность (приоритет) доставки push-сообщения. Допустимые значения: `high`, `normal`. Значение по умолчанию — `high`. Срочные push-сообщения вызывают просыпание устройства, запуск приложения в фоновом режиме и получение доступа к интернету на короткий промежуток времени. Срочные push-сообщения доставляются быстрее и надёжнее. Подробнее о [приоритете FCM сообщений](https://firebase.google.com/docs/cloud-messaging/concept-options#setting-the-priority-of-a-message) в [документации Android](https://developer.android.com/training/monitoring-device-state/doze-standby#using_fcm). ||
|| `push_batch_request.batch.messages.android.open_action` | Действие, которое будет произведено при клике на push-сообщение. При отсутствии этого поля нажатие на push-сообщение приведет к открытию приложения. ||
|| `push_batch_request.batch.messages.android.open_action.deeplink` | Deeplink по которому будет осуществлен переход при клике на push-сообщение. ||
|| `push_batch_request.batch.messages.ios` | Платформа устройства. ||
|| `push_batch_request.batch.messages.ios.silent` | Признак отправки [silent push-сообщений](*silent push-сообщений). Допустимые значения: `true | false`. ||
|| `push_batch_request.batch.messages.ios.contentt` | Содержание push-сообщения. ||
|| `push_batch_request.batch.messages.ios.content.title` | Заголовок push-сообщения. Обязателен для не silent push-сообщений. ||
|| `push_batch_request.batch.messages.ios.content.text` | Текст сообщения. Обязателен для не silent push-сообщений. ||
|| `push_batch_request.batch.messages.ios.content.badge` | Число, которое отобразится на иконке приложения при получении сообщения. ||
|| `push_batch_request.batch.messages.ios.content.sound` | Звук сообщения. Допустимые значения `default | disable`. ||
|| `push_batch_request.batch.messages.ios.content.thread_id` | Идентификатор для группировки push-уведомлений. Значение указывается в свойстве [threadIdentifier](https://developer.apple.com/documentation/usernotifications/unmutablenotificationcontent/1649872-threadidentifier?language=objc) объекта [UNNotificationContent](https://developer.apple.com/documentation/usernotifications/unnotificationcontent). ||
|| `push_batch_request.batch.messages.ios.content.category` | Категория push-уведомления. Значение указывается в свойстве [identifier](https://developer.apple.com/documentation/usernotifications/unnotificationcategory/1649276-identifier?language=objc) объекта `UNNotificationCategory`. Подробнее об объявлении действий и категорий push-уведомлений [в документации Apple](https://developer.apple.com/documentation/usernotifications/declaring_your_actionable_notification_types?language=objc). ||
|| `push_batch_request.batch.messages.ios.content.mutable_content` | Признак расширения Notification Service Extension. Если указано значение `1`, то push-уведомление обрабатывается расширением. В AppMetrica с помощью него отслеживается доставка push-уведомлений.

Чтобы отслеживать доставку, настройте [сбор статистики push-уведомлений](ССЫЛКА) и передайте в поле значение `1`. Если значение не передается, то в отчетах число доставленных push-уведомлений будет равно числу открытых. ||
|| `push_batch_request.batch.messages.ios.content.expiration` | Время, в течение которого будут предприниматься попытки доставить сообщение на устройство пользователя. Задается в секундах.
Если по истечении указанного времени устройство будет недоступно (например, не подключено к интернету), сообщение не будет доставлено. По умолчанию время не ограничено. ||
|| `push_batch_request.batch.messages.ios.content.data` | Произвольная строка данных. Вы можете передавать любые данные приложению в виде строкового значения. Обработать строку данных можно с помощью соответствующих методов AppMetrica Push SDK. ||
|| `push_batch_request.batch.messages.ios.content.collapse_id` | Идентификатор сворачивания [apns-collapse-id](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/CommunicatingwithAPNs.html#//apple_ref/doc/uid/TP40008194-CH11-SW12). Несколько уведомлений с одним и тем же идентификатором отображаются пользователю как одно уведомление. ||
|| `push_batch_request.batch.messages.ios.content.attachments` | Массив вложений, которые необходимо прикрепить в push-сообщении. Подробности настройки можно прочитать в статье [Шаг 6. (_Опционально_) Настройте загрузку прикрепленных файлов](ССЫЛКА). ||
|| `push_batch_request.batch.messages.ios.content.attachments.id` | Идентификатор содержимого в push-сообщении. ||
|| `push_batch_request.batch.messages.ios.content.attachments.file_url` | URL файла из push-сообщения. ||
|| `push_batch_request.batch.messages.ios.content.attachments.file_type` | Тип вложенного файла в push-сообщении. Допустимые типы можно посмотреть в разделе [Типы файлов в push-сообщениях](file-type.md). ||
|| `push_batch_request.batch.messages.android.open_action` | Действие, которое будет произведено при клике на push-сообщение. При отсутствии этого поля нажатие на push-сообщение приведет к открытию приложения. ||
|| `push_batch_request.batch.messages.android.open_action.url` | URL по которому будет осуществлен переход при клике на push-сообщение. ||
|| `push_batch_request.batch.devices` | Устройства, на которые необходимо отправить push-уведомления. Одна отправка может содержать до 250 000 устройств.
Устройства группируются по `id_type`. В одной отправке допускается от 1 до 5 групп. Все группы в сумме за один HTTP-запрос могут содержать до 250 000 устройств. Например, если в группе `appmetrica_device_id` содержится 100 000 устройств, в остальных допускается указать 150 000. ||
|| `push_batch_request.batch.devices.id_type` | Тип идентификатора устройства. Допустимые значения: `appmetrica_device_id`, `ios_ifa`, `google_aid`, `android_push_token`, `ios_push_token`, `huawei_push_token`, `huawei_oaid`.

{% note info %}

При использовании push-токена в качестве идентификатора, AppMetrica проверяет перед отправкой наличие токена и информации об устройстве в базе. Если информации об устройстве нет, то push-сообщение не будет отправлено. Это необходимо для контроля отправки сообщений нужным адресатам и отображения информации в отчетах после отправки.

{% endnote %}

|| `push_batch_request.batch.devices.id_values` | Список устройств на которые необходимо отправить push-сообщения. 

{% note alert %}

Список не может быть пустым.

{% endnote %} ||
|#

## Формат ответа {#response_format}

```json translate=no
{
  "push_response": {
    "transfer_id": 1,
    "client_transfer_id": long
  }
}
```

#|
|| `push_response` | Ответ об отправке push-сообщений. ||
|| `push_response.transfer_id` | Идентификатор (ID) отправки. Используется для [проверки статуса](get-status-id.md) отправки. ||
|| `push_response.client_transfer_id` | Идентификатор (ID) отправки, заданный пользователем в теле запроса. Используется для [проверки статуса](get-status-group-id.md) отправки. 

{% note info %}

Поле будет возвращено только если оно было указано в теле запроса.

{% endnote %}
||
|#

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}

[*Тег отправки]: Тег — это произвольная строка, маркирующая каждую отправку push-сообщений через API. Одним тегом может быть промаркировано произвольное количество отправок. В отчете отображается на втором уровне.

[*silent push-сообщений]: Сообщение, которое обрабатывается приложением в фоновом режиме без отображения пользователю. С помощью silent push можно передать дополнительные данные, либо проверить доставляемость уведомлений.
