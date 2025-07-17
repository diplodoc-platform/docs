# S2S интеграция

Ряд рекламных сетей поддерживает server-to-server (S2S) интеграцию с AppMetrica. При S2S интеграции пользователь, переходящий по рекламному размещению, перенаправляется напрямую в магазин приложений. При этом рекламная сеть выполняет «показ» или «клик» — вызов соответствующей трекинговой ссылки. Этот вызов происходит с сервера рекламной сети. 

{% note info %}

В атрибуции участвуют показы и клики, отправленные в AppMetrica не позднее, чем через 12 часов после события.

{% endnote %}

Прямой переход пользователя в магазин приложений (без дополнительного редиректа) в некоторых случаях позволяет повысить конверсию.

Для корректной работы трекинга при использовании этого механизма рекламная сеть должна выполнить переход по трекинговой ссылке, как это сделал бы браузер пользователя. Чтобы передать данные, необходимые для атрибуции установки, добавьте указанные ниже параметры в tracking URL / impression URL, а также в итоговую посадочную страницу.

## Параметры в tracking URL/ impression URL {#tracking-url}

#|
|| 
**Параметр** | **Обязательный** | **Пример** | **Описание** 
||
|| 
`device_ip` | Да | device_ip=192.0.2.0/24 | URL-encoded IP адрес устройства пользователя. Поддерживаются IPv4 и IPv6
||
|| 
`device_ua` | Да | device_ua=... | URL-encoded User-Agent устройства пользователя
||
|| 
`click_timestamp` | Да | click_timestamp=1453895044 | UTC timestamp клика в секундах
||
|| 
`noredirect` | Нет | noredirect=1 | Cообщает в AppMetrica, что надо учесть клик, но не надо перенаправлять на магазин приложений. Значение по умолчанию — 1
||
|| 
`click_id` | Нет | click_id=123456789 | Уникальный идентификатор клика. В том числе используется для корректной работы [InstallReferrer](technology.md#install-referrer)
||
||
`external_click_id` | Нет | external_click_id=123456789 | Дополнительный уникальный идентификатор клика.  Применяется для атрибуции по технологии [InstallReferrer](technology.md#install-referrer), когда нет возможности передавать `click_id`
||
||
`google_aid` | Нет | google-aid=8e4dd44b-82ec-43d0-a5de-321...... | Google AID, в формате, как был получен с устройства
||
|| 
`idfa` | Нет | idfa=30255BCE-4CDA-4F62–91DC-475.......... | IFA в формате, как был получен с устройства
||
||
`oaid` | Нет | oaid=1fe9a970-efbb-29e0-0bdd-f5.......... | Huawei OAID, в формате, как был получен с устройства
||
|#

Вы можете использовать [дополнительные параметры](tracking-specification.md) для идентификации устройства.

##  Параметры в итоговую посадочную страницу {#landing}
 
Необходимо передать параметр `referrer` с парой значений `appmetrica_click_id={click_id}` или `appmetrica_click_id={external_click_id}`.

Пример:

```
play.google.com/store/apps/details?hl=ru&gl=ru&id=com.non.noncalendar&referrer=appmetrica_click_id%3D123456789
```
{% note info "" %}

Для корректной работы атрибуции по технологии InstallReferrer необходимо передавать значения `click_id` (или `external_click_id`) как в целевой ссылке, так и в GET-запросе. Поэтому мы советуем реализовать этот способ передачи данных.

{% endnote %}

Пример для InstallReferrer:

- Параметр в refferer

    ```
    play.google.com/store/apps/details?hl=ru&gl=ru&id=com.non.noncalendar&referrer=appmetrica_click_id%3D123456789
    ```

- Параметр в GET-запросе

    ```httpget translate=no
    GET redirect.appmetrica.yandex.com/serve/TRACKING_ID?click_id=123456789&external_click_id=987654321&device_ip=192.0.2.0/24&device_ua=Mozilla/5.0%20
    (Linux;%20Android%204.4.4;%205042D%20Build/KTU84P)%20AppleWebKit/537.36%20(KHTML,%20like%20Gecko)%20Version/4.0%20Chrome/33.0.0.0%20Mobile%20Safari/537.36&click_timestamp=1453895044&noredirect
    ```

## Пример запроса {#example}

Для кликов:
 
```httpget translate=no
GET redirect.appmetrica.yandex.com/serve/TRACKING_ID?click_id=123456789&external_click_id=987654321&device_ip=192.0.2.0/24&device_ua=Mozilla/5.0%20
(Linux;%20Android%204.4.4;%205042D%20Build/KTU84P)%20AppleWebKit/537.36%20(KHTML,%20like%20Gecko)%20Version/4.0%20Chrome/33.0.0.0%20Mobile%20Safari/537.36&click_timestamp=1453895044&noredirect
```
 
где `TRACKING_ID` — идентификатор трекера в AppMetrica (присутствует в tracking URL пользователя).
 
Для показов:
 
```httpget translate=no
GET impression.appmetrica.yandex.com/serve/TRACKING_ID?click_id=123456789&external_click_id=987654321&device_ip=192.0.2.0/24&device_ua=Mozilla/5.0%20
(Linux;%20Android%204.4.4;%205042D%20Build/KTU84P)%20AppleWebKit/537.36%20(KHTML,%20like%20Gecko)%20Version/4.0%20Chrome/33.0.0.0%20Mobile%20Safari/537.36&click_timestamp=1453895044&noredirect
```
 
где `TRACKING_ID` — идентификатор трекера в AppMetrica (присутствует в impression URL пользователя).

HTTP-код ответа AppMetrica на такие запросы: 204 No Content.

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
