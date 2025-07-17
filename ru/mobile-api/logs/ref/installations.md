# Установки приложения

{{ installations }}

## Формат запроса {#request-format}

```
GET {{ api-url }}/logs/v1/export/installations.{csv | json}
  ? application_id=<int>
  & date_since=<string>
  & date_until=<string>
  & fields=<string>
  & [date_dimension=<string>]
  & [limit=<string>]
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
application_id,installation_id,attributed_touch_type,click_datetime,click_id,click_ipv6,click_timestamp,click_url_parameters,click_user_agent,profile_id,publisher_id,publisher_name,tracker_name,tracking_id,install_datetime,install_ipv6,install_receive_datetime,install_receive_timestamp,install_timestamp,is_reattribution,is_reinstallation,match_type,appmetrica_device_id,city,connection_type,country_iso_code,device_locale,device_manufacturer,device_model,device_type,google_aid,oaid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,windows_aid,app_package_name,app_version_name
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
        "installation_id": "string",
        "attributed_touch_type": "string",
        "click_datetime": "string",
        "click_id": "string",
        "click_ipv6": "string",
        "click_timestamp": "integer",
        "click_url_parameters": "string",
        "click_user_agent": "string",
        "profile_id": "string",
        "publisher_id": "integer",
        "publisher_name": "string",
        "tracker_name": "string",
        "tracking_id": "integer",
        "install_datetime": "string",
        "install_ipv6": "string",
        "install_receive_datetime": "string",
        "install_receive_timestamp": "integer",
        "install_timestamp": "integer",
        "is_reattribution": "boolean",
        "is_reinstallation": "boolean",
        "match_type": "string",
        "appmetrica_device_id": "integer",
        "city": "string",
        "connection_type": "string",
        "country_iso_code": "string",
        "device_locale": "string",
        "device_manufacturer": "string",
        "device_model": "string",
        "device_type": "string",
        "google_aid": "string",
        "oaid": "string",
        "ios_ifa": "string",
        "ios_ifv": "string",
        "mcc": "integer",
        "mnc": "integer",
        "operator_name": "string",
        "os_name": "string",
        "os_version": "string",
        "windows_aid": "string",
        "app_package_name": "string",
        "app_version_name": "string"
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
|| `installation_id` | {{ installation_id }} ||
|| `attributed_touch_type`| {{ attributed_touch_type }} ||
|| `click_datetime` | {{ click_datetime }} ||
|| `click_id` | {{ click_id }} ||
|| `click_ipv6` | {{ click_ipv6 }} ||
|| `click_timestamp` | {{ click_timestamp }} ||
|| `click_url_parameters` | {{ click_url_parameters }} ||
|| `click_user_agent` | {{ click_user_agent }} ||
|| `profile_id` | {{ profile_id }} ||
|| `publisher_id` | {{ publisher_id }} ||
|| `publisher_name` | {{ publisher_name }} ||
|| `tracker_name` | {{ tracker_name }} ||
|| `tracking_id` | {{ tracking_id }} ||
|| `install_datetime` | {{ install_datetime }} ||
|| `install_ipv6` | {{ install_ipv6 }} ||
|| `install_receive_datetime` | {{ install_receive_datetime }} ||
|| `install_receive_timestamp` | {{ install_receive_timestamp }} ||
|| `install_timestamp` | {{ install_timestamp }} ||
|| `is_reattribution` | {{ is_reattribution }} ||
|| `is_reinstallation` | {{ is_reinstallation }} ||
|| `match_type` | [Способ атрибуции](../../../mobile-tracking/technology.md): `fingerprint` \| `referrer` \| `identifier` \| `''` (пустая строка). ||
|| `appmetrica_device_id` | {{ appmetrica_device_id }} ||
|| `city` | {{ city }} ||
|| `connection_type` | {{ connection_type }} ||
|| `country_iso_code` | {{ country_iso_code }} ||
|| `device_locale` | {{ device_locale }} ||
|| `device_manufacturer` | {{ device_manufacturer }} ||
|| `device_model` | {{ device_model }} ||
|| `device_type` | {{ device_type }} ||
|| `google_aid` | {{ google_aid }} ||
|| `oaid` | {{ oaid }} ||
|| `ios_ifa` | {{ ios_ifa }} ||
|| `ios_ifv` | {{ ios_ifv }} ||
|| `mcc` | {{ mcc }} ||
|| `mnc` | {{ mnc }} ||
|| `operator_name` | {{ operator_name }} ||
|| `os_name` | {{ os_name }} ||
|| `os_version` | {{ os_version }} ||
|| `windows_aid` | {{ windows_aid }} ||
|| `app_package_name` | {{ app_package_name }} ||
|| `app_version_name` | {{ app_version_name }} ||
|#

## Пример {#example}

Запрос:

```bash translate=no
curl -X GET \
  '{{ api-url }}/logs/v1/export/installations.json?application_id=1111&date_since=2018-10-10&date_until=2018-10-11&fields=application_id,installation_id,attributed_touch_type,click_datetime,click_id,click_ipv6,click_timestamp,click_url_parameters,click_user_agent,profile_id,publisher_id,publisher_name,tracker_name,tracking_id,install_datetime,install_ipv6,install_receive_datetime,install_receive_timestamp,install_timestamp,is_reattribution,is_reinstallation,match_type,appmetrica_device_id,city,connection_type,country_iso_code,device_locale,device_manufacturer,device_model,device_type,google_aid,oaid,ios_ifa,ios_ifv,mcc,mnc,operator_name,os_name,os_version,windows_aid,app_package_name,app_version_name' \
  -H 'Authorization: OAuth oauth_token'
```

Ответ:

```json translate=no
{
  "data": [
    {
      "application_id": "1111",
      "installation_id": "fdfssd23432",
      "attributed_touch_type": "click",
      "click_datetime": "yyyy-mm-dd hh:mm:ss",
      "click_id": "f2ae4254de8844dda58b29cac2cf0e87",
      "click_ipv6": "::ffff:5.255.232.147",
      "click_timestamp": "1556258660",
      "click_url_parameters": "click_id=f2ae4254de8844dda58b29cac2cf0e87&c=1234&google_aid=&google_aid_sha1=&google_aid_md5=&ios_ifa=&ios_ifa_sha1=&ios_ifa_md5&click_timestamp=1554824136&afpub_id=&site_id=&creative_id=&goal_id1=&goal_id2 ",
      "click_user_agent": "Mozilla/5.0 (iPhone; CPU iPhone OS 12_2 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.1 Mobile/15E148 Safari/604.1",
      "profile_id": "test",
      "publisher_id": "39",
      "publisher_name": "AdColony",
      "tracker_name": "Advertising iOS campaign",
      "tracking_id": "12345678901234567890",
      "install_datetime": "yyyy-mm-dd hh:mm:ss",
      "install_ipv6": "::ffff:5.255.232.147",
      "install_receive_datetime": "yyyy-mm-dd hh:mm:ss",
      "install_receive_timestamp": "1556258667",
      "install_timestamp": "1556258660",
      "is_reattribution": "false",
      "is_reinstallation": "false",
      "match_type": "fingerprint",
      "appmetrica_device_id": "123456789012345678",
      "city": "Moscow",
      "connection_type": "wifi",
      "country_iso_code": "RU",
      "device_locale": "ru_RU",
      "device_manufacturer": "Apple",
      "device_model": "iPhone X",
      "device_type": "phone",
      "google_aid": "",
      "oaid": "",
      "ios_ifa": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "ios_ifv": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "mcc": "250",
      "mnc": "1",
      "operator_name": "MTS RUS",
      "os_name": "ios",
      "os_version": "12.2",
      "windows_aid": "",
      "app_package_name": "ru.yandex.metro",
      "app_version_name": "1.0"
    }
  ]
}
```

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
