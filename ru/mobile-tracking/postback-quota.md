# Политика отправки postback

![](../../_images/postback-settings-{{ locale }}.png){style="max-width: 800px;"}

Постбеки можно добавить при [создании трекера](add-tracker.md#step5) или позднее, при редактировании трекера. Созданные ранее постбеки можно отредактировать в настройках трекера. 

## 1. Install postback {#install-postback}

AppMetrica отправляет install postback при успешной атрибуции. Отправка install postback выполняется в реальном времени, задержка не превышает нескольких минут.

{% note info "" %}

Необходимо учитывать, что процесс атрибуции запускается только когда AppMetrica SDK, интегрированный в приложение, успешно отправил данные на сервер. Для этого необходимо, чтобы мобильное устройство имело подключение к интернету.

{% endnote %}

## 2. Event postback {#event-postback}

AppMetrica отправляет event postback при получении из приложения события, указанного в настройках трекера. Также необходимо, чтобы данная установка приложения была ранее атрибутирована этому трекеру.

Максимальный срок для отправки event postback с момента установки приложения составляет 6 месяцев.

## 3. Ecommerce postback {#ecommerce-postback}

AppMetrica отправляет ecommerce postback при получении из приложения ecommerce-события.

Максимальный срок для отправки ecommerce postback с момента ecommerce-события составляет 6 месяцев.

## 4. In-App postback {#inapp-postback}

AppMetrica отправляет In-App postback при получении из приложения события об inapp-покупках и подписках.

Максимальный срок для отправки purchase postback с момента inapp-покупки составляет 6 месяцев.

## 5. Ad Revenue postback {#adrevenue-postback}

AppMetrica отправляет Ad Revenue postback при получении из приложения события о показе рекламы.

Максимальный срок для отправки adrevenue postback с момента события показа составляет 6 месяцев.

## 6. Неатрибуцированные postback {#unattributed-postback}

Для каждого типа postback можно включить отправку postback на действия всех пользователей, независимо от того, была их установка атрибуцирована к источнику трафика или нет.

## Спецификация {#specification}

Postback — это GET или POST-запрос по протоколу HTTP или HTTPS (рекомендовано) на postback URL, указанный в настройках трекера.

Отправка postback считается неуспешной, если:

- HTTP-код ответа отличается от 200-х;
- Таймаут ответа сервера составил 5 секунд.

Повторная отправка произойдет через 3 минуты, как и все последующие за ней. Если в течении 24 часов с момента первой попытки postback не был успешно отправлен, попытки прекращаются.

AppMetrica использует User-Agent postback запроса `Mozilla/5.0 (compatible; YandexMetrika/2.0; +http://yandex.com/bots)`.

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
