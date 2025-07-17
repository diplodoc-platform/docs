# Postbacks

{{ postbacks }}

## Request format {#request-format}

```
GET {{ api-url }}/logs/v1/export/postbacks.{csv | json}
  ? application_id=<int>
  & date_since=<string>
  & date_until=<string>
  & fields=<string>
  & [limit=<int>]
  & [use_utf8_bom=<bool>]
  & [<any field name>=<string>]
```

#|
|| `application_id`* | {{ application_id_query }} ||
|| `date_since`* | {{ date_since-query-postback }} ||
|| `date_until`* | {{ date_until-query-postback }} ||
|| `fields`* | A comma-separated [list of fields](../endpoints.md) for the sample.

A list that contains all available fields (for quick copy):

```objectivec translate=no
application_id,attributed_touch_type,click_datetime,click_id,click_ipv6,click_timestamp,click_url_parameters,click_user_agent,publisher_id,publisher_name,tracker_name,tracking_id,install_datetime,install_ipv6,install_timestamp,match_type,appmetrica_device_id,device_locale,device_manufacturer,device_model,device_type,google_aid,oaid,ios_ifa,os_name,os_version,windows_aid,app_package_name,app_version_name,conversion_datetime,conversion_timestamp,event_name,attempt_datetime,attempt_timestamp,cost_model (postback_type),notifying_status,postback_url,postback_url_parameters,response_body,response_code
```
||
|| `limit` | {{ limit-query }} ||
|| `use_utf8_bom` | {{ use_utf8_bom-query }} ||
|| `<any field name>` | {{ any-field-name-query }} ||
|#

## Response format {#response-format}

If all available fields are requested:

{% list tabs %}

- JSON

   ```json translate=no
   {
     "data": [
       {
         "application_id": "integer",
         "attributed_touch_type": "string",
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
         "install_datetime": "string",
         "install_ipv6": "string",
         "install_timestamp": "integer",
         "match_type": "string",
         "appmetrica_device_id": "integer",
         "device_locale": "string",
         "device_manufacturer": "string",
         "device_model": "string",
         "device_type": "string",
         "google_aid": "string",
         "oaid": "string",
         "ios_ifa": "string",
         "ios_ifv": "string",
         "os_name": "string",
         "os_version": "string",
         "windows_aid": "string",
         "app_package_name": "string",
         "app_version_name": "string",
         "conversion_datetime": "string",
         "conversion_timestamp": "integer",
         "event_name": "string",
         "attempt_datetime": "string",
         "attempt_timestamp": "integer",
         "cost_model": "string",
         "notifying_status": "string",
         "postback_url": "string",
         "postback_url_parameters": "string",
         "response_body": "string",
         "response_code": "integer"
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
|| `attributed_touch_type` | {{ attributed_touch_type }} ||
|| `click_datetime` | {{ click_datetime }} ||
|| `click_id` | {{ click_id }} ||
|| `click_ipv6` | {{ click_ipv6 }} ||
|| `click_timestamp` | {{ click_timestamp }} ||
|| `click_url_parameters` | {{ click_url_parameters }} ||
|| `click_user_agent` | {{ click_user_agent }} ||
|| `publisher_id` | {{ publisher_id_postback }} ||
|| `publisher_name` | {{ publisher_name_postback }} ||
|| `tracker_name` | {{ tracker_name_postback }} ||
|| `tracking_id` | {{ tracking_id_postback }} ||
|| `install_datetime` | {{ install_datetime }} ||
|| `install_ipv6` | {{ install_ipv6 }} ||
|| `install_timestamp` | {{ install_timestamp }} ||
|| `match_type` | [Attribution method](../../../mobile-tracking/technology.md): `fingerprint` \| `referrer` \| `identifier` \| `''` (empty string). ||
|| `appmetrica_device_id` | {{ appmetrica_device_id }} ||
|| `device_locale` | {{ device_locale }} ||
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
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|| `conversion_datetime` | {{ conversion_datetime }} ||
|| `conversion_timestamp` | {{ conversion_timestamp }} ||
|| `event_name` | {{ event_name }} ||
|| `attempt_datetime` | {{ attempt_datetime }} ||
|| `attempt_timestamp` | {{ attempt_timestamp }} ||
|| `cost_model` | {{ cost_model }} ||
|| `notifying_status` | {{ notifying_status }} ||
|| `postback_url` | {{ postback_url }} ||
|| `postback_url_parameters` | {{ postback_url_parameters }} ||
|| `response_body` | {{ response_body }} ||
|| `response_code` | {{ response_code }} ||
|#

## Example {#example}

Request:

```bash translate=no
curl -X GET \
  '{{ api-url }}/logs/v1/export/postbacks.json?application_id=1111&date_since=2018-10-10&date_until=2018-10-11&fields=application_id,attributed_touch_type,click_datetime,click_id,click_ipv6,click_timestamp,click_url_parameters,click_user_agent,publisher_id,publisher_name,tracker_name,tracking_id,install_datetime,install_ipv6,install_timestamp,match_type,appmetrica_device_id,device_locale,device_manufacturer,device_model,device_type,google_aid,oaid,ios_ifa,ios_ifv,os_name,os_version,windows_aid,app_package_name,app_version_name,conversion_datetime,conversion_timestamp,event_name,attempt_datetime,attempt_timestamp,cost_model,notifying_status,postback_url,postback_url_parameters,response_body,response_code' \
  -H 'Authorization: OAuth oauth_token'
```

Response:

```json translate=no
{
  "data": [
    {
      "application_id": "1111",
      "attributed_touch_type": "click",
      "click_datetime": "yyyy-mm-dd hh:mm:ss",
      "click_id": "f2ae4254de8844dda58b29cac2cf0e87",
      "click_ipv6": "::ffff:5.255.232.147",
      "click_timestamp": "1556258660",
      "click_url_parameters": "click_id=f2ae4254de8844dda58b29cac2cf0e87&c=1234&google_aid=&google_aid_sha1=&google_aid_md5=&ios_ifa=&ios_ifa_sha1=&ios_ifa_md5&click_timestamp=1554824136&afpub_id=&site_id=&creative_id=&goal_id1=&goal_id2 ",
      "click_user_agent": "Mozilla/5.0 (iPhone; CPU iPhone OS 12_2 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.1 Mobile/15E148 Safari/604.1",
      "publisher_id": "39",
      "publisher_name": "AdColony",
      "tracker_name": "Advertising iOS campaign",
      "tracking_id": "12345678901234567890",
      "install_datetime": "yyyy-mm-dd hh:mm:ss",
      "install_ipv6": "::ffff:5.255.232.147",
      "install_timestamp": "1556258660",
      "match_type": "fingerprint",
      "appmetrica_device_id": "123456789012345678",
      "device_locale": "ru_RU",
      "device_manufacturer": "Apple",
      "device_model": "iPhone X",
      "device_type": "phone",
      "google_aid": "",
      "oaid": "",
      "ios_ifa": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "ios_ifv": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "os_name": "ios",
      "os_version": "12.2",
      "windows_aid": "",
      "app_package_name": "ru.yandex.metro",
      "app_version_name": "1.0",
      "conversion_datetime": "yyyy-mm-dd hh:mm:ss",
      "conversion_timestamp": "1556258660",
      "event_name": "New person",
      "attempt_datetime": "yyyy-mm-dd hh:mm:ss",
      "attempt_timestamp": "1556258660",
      "cost_model": "cpi",
      "notifying_status": "sent",
      "postback_url": "https://adcolony.servecvr.com/?transaction_id=f2ae4254de8844dda58b29cac2cf0e87",
      "postback_url_parameters": "transaction_id=f2ae4254de8844dda58b29cac2cf0e87",
      "response_body": "SUCCESS",
      "response_code": "200"
    }
  ]
}
```

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
