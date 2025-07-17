# S2S integration

A number of advertising networks support "server-to-server" (S2S) integration with AppMetrica. With S2S integration, ad traffic is redirected directly to the app store. In that case, the advertising network records the "impression" or "click" by calling the tracking link. This call comes from the advertising network's server. 

{% note info %}

The attribution includes impressions and clicks sent to AppMetrica no later than 12 hours after the event.

{% endnote %}

Sending the user directly to the app store (without an additional redirect) sometimes improves the conversion rate.

For tracking to work correctly when using this method, the advertising network must make the transition using the tracking link, as the user's browser would have. To transmit the data required for attribution of the installation, add the following parameters to the tracking URL/impression URL, as well as to the final landing page.

## To the tracking URL/impression URL {#tracking-url}
 
#|
||
**Parameter** | **Required** | **Example** | **Description**
||
||
`device_ip` | Yes | device_ip=192.0.2.0/24 | URL-encoded IP address of the user's device. IPv4 and IPv6 are supported
||
||
`device_ua` | Yes | device_ua=... | URL-encoded User-Agent on the user's device
||
||
`click_timestamp` | Yes | click_timestamp=1453895044 | UTC timestamp of the click, in seconds
||
||
`noredirect` | No | noredirect=1 | Notifies AppMetrica that the click should be counted without redirection to the app store. The default value is 1
||
||
`click_id` | No | click_id=123456789 | Unique click ID. Also enables the correct operation of [InstallReferrer](technology.md#install-referrer)
||
||
`external_click_id` | No | external_click_id=123456789 | An additional unique click ID. It is used for attribution using the [InstallReferrer](technology.md#install-referrer) technology when it is not possible to transmit the `click_id`
||
||
`google_aid` | No | google-aid=8e4dd44b-82ec-43d0-a5de-321...... | Google AID, exactly as received from the device
||
||
`idfa` | No | idfa=30255BCE-4CDA-4F62–91DC-475.......... | IFA, exactly as received from the device
||
||
`oaid` | No | oaid=1fe9a970-efbb-29e0-0bdd-f5.......... | Huawei OAID, exactly as received from the device
||
|#

You can use the [additional parameters](tracking-specification.md) for device identification.

## To the resulting landing page {#landing}
 
Pass the `referrer` parameter with the pair of values `appmetrica_click_id={click_id}` or `appmetrica_click_id={external_click_id}`.

Example:

```
play.google.com/store/apps/details?hl=ru&gl=ru&id=com.non.noncalendar&referrer=appmetrica_click_id%3D123456789
```

{% note info "" %}

For correct InstallReferrer attribution, pass `click_id` (or `external_click_id`) both in the destination URL and in the GET request. To do this, we recommend implementing the following method of data transfer.

{% endnote %}

Example for InstallReferrer:

- Parameter in the referrer

    ```
    play.google.com/store/apps/details?hl=ru&gl=ru&id=com.non.noncalendar&referrer=appmetrica_click_id%3D123456789
    ```

- Parameter in the GET request

    ```httpget translate=no
    GET redirect.appmetrica.yandex.com/serve/TRACKING_ID?click_id=123456789&external_click_id=987654321&device_ip=192.0.2.0/24&device_ua=Mozilla/5.0%20
    (Linux;%20Android%204.4.4;%205042D%20Build/KTU84P)%20AppleWebKit/537.36%20(KHTML,%20like%20Gecko)%20Version/4.0%20Chrome/33.0.0.0%20Mobile%20Safari/537.36&click_timestamp=1453895044&noredirect
    ```

## Sample request {#example}

For clicks:

```httpget translate=no
GET redirect.appmetrica.yandex.com/serve/TRACKING_ID?click_id=123456789&external_click_id=987654321&device_ip=192.0.2.0/24&device_ua=Mozilla/5.0%20
(Linux;%20Android%204.4.4;%205042D%20Build/KTU84P)%20AppleWebKit/537.36%20(KHTML,%20like%20Gecko)%20Version/4.0%20Chrome/33.0.0.0%20Mobile%20Safari/537.36&click_timestamp=1453895044&noredirect
```

where `TRACKING_ID` is the ID of the tracker in AppMetrica (present in the user's tracking URL).

For impressions:

```httpget translate=no
GET impression.appmetrica.yandex.com/serve/TRACKING_ID?click_id=123456789&external_click_id=987654321&device_ip=192.0.2.0/24&device_ua=Mozilla/5.0%20
(Linux;%20Android%204.4.4;%205042D%20Build/KTU84P)%20AppleWebKit/537.36%20(KHTML,%20like%20Gecko)%20Version/4.0%20Chrome/33.0.0.0%20Mobile%20Safari/537.36&click_timestamp=1453895044&noredirect
```

Where `TRACKING_ID` is the ID of the tracker in AppMetrica (part of the user's tracking URL).

The HTTP response code from AppMetrica for requests in those cases is 204 No Content.

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
