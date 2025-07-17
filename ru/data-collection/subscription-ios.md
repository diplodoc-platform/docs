# In-app подписки App Store

<!-- {% note warning %}

Функциональность больше не поддерживается и не обновляется. Точность данных не гарантируется.

AppMetrica предоставляет [альтернативную технологию трекинга](https://appmetrica.yandex.com/docs/ru/data-collection/apphud/apphud-about), которая доступна в некоторых регионах.

{% endnote %} -->

Для отслеживания статусов подписок в App Store используется App Store Shared Secret и App Store Server Notifications. Вы можете не использовать App Store Server Notifications для отслеживания подписок в AppMetrica (например, если вы используете дополнительный сервис отслеживания статусов подписок), но в таком случае данные о подписках могут приходить с задержкой до 24 часов. Также часть событий о подписках будет недоступна.

Адрес для нотификаций — [https://apple.inapp.appmetrica.yandex.net](https://apple.inapp.appmetrica.yandex.net).

## App Store Shared Secret {#shared-secret}

AppMetrica использует ключ для валидации, расшифровки рецепта и для проверки статуса подписки.

1. Откройте App Store Connect, перейдите в раздел [Apps](https://appstoreconnect.apple.com/apps) и выберите свое приложение.
2. В секции **Features** слева перейдите в **Subscriptions**.
3. На странице найдите раздел **App-Specific Shared Secret**, нажмите кнопку **Manage**.
4. Создайте и скопируйте **Shared Secret**.
5. В интерфейсе AppMetrica перейдите в настройки вашего приложения, в раздел **Revenue**.
6. Вставьте **Shared Secret** для приложения в поле **App Store Shared Secret**.

## App Store Server Notifications {#notifications}

Apple позволяет подключить уведомления "server-to-server", поэтому вы можете получать информацию об изменении статусов подписок. Для этого необходимо настроить отправку уведомлений от App Store Server Notifications:

1. Скопируйте URL-адрес для уведомлений сервера App Store ([https://apple.inapp.appmetrica.yandex.net](https://apple.inapp.appmetrica.yandex.net)) или из интерфейса AppMetrica **Настройки** → **Revenue**.
2. Откройте App Store Connect, перейдите в раздел [Apps](https://appstoreconnect.apple.com/apps) и выберите свое приложение.
3. В секции **General** слева перейдите в **App Information**.
4. Внизу открывшейся страницы, в блоке **App Store Server Notifications** у пункта **Production Server URL** нажмите кнопку **Edit**.
5. В поле **Production Server URL** введите URL-адрес из AppMetrica.
6. Ниже в форме выберите **Version 2 Notifications** и нажмите **Save**.

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
