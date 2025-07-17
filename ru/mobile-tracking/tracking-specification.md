# Параметры трекинг-ссылки

Ниже представлено описание структуры и параметров трекинг-ссылки AppMetrica.

## Структура {#structure}

```no-highlight translate=no
https://[redirect|impression].appmetrica.yandex.com/serve/[tracking ID — идентификатор трекера]
```

Домен `redirect.appmetrica.yandex.com` используется для атрибуции кликов, а `impression.appmetrica.yandex.com` — для показов.

Пример:

```no-highlight translate=no
https://redirect.appmetrica.yandex.com/serve/1019409635088005254
```

`redirect.appmetrica.yandex.com` — основной домен, который используется в данное время. Возможные варианты:

- `appmetrika.yandex.com`
- `appmetrica.yandex.ru`
- `appmetrika.yandex.ru`

Трекинг-ссылка может содержать предопределенные параметры, которые необходимы для работы трекинга. Рекламная система (партнер AppMetrica) должна передавать определенные значения через эти параметры. Для упрощения этого процесса AppMetrica предоставляет макросы различных рекламных партнеров для подстановки в параметры. Например:

AppMetrica хранит `macros-params` соответствия для **Партнера A**:

- `click_id — {transaction_id}`
- `google_aid — {GAID}`

Трекинг-ссылка полученная для **Партнера A**:

```
https://redirect.appmetrica.yandex.com/serve/1019409635088005254?click_id={transaction_id}&google_aid={GAID}
```

Пользователю необходимо предоставить эту трекинг-ссылку Партнеру A. Трекинг начнет работать автоматически.

## Параметры {#params}

Параметры разделены на категории: обязательные, рекомендованные, необязательные. Обратите внимание на дополнительные параметры для S2S вызова.

### Обязательные {#required-params}

`click_id={YOURMACRO}&` — макрос для передачи уникального `click ID`. Используется для дедубликации.

### Рекомендованные {#recommended-params}

Параметры для более точного учета установок.

`google_aid={YOURMACRO}&` — Google AID, в формате, как был получен с устройства.

`google_aid_sha1={YOURMACRO}&` — SHA1 хэш от Google AID.

`google_aid_md5={YOURMACRO}&` — MD5 хэш от Google AID.

`ios_ifa={YOURMACRO}&` — IFA в формате, как был получен с устройства.

`ios_ifa_sha1={YOURMACRO}&` — SHA1 хэш от IFA.

`ios_ifa_md5={YOURMACRO}&` — MD5 хэш от IFA.

`oaid={YOURMACRO}&` — Huawei OAID, в формате, как был получен с устройства.

`oaid_sha1={YOURMACRO}&` — SHA1 хэш от Huawei OAID.

`oaid_md5={YOURMACRO}&` — MD5 хэш от Huawei OAID.

`windows_aid = {YOURMACRO}&` — Windows AID в формате, как был получен с устройства.

`windows_aid_sha1={YOURMACRO}&` — SHA1 хэш от Windows AID.

`windows_aid_md5={YOURMACRO}&` — MD5 хэш от Windows AID.

### Параметры для S2S вызова {#s2s-params}

`device_ip={YOURMACRO}&` — URL-encoded IP адрес устройства. Поддерживаются IPv4 и IPv6.

`device_ua={YOURMACRO}&` — URL-encoded User-Agent устройства.

`click_timestamp={YOURMACRO}&` — UTC timestamp клика в секундах.

`noredirect={YOURMACRO}&` — Cообщает в AppMetrica, что надо учесть клик, но не надо перенаправлять на магазин приложений. Значение по умолчанию равно 1.

Подробнее о s2s интеграции в разделе [S2S интеграция](s2s.md).

### Необязательные {#optional-params}

Параметры для оптимизации кампаний. Переданные параметры отображаются в виде дерева в отчете [Источники трафика](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&report=campaigns2&metrics=ym_m_advInstallDevicesFake&sampling=medium).

`afpub_id={YOURMACRO}&` — ID аффилированного паблишера (суб-партнер).

`site_id={YOURMACRO}&` — ID конкретного рекламного места.

`creative_id={YOURMACRO}&` — ID конкретного баннера.

`appmetrica_js_redirect=0&` — отключает JavaScript-редирект.

### Произвольные параметры {#custom-params}

Для лучшей оптимизации кампании рекламодатель и рекламная сеть могут передавать дополнительные параметры в трекинг-ссылке.

Для передачи произвольных параметров добавьте их в трекинг-ссылку. Вы можете передавать значения через эти параметры несколькими способами:

- Вручную — укажите значение параметра:
    
    ```
    custom_parameter=value&
    ```
    
- Автоматически — используйте автоматические подстановки через макросы на стороне рекламной сети:
    
    ```
    example_param={CUSTOM_MACRO}&
    ```
    

Все параметры, которые перечислены в трекинг-ссылке, будут представлены в отчете [Источники трафика](https://appmetrica.yandex.{{ domain }}/statistic?appId=1111&report=campaigns2&metrics=ym_m_advInstallDevicesFake&sampling=medium) в виде дерева.

## Примеры {#examples}

Эти примеры вы можете использовать для тестирования — замените макросы на свои собственные. Удалите лишние, не поддерживаемые, необязательные параметры, если это необходимо.

**Android**

```
https://redirect.appmetrica.yandex.com/serve/600573419754384676?click_id={transaction_id}&google_aid={google_aid}&afpub_id={affiliate_id}&custom_price={payout}
```

**iOS**

```
https://redirect.appmetrica.yandex.com/serve/528515824760210044?click_id={transaction_id}&ios_ifa={ios_ifa}&afpub_id={affiliate_id}&custom_price={payout}
```

## Передача параметров в postback URL, deeplink и целевую ссылку {#passing-params}

Чтобы передать значение параметра из tracking URL в postback URL, deeplink или в целевую ссылку, добавьте в их URL имя параметра в фигурных скобках: `{custom_parameter}`. Таким образом могут быть переданы любые параметры — произвольные и предопределенные.

{% note info "" %}

Если вы используете [Universal link](../sdk/ios/analytics/ios-universal-links.md) в качестве трекинговой ссылки, то значения параметров будут автоматически переданы в deeplink.

{% endnote %}

Примеры передачи параметров:

{% cut "В целевую ссылку" %}

Чтобы добавить макрос для передачи, достаточно отредактировать целевую ссылку в настройках трекера:

Например, в tracking URL передаются следующие параметры:

```
https://redirect.appmetrica.yandex.com/serve/123456?custom_parameter=value1&another_param=value2
```

Чтобы передать параметры `value1` и `value2` в целевой ссылке, следует написать:

```
https://endpoint.myadnetwork.com?some_parameter={custom_parameter}&another_param={another_param}
```

{% endcut %}

{% cut "В postback URL" %}

Чтобы добавить макрос для передачи, достаточно отредактировать postback URL в настройках трекера:

Например, в tracking URL передаются следующие параметры:

```
https://redirect.appmetrica.yandex.com/serve/123456?custom_parameter=value1&another_param=value2
```

Чтобы передать параметры `value1` и `value2` в postback URL следует написать:

```
https://endpoint.myadnetwork.com?some_parameter={custom_parameter}&another_param={another_param}
```

{% endcut %}

{% cut "В deeplink" %}

Передача параметров из трекинг-ссылки в deeplink происходит по следующей схеме:

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-tracking/tracking-url-scheme.png)

Чтобы добавить макрос для передачи, достаточно отредактировать deeplink в настройках трекера:

Например, в tracking URL передаются следующие параметры:

```
https://redirect.appmetrica.yandex.com/serve/123456?custom_parameter=value1&another_param=value2
```

Чтобы передать параметры `value1` и `value2` в deeplink следует написать:

```
myscheme://custom_parameter={custom_parameter}&another_param={another_param}
```

{% endcut %}

## Узнать больше {#learn-more}

- [Блог AppMetrica: Параметры в tracking URL](https://appmetrica.yandex.ru/blog/custom-url-parameters)
- [Использует ли AppMetrica UTM-метки?](../troubleshooting/troubleshooting.md#utm)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
