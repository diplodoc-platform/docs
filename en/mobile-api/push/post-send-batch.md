# Sending push messages

Sends one or several push messages to the specified devices.

This operation allows you to send messages with different properties (e.g. text, media attachment, etc.) in a single HTTP request. Each request can contain up to 250,000 devices to which messages will be sent.

{% note info %}

We recommend using this operation instead of the obsolete `POST /push/v1/send`.

{% endnote %}

## Request format {#request_format}

```
POST {{ push-api-url }}/push/v1/send-batch
```

## Request body {#request_body}

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
|| `push_batch_request` | Request to send batch push messages ||
|| `push_batch_request.group_id`* | {{ push-get-id }} ||
|| `push_batch_request.client_transfer_id` | Sending ID specified by the user. It is used for [checking the status of the sending](get-status-group-id.md).

{% note alert %}

The `client_transfer_id` value must be unique in the specified group (`group_id`).

{% endnote %}
||
|| `push_batch_request.tag`* | [The sending tag](*The sending tag). ||
|| `push_batch_request.batch` | Array of `messages` objects. It contains push messages with properties. ||
|| `push_batch_request.batch.messages` | Push message. ||
|| `push_batch_request.batch.messages.android` | The device platform. ||
|| `push_batch_request.batch.messages.android.silent` | A flag that indicates [silent push](*silent push) sending. Possible values: `true | false`. ||
|| `push_batch_request.batch.messages.android.content` | The content of the push message. ||
|| `push_batch_request.batch.messages.android.content.title` | The title of the push message. The value is mandatory for the non-silent push messages. ||
|| `push_batch_request.batch.messages.android.content.text` | The text of the message. The value is mandatory for the non-silent push messages. ||
|| `push_batch_request.batch.messages.android.content.icon` | The icon is shown in the notification bar. By default, the standard app icon is displayed. To change the icon, set the icon resource ID in the standard `/res/drawable/` directory. ||
|| `push_batch_request.batch.messages.android.content.icon_background` | The color of the message icon. It is specified as a string in the format of the hex code `#AARRGGBB`. ||
|| `push_batch_request.batch.messages.android.content.image` | The URL of the image which is displayed in the push message next to the notification text. ||
|| `push_batch_request.batch.messages.android.content.banner` | The URL of the image that is shown in the push message. ||
|| `push_batch_request.batch.messages.android.content.data` | An arbitrary data string. You can pass any data you need as a string value. You can process the data string by using the appropriate AppMetrica Push SDK methods. ||
|| `push_batch_request.batch.messages.android.content.channel_id` | ID of the notification channel. If the ID is not specified, the default channel is used.
Available for Android 8 or higher. For more information about channels, see [Android documentation](https://developer.android.com/training/notify-user/channels). ||
|| `push_batch_request.batch.messages.android.content.priority` | Notification priority. Acceptable values are in the range of `[-2; 2]`. The platform determines the priority of messages and takes appropriate actions: interrupts the user (displays a message on the screen), or does not notify the user about the message. On different devices, priority is interpreted differently. ||
|| `push_batch_request.batch.messages.android.content.collapse_key` | Notification ID. The default value is 0. Ignored if there are no push notifications currently displayed for this application. If one or more notifications are displayed and the new message has the same notification ID, the content of this notification will be updated. If the ID is different, the new message is displayed. ||
|| `push_batch_request.batch.messages.android.content.vibration` | Vibration pattern on message arrival. Format:  `[pause in ms, duration of vibration in ms, pause in ms, duration of vibration in ms, ...]`. ||
|| `push_batch_request.batch.messages.android.content.led_color` | LED color. It is specified as a string in the format of the hex code `#RRGGBB`. ||
|| `push_batch_request.batch.messages.android.content.led_interval` | The duration of the glow of the LED indicator in ms.  ||
|| `push_batch_request.batch.messages.android.content.led_pause_interval` | Pause time for the glow of the LED indicator in ms.  ||
|| `push_batch_request.batch.messages.android.content.time_to_live` | The duration of the interval in seconds that FireBase will store the push message if the device is offline or out of range. ||
|| `push_batch_request.batch.messages.android.content.visibility` | Displaying the push message on the lock screen. Ignored on Android 8 and higher (API level 26+), where it's set at the channel level. Acceptable values: `secret`, `private`, `public`. Not set by default. For more information about the `visibility` property, see the [Android documentation](https://developer.android.com/reference/android/app/Notification#VISIBILITY_PRIVATE) ||
|| `push_batch_request.batch.messages.android.content.urgency` | Urgency (priority) of push message delivery. Acceptable values: `high`, `normal`. The default value is `high`. Urgent push messages wake up the device, launch the app in background mode, and get access to the internet for a short time. Urgent push messages are delivered faster and more reliably. For more information about [priority of FCM messages](https://firebase.google.com/docs/cloud-messaging/concept-options#setting-the-priority-of-a-message), see the [Android documentation](https://developer.android.com/training/monitoring-device-state/doze-standby#using_fcm). ||
|| `push_batch_request.batch.messages.android.open_action` | The action to be taken when a user clicks on a push notification. If the field is empty, the user click opens the application. ||
|| `push_batch_request.batch.messages.android.open_action.deeplink` | The deeplink with an application screen to take a user to after clicking on a push message. ||
|| `push_batch_request.batch.messages.ios` | The device platform. ||
|| `push_batch_request.batch.messages.ios.silent` | A flag that indicates [silent push](*silent push) sending. Possible values: `true | false`. ||
|| `push_batch_request.batch.messages.ios.contentt` | The content of the push message. ||
|| `push_batch_request.batch.messages.ios.content.title` | The title of the push message. The value is mandatory for the non-silent push messages. ||
|| `push_batch_request.batch.messages.ios.content.text` | The text of the message. The value is mandatory for the non-silent push messages. ||
|| `push_batch_request.batch.messages.ios.content.badge` | Badge number to be displayed on the application icon on message arrival. ||
|| `push_batch_request.batch.messages.ios.content.sound` | The message sound. Possible values: `default | disable` ||
|| `push_batch_request.batch.messages.ios.content.thread_id` | ID for grouping push notifications. The value is specified in the [threadIdentifier](https://developer.apple.com/documentation/usernotifications/unmutablenotificationcontent/1649872-threadidentifier?language=objc) property of the [UNNotificationContent](https://developer.apple.com/documentation/usernotifications/unnotificationcontent) object. ||
|| `push_batch_request.batch.messages.ios.content.category` | Push notifications category. The value is specified in the [identifier](https://developer.apple.com/documentation/usernotifications/unnotificationcategory/1649276-identifier?language=objc) property of the `UNNotificationCategory` object. More information about push actions and categories in the [Apple documentation](https://developer.apple.com/documentation/usernotifications/declaring_your_actionable_notification_types?language=objc). ||
|| `push_batch_request.batch.messages.ios.content.mutable_content` | Indicates Notification Service Extension. If the value is `1`, the push notification is processed by the extension. AppMetrica uses it to track the delivery of push notifications.

To track the delivery, set up [push notification statistics collection](LINK) and pass `1` as a field value. If the value is omitted, the number of delivered push notifications in reports is equal to the number of opened messages. ||
|| `push_batch_request.batch.messages.ios.content.expiration` | The duration of time to continue trying to deliver the notification to the user's device. The value should be specified in seconds.
If this time expires and the device is still unavailable (for example, it doesn't have internet access), the notification isn't delivered. By default, the time is unrestricted. ||
|| `push_batch_request.batch.messages.ios.content.data` | An arbitrary string of data. You can pass any data you need as a string value. You can process the data string by using the appropriate AppMetrica Push SDK methods. ||
|| `push_batch_request.batch.messages.ios.content.collapse_id` | Collapse ID [apns-collapse-id](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/CommunicatingwithAPNs.html#//apple_ref/doc/uid/TP40008194-CH11-SW12). Multiple notifications with the same ID are displayed to the user as a single notification. ||
|| `push_batch_request.batch.messages.ios.content.attachments` | An array of attachments to be added in a push message. Read more in the article [Step 6. (_Optional_) Configure uploading attached files](LINK). ||
|| `push_batch_request.batch.messages.ios.content.attachments.id` | ID of the push message contents. ||
|| `push_batch_request.batch.messages.ios.content.attachments.file_url` | URL of the file from the push message. ||
|| `push_batch_request.batch.messages.ios.content.attachments.file_type` | Type of the attached file in the push message. For acceptable types, see [File types in push messages](file-type.md). ||
|| `push_batch_request.batch.messages.android.open_action` | The action to be taken when a user clicks on a push notification. If the field is empty, the user click opens the application. ||
|| `push_batch_request.batch.messages.android.open_action.url` | The URL to go to when the push message is clicked. ||
|| `push_batch_request.batch.devices` | Devices to send push notifications to. Each dispatch of messages can contain up to 250,000 devices.
Devices are grouped by `id_type`. One sending can have from 1 to 5 groups. All groups can contain up to 250,000 devices in total in a single HTTP request. For example, if the `appmetrica_device_id` group contains 100,000 devices, only 150,000 can be specified in the others. ||
|| `push_batch_request.batch.devices.id_type` | The type of the ID. Acceptable values: `appmetrica_device_id`, `ios_ifa`, `google_aid`, `android_push_token`, `ios_push_token`, `huawei_push_token`, `huawei_oaid`.

{% note info %}

When you use a push token as an identifier, AppMetrica checks the presence of a token and device information in the database before sending. If there is no device information, the push message is not sent. This is necessary to control sending messages to the desired addressees and display information in the reports.

{% endnote %}
||
|| `push_batch_request.batch.devices.id_values` |List of devices to send push messages to.

{% note alert %}

The list can't be empty.

{% endnote %} ||
|#

## Response format {#response_format}

```json translate=no
{
  "push_response": {
    "transfer_id": 1,
    "client_transfer_id": long
  }
}
```

#|
|| `push_response` | The response after sending push messages. ||
|| `push_response.transfer_id` | ID of the dispatch. It is used for [checking the status of the dispatch](get-status-id.md). ||
|| `push_response.client_transfer_id` | Sending ID, specified by the user in the body of the request. It is used for [checking the status of the dispatch](get-status-group-id.md).

{% note info %}

The field is returned only if it was specified in the body of the request.

{% endnote %}
||
|#

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}

[*The sending tag]: A tag is an arbitrary string that labels every sending performed by the API. You can label an arbitrary number of sendings by one tag. The report displays tag at the second level.

[*silent push]: A message processed by the application in the background without being displayed to the user. You can transfer additional data to the application via silent push messages or check the delivery of notifications.
