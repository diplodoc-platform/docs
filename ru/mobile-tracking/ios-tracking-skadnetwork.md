# Интеграция для рекламных сетей в рамках SKAdNetwork

AppMetrica может принимать от рекламных сетей постбеки, полученные от Apple в рамках SKAdNetwork. Такое решение позволяет:

- рекламным партнерам масштабировать единое решение на все трекеры (MMP) без дополнительных доработок на своей стороне;
- рекламодателям объективно оценивать результаты кампаний с учетом пользователей, которые запретили отслеживание.

## Принцип работы {#operation-principle}

1. Apple присылает SKAd-постбек в рекламную сеть.
2. Рекламная сеть пересылает в AppMetrica постбек без изменений или обогащенный внутренними параметрами (например, наименованием или id кампании).
3. AppMetrica отображает данные в отчете User Acquisition SKAdNetwork.

## Формат запроса {#query-format}

Авторизационный токен не требуется.

Предоставление IP адресов для включения в whitelist не требуется.

`POST https://skadnet-postback.yandex.net/postback`

`Content-Type: application/json`

## Параметры запроса {#params}

Ниже описаны параметры запроса интеграции рекламных сетей с AppMetrica с использованием SkAdNetwork.

| Параметр | Обязательный | Формат | Описание / Пример | Источник |
| -------- | ------------ | ------ | ----------------- | -------- |
| `version` | Да | String | 2.0 | SKAd |
| `ad-network-id` | Да | String | Abc123.skadnetwork | SKAd |
| `campaign-id` | Да | Integer | 42 | SKAd |
| `transaction-id` | Да | String | 68eb3d91-15f5-44ee-9267-25c7655c20b6 | SKAd |
| `app-id` | Да | Integer | 472650686 | SKAd |
| `attribution-signature` | Да | String |  | SKAd |
| `redownload` | Нет | Boolean |  | SKAd |
| `source-app-id` | Нет | Integer | 1050704155 | SKAd |
| `conversion-value` | Нет | Integer | 0-63 | SKAd |
| `fidelity-type` | Нет | Integer | 0 or 1, required since version 2.2 | SKAd |
| `ad-network-campaign-id` | Нет | String | Internal campaign id | Network |
| `ad-network-campaign-name` | Нет | String | Internal campaign name | Network |
| `ad-network-adset-id` | Нет | String | Internal adset id | Network |
| `ad-network-adset-name` | Нет | String | Internal adset name | Network |
| `ad-network-ad-id` | Нет | String | Internal ad id | Network |
| `ad-network-ad-name` | Нет | String | Internal ad name | Network |
| `ip` | Нет | String | IP of device, may be used for location (ipv4 / ipv6) | Network |
| `timestamp` | Нет | String | Time the network received postback from Apple (unix timestamp) | Network |
| `timestamp` | Нет | String | Time the network received postback from Apple (unix timestamp) | Network |

Разрешено передавать дополнительные параметры, которых нет в таблице, но они не будут отображаться в отчете User Acquisition SKAdNetwork.

## HTTP-код ответа {#responce}

`200 OK` — Запрос выполнен успешно.

`400 Bad request` — Один из параметров запроса имеет недопустимое значение или формат данных.

## Рекламные партнеры AppMetrica {#partners-list}

AppMetrica поддерживает SKAdNetwork и интегрирована со следующими рекламными партнерами:

- AdColony
- Hybrid
- Spyke Media
- Яндекс
- AdTiming
- Unity Ads
- {% if locale == "ru" %}VK Реклама{% else %}VK Ads{% endif %}

Если вы не нашли нужного рекламного партнера, то можете настроить передачу всех SKAdNetwork-постбеков в AppMetrica по [инструкции](ios15-tracking.md).

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
