# Трекинг в iOS 15

Начиная с iOS 15 можно настроить отправление postback SKAdNetwork напрямую от Apple в AppMetrica. В этом случае в отчете [User Acquisition SKAdNetwork](../mobile-reports/user-acquisition-skadnetwork.md) будут собраны данные по рекламным установкам всех пользователей, включая не предоставивших доступ к IDFA.

## Настройка отправки копий postback в AppMetrica {#ios15-postbacks}

Чтобы отправлять копии postback об установках:

1. Выберите файл `Info.plist` в навигаторе проектов в Xcode.
2. Добавьте новый ключ в список свойств.
3. Введите имя ключа [NSAdvertisingAttributionReportEndpoint](https://developer.apple.com/documentation/bundleresources/information_property_list/nsadvertisingattributionreportendpoint?changes=latest_minor).
4. Укажите тип свойства String.
5. В значении свойства укажите **https://appmetrica.yandex** — URL адрес для приёма постбеков SKAdNetwork в AppMetrica.

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
