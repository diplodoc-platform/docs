# Трекинговые клики и показы

{{ clicks }}

## Формат запроса {#request-format}

```
GET {{ api-url }}/logs/v1/export/clicks.{csv | json}
  ? application_id=<int>
  & date_since=<string>
  & date_until=<string>
  & fields=<string>
  & [date_dimension=<string>]
  & [limit=<int>]
  & [use_utf8_bom=<bool>]
  & [<any field name>=<string>]
```

#|
|| `application_id`* | {{ application_id_query }} ||
|| `date_since`* | {{ date_since-query }} ||
|| `date_until`* | {{ date_until-query }} ||
|| `fields`* | Разделенный запятой [список полей](../endpoints.md) для выборки.

Список, который содержит все доступные поля (для быстрого копирования):

```objectivec translate=no
application_id,click_datetime,click_id,click_ipv6,click_timestamp,click_url_parameters,click_user_agent,publisher_id,publisher_name,tracker_name,tracking_id,touch_type,is_bot,city,country_iso_code,device_manufacturer,device_model,device_type,google_aid,oaid,ios_ifa,ios_ifv,os_name,os_version,windows_aid
``` ||
|| `date_dimension` | {{ date_dimension-query }} ||
|| `limit` | {{ limit-query }} ||
|| `use_utf8_bom` | {{ use_utf8_bom-query }} ||
|| `<any field name>` | {{ any-field-name-query }} ||
|#

## Формат ответа {#response-format}

В случае, если запрашиваются все доступные поля:

{% list tabs %}

- JSON
  
  ```json translate=no
  {
    "data": [
      {
        "application_id": "integer",
        "touch_type": "string",
        "click_datetime": "string",
        "click_id": "string",
        "click_ipv6": "string",
        "click_timestamp": "integer",
        "click_url_parameters": "string",
        "click_user_agent": "string",
        "publisher_id": "integer",
        "publisher_name": "string",
        "tracker_name": "string",
        "tracking_id": "integer",
        "city": "string",
        "country_iso_code": "string",
        "device_type": "string",
        "device_model": "string",
        "device_manufacturer": "string",
        "os_version": "string",
        "os_name": "string",
        "windows_aid": "string",
        "google_aid": "string",
        "oaid": "string",
        "ios_ifv": "string",
        "ios_ifa": "string",
        "is_bot": "boolean"
      },
      ...
    ]
  }
  ```

- CSV

  ```
  application_id,ios_ifa,os_name,...
  1111,024AE7EB-4128-4237-9803-D24950323D4D,ios,...
  1111,3A86D5E8-1985-4A23-B147-5A1C0CF8781E,ios,...
  1111,,android
  ...
  ```

{% endlist %}

#|
|| `application_id` | {{ application_id }} ||
|| `touch_type` | {{ touch_type }} ||
|| `click_datetime` | {{ click_datetime }} ||
|| `click_id` | {{ click_id }} ||
|| `click_ipv6` | {{ click_ipv6 }} ||
|| `click_timestamp` | {{ click_timestamp }} ||
|| `click_url_parameters` | {{ click_url_parameters }} ||
|| `click_user_agent` | {{ click_user_agent }} ||
|| `publisher_id` | {{ publisher_id }} ||
|| `publisher_name` | {{ publisher_name }} ||
|| `tracker_name` | {{ tracker_name }} ||
|| `tracking_id` | {{ tracking_id }} ||
|| `city` | {{ city }} ||
|| `country_iso_code` | {{ country_iso_code }} ||
|| `device_manufacturer` | {{ device_manufacturer }} ||
|| `device_model` | {{ device_model }} ||
|| `device_type` | {{ device_type }} ||
|| `google_aid` | {{ google_aid }} ||
|| `oaid` | {{ oaid }} ||
|| `ios_ifa` | {{ ios_ifa }} ||
|| `ios_ifv` | {{ ios_ifv }} ||
|| `os_name` | {{ os_name }} ||
|| `os_version` | {{ os_version }} ||
|| `windows_aid` | {{ windows_aid }} ||
|| `is_bot` | {{ is_bot }} ||
|#

## Пример {#example}

Запрос:

```bash translate=no
curl -X GET \
  '{{ api-url }}/logs/v1/export/clicks.json?application_id=1111&date_since=2018-10-10&date_until=2018-10-11&fields=application_id,touch_type,click_datetime,click_id,click_ipv6,click_timestamp,click_url_parameters,click_user_agent,publisher_id,publisher_name,tracker_name,tracking_id,city,country_iso_code,device_type,device_model,device_manufacturer,os_version,os_name,windows_aid,google_aid,oaid,ios_ifv,ios_ifa,is_bot' \
  -H 'Authorization: OAuth oauth_token'
```

Ответ:

```json translate=no
{
  "data": [
    {
      "application_id": "1111",
      "touch_type": "click",
      "click_datetime": "yyyy-mm-dd hh:mm:ss",
      "click_id": "f2ae4254de8844dda58b29cac2cf0e87",
      "click_ipv6": "::ffff:5.255.232.147",
      "click_timestamp": "1556258660",
      "click_timestamp": "1556258660",
      "click_url_parameters": "click_id=f2ae4254de8844dda58b29cac2cf0e87&c=1234&google_aid=&google_aid_sha1=&google_aid_md5=&ios_ifa=&ios_ifa_sha1=&ios_ifa_md5&click_timestamp=1554824136&afpub_id=&site_id=&creative_id=&goal_id1=&goal_id2 ",
      "click_user_agent": "Mozilla/5.0 (iPhone; CPU iPhone OS 12_2 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.1 Mobile/15E148 Safari/604.1",
      "publisher_id": "39",
      "publisher_name": "AdColony",
      "tracker_name": "Advertising iOS campaign",
      "tracking_id": "12345678901234567890",
      "city": "Moscow",
      "country_iso_code": "RU",
      "device_type": "phone",
      "device_model": "iPhone X",
      "device_manufacturer": "Apple",
      "os_version": "12.2",
      "os_name": "ios",
      "windows_aid": "",
      "google_aid": "",
      "oaid": "",
      "ios_ifv": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "ios_ifa": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "is_bot": "false"
    }
  ]
}
```

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
