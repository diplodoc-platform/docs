# Авторизация

Для использования API AppMetrica необходимо получить {% if locale == 'ru' %}[авторизационный токен](https://tech.yandex.ru/oauth/doc/dg/concepts/ya-oauth-intro-docpage/){% endif %}{% if locale == 'en' %}[авторизационный токен](https://tech.yandex.com/oauth/doc/dg/concepts/ya-oauth-intro-docpage/){% endif %} с помощью Яндекс.OAuth. Его необходимо передавать для каждого метода в HTTP-заголовке `Authorization`.

Пример:

{% list tabs %}

- cURL

  ```bash translate=no
  curl -X GET \
    https://api.appmetrica.yandex.ru/management/v1/applications \
    -H 'Authorization: OAuth <your_token>'
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](#get-oauth-token).

- HTTP

  ```httpget translate=no
  GET /management/v1/applications HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Authorization: OAuth <your_token>
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](#get-oauth-token).

{% endlist %}

{% note alert %}

Передача токена в параметрах URL не поддерживается.

{% endnote %}

Если метод API вызван без токена или в запросе передан недействительный токен, сервер возвращает HTTP-статус `401 Unauthorized`.

## Получение OAuth-токена {#get-oauth-token}

Чтобы получить авторизационный токен:

1. Перейдите на страницу [создания приложения](https://oauth.yandex.{{ domain }}/client/new) в Яндекс ID.

    {% note alert "" %}

    Используйте ссылку из инструкции. Если открыть страницу из Яндекс ID, указать нужные доступы не получится.

    {% endnote %}

2. Укажите почту для связи. Внизу страницы нажмите **Создать приложение**: откроется окно **Доступ внешних приложений** в Яндекс ID.
3. В разделе **Общие данные** введите название сервиса. При желании прикрепите его иконку.
4. В разделе **Платформы приложения** выберите пункт **Веб-сервисы**. Другие пункты не нужны.
5. В поле **Redirect URI** введите адрес `https://oauth.yandex.ru/verification_code`.

    {% cut "Скриншот" %}

    ![](../../../_images/click-url-redirect-{{ locale }}.png){width=500px}{style="border: solid 1px #cccccc;"}

    {% endcut %}

6. В разделе **Права доступа к данным пользователей** укажите **appmetrica:read** и **appmetrica:write**. Чтобы доступы появились в выпадающем списке, начните вводить их название.

    {% cut "Скриншот" %}

    ![](../../../_images/access-data-{{ locale }}.png){width=500px}{style="border: solid 1px #cccccc;"}

    {% endcut %}


7. Скопируйте идентификатор вашего приложения в блоке **ClientID**.

    {% cut "Скриншот" %}

    ![](../../../_images/clientid-copy-{{ locale }}.png){width=500px}{style="border: solid 1px #cccccc;"}

    {% endcut %}

8. Вставьте его в ссылку, чтобы получить отладочный токен:

    ```
    https://oauth.yandex.ru/authorize?response_type=token&client_id=<идентификатор приложения>
    ```

Подробнее об авторизации с помощью OAuth {% if locale == 'ru' %}[в документации сервиса](https://tech.yandex.ru/oauth/doc/dg/concepts/about-docpage/){% endif %}{% if locale == 'en' %}[в документации сервиса](https://tech.yandex.com/oauth/doc/dg/concepts/about-docpage/){% endif %}.

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
