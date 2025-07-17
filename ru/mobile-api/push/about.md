# Push API

Позволяет создавать группы push-сообщений, рассылать push-сообщения на устройства, проверить статус их отправки.

{% note info %}

Для использования API необходимо [получить авторизационный токен](../intro/authorization.md). Токен необходимо передавать в HTTP заголовке или в параметрах запроса.

{% endnote %}

Группа — это контейнер для отправки push-сообщений. Позволяет группировать отправки в [отчете по push-кампаниям](../../mobile-reports/push-campaign.md). Группа может содержать произвольное количество отправок. В отчете отображается на первом уровне вместе с push-кампаниями, запущенными через [веб-интерфейс](../../push/marketing.md).

Тег — это произвольная строка, маркирующая каждую отправку push-сообщений через API. Одним тегом может быть промаркировано произвольное количество отправок. В отчете отображается на втором уровне.

Запрос выполняется к хосту `https://push.api.appmetrica.yandex.net`. Например:

```
https://push.api.appmetrica.yandex.net/push/v1/management/groups
```

Отправленные группы будут отображаться в отчете по push-кампаниям и могут быть выгружены с помощью [API отчетов](../api_v1/intro.md). Доступны следующие измерения и метрики для построения отчетов:

- Измерения: `ym:pc:group`, `ym:pc:tag`, `ym:pc:transfer`, `ym:pc:operatingSystem`.
- Метрики: `ym:pc:sentDevices`, `ym:pc:receivedDevices`, `ym:pc:openedDevices`, `ym:pc:conversion`.

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
