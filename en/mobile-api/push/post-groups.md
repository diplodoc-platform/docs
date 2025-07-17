# Creating a group

Creates a [group](*group) for sending push messages to the specified application.

## Request format {#request-format}

```
POST {{ push-api-url }}/push/v1/management/groups
```

## Request body

```json translate=no
{
  "group": {
    "app_id": int,
    "name": "string",
    "send_rate": int
  }
}
```

#|
|| `group` | {{ push-group }} ||
|| `group.app_id`* | {{ push-app_id }} ||
|| `group.name`* | {{ push-name }} ||
|| `group.send_rate` | {{ push-send_rate }} ||
|#

## Response format {#response-format}

```json translate=no
{
  "group": {
    "id": int,
    "app_id": int,
    "name": "string",
    "send_rate": int
  }
}
```
#|
|| `group` | {{ push-group }} ||
|| `group.id` | {{ push-id }} ||
|| `group.app_id` | {{ push-app_id }} ||
|| `group.name` | {{ push-name }} ||
|| `group.send_rate` | {{ push-send_rate }} ||
|#

## Sample request

> ```bash translate=no
> curl -X POST \
>   {{ push-api-url }}/push/v1/management/groups \
>   -H 'Authorization: OAuth AQAAAAAR62cMAAQgnh4fTgjnrEH...' \
>   -H 'Content-Type: application/json' \
>   -d '{
>   "group": {
>     "app_id": XXXXXX,
>     "name": "group-name",
>     "send_rate": 200
>   }
> }'
> ```

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}

[*group]: A group is a container for sending push messages. It allows grouping messages sendings in the [push campaign report](../../mobile-reports/push-campaign.md). The group can contain an arbitrary number of sendings. The push campaign report displays these groups at the first level along with push campaigns that are launched through the [web interface](../../push/marketing.md).
