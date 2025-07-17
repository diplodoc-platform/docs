# Authorization

To use the AppMetrica API, you need to get an {% if locale == 'ru' %}[access token](https://tech.yandex.ru/oauth/doc/dg/concepts/ya-oauth-intro-docpage/){% endif %}{% if locale == 'en' %}[access token](https://tech.yandex.com/oauth/doc/dg/concepts/ya-oauth-intro-docpage/){% endif %} from the Yandex.OAuth service. The token must be sent with all method requests in the HTTP `Authorization` header.

Example:

{% list tabs %}

- cURL

   ```bash translate=no
   curl -X GET \
     https://api.appmetrica.yandex.ru/management/v1/applications \
     -H 'Authorization: OAuth <your_token>'
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](#get-oauth-token).

- HTTP

   ```httpget translate=no
   GET /management/v1/applications HTTP/1.1
   Host: api.appmetrica.yandex.ru
   Authorization: OAuth <your_token>
   ```

   where `<your_token>` is an OAuth token that can be obtained using [instructions](#get-oauth-token).

{% endlist %}

{% note alert %}

Sending the token in the URL parameters is not supported.

{% endnote %}

If an API method is called without a token, or the request includes an invalid token, the server returns the HTTP status `401 Unauthorized`.

## Obtaining the OAuth token {#get-oauth-token}

To get an access token:

1. Go to the [app creation](https://oauth.yandex.{{ domain }}/client/new) page in Yandex ID.

   {% note alert "" %}

   Use the link from the instructions. Opening the page from Yandex ID doesn't provide an option to set up permissions.

   {% endnote %}

2. Specify a contact email address. At the bottom of the page, click **Create app** to open the **External app access** window in Yandex ID.
3. Under **General data**, input the service name. Attach a service icon if needed.
4. In the **App platforms** section, select **Web services**. Other items are optional.
5. In the **Redirect URI** field, enter the address `https://oauth.yandex.ru/verification_code`.

   {% cut "Screenshot" %}

   ![](../../../_images/click-url-redirect-{{ locale }}.png){width=500px}{style="border: solid 1px #cccccc;"}

   {% endcut %}

6. In the **Data access** section, specify **appmetrica:read** and **appmetrica:write**. To see the premissions in the dropdown, begin typing their name.

   {% cut "Screenshot" %}

   ![](../../../_images/access-data-{{ locale }}.png){width=500px}{style="border: solid 1px #cccccc;"}

   {% endcut %}


7. Copy the ID of your app from the **ClientID** section.

   {% cut "Screenshot" %}

   ![](../../../_images/clientid-copy-{{ locale }}.png){width=500px}{style="border: solid 1px #cccccc;"}

   {% endcut %}

8. Paste it into the link to get a debug token:

   ```
   https://oauth.yandex.ru/authorize?response_type=token&client_id=<app_id>
   ```

For more information, see {% if locale == 'ru' %}[OAuth documentation](https://tech.yandex.ru/oauth/doc/dg/concepts/about-docpage/){% endif %}{% if locale == 'en' %}[OAuth documentation](https://tech.yandex.com/oauth/doc/dg/concepts/about-docpage/){% endif %}.

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
