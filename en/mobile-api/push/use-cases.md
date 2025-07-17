# Use cases

## Creating a group {#create}

To send a push message you should define the unique name of the group. Each sending is owned by any created group. It allows you to group message sendings in the report.

To create a group make the following request [`POST /push/v1/management/groups`](post-groups.md):

```
curl -X POST \
  '{{ push-api-url }}/push/v1/management/groups' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: OAuth <your_token>' \
  -d '{"group":{"app_id":XXXXXX,"name":"the_name_of_the_group"}}'
```

where `<your_token>` is an OAuth token that can be obtained using [instructions](../intro/authorization.md#get-oauth-token).

If the request is successful, you will receive a response that looks like:

```
{
  "group": {
    "id": XXXXXX,
    "app_id": XXXXXX,
    "name": "the_name_of_the_group"
  }
}
```

The received `group_id` must be used for further push messages sending.

## Sending a push message {#send-push}

To send a push you should specify the group ID and a dispatch tag. Multiple dispatches can have the same tag. The tag is an arbitrary string displayed in reports at the second level.

To send a push message, make the following request [`POST /push/v1/send-batch`](post-send-batch.md):

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

where `<your_token>` is an OAuth token that can be obtained using [instructions](../intro/authorization.md#get-oauth-token).

{% note info %}

The description of the request fields is given in the section [Sending push messages](post-send-batch.md).

{% endnote %}

If the request is successful, you will receive a response that looks like:

```
{
  "push_response": {
  "transfer_id": XXXXXX
  }
}
```

The recieved `transfer_id` is used to check the status of sending.

## Checking the status of sending {#check-transfer}

To check the status of sending use the `transferId` dispatch identifier.

{% note info %}

You can also check the status by using the specified value of the `client_transfer_id` field. For more information, see [Sending push messages](post-send-batch.md).

{% endnote %}

To check the status make the following request [`GET /push/v1/status/{transferId}`](get-status-id.md):

```
curl -X GET \
  '{{ push-api-url }}/push/v1/status/XXXXXX' \
  -H 'Authorization: OAuth <your_token>'
```

where `<your_token>` is an OAuth token that can be obtained using [instructions](../intro/authorization.md#get-oauth-token).

You will receive a response that looks like:

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

The description of the response fields is given in the section [Checking the status of sending with transferId](get-status-id.md).

{% endnote %}

## Getting a push campaign report {#report}

To get a push campaign report, use the [Reporting API](../api_v1/intro.md).

To get the information about sending use the following request

```
curl -X GET \
  '{{ api-url }}/stat/v1/data?limit=10&date1=today&date2=today&ids=XXXXXX&metrics=ym:pc:users&dimensions=ym:pc:group,ym:pc:tag,ym:pc:transfer'
  -H 'Authorization: OAuth <your_token>'
```

where `<your_token>` is an OAuth token that can be obtained using [instructions](../intro/authorization.md#get-oauth-token).

If the request is successful, you will receive a response that looks like:

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

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
