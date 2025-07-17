# Postback policy

![](../../_images/postback-settings-{{ locale }}.png){style="max-width: 800px;"}

You can add postbacks when [creating a tracker](add-tracker.md#step5) or later when editing a tracker. Postbacks that have already been created can be edited in the tracker settings.

## 1. Install postback {#install-postback}

AppMetrica sends an install postback for successful attribution. The install postback is sent in real time with a delay of no more than a few minutes.

{% note info "" %}

Keep in mind that the attribution process is only run when the AppMetrica SDK that is integrated in the app successfully sent data to the server. In order for this to happen, the mobile device must be connected to the internet.

{% endnote %}

## 2. Event postback {#event-postback}

AppMetrica sends an event postback when it receives the event from the app that is specified in the tracker settings. It is also necessary that this app installation was previously attributed to this tracker.

The maximum period for sending an event postback is 6 months from the time of app installation.

## 3. E-commerce postback {#ecommerce-postback}

AppMetrica sends an E-commerce postback after receiving an E-commerce event from the app.

E-commerce postbacks are sent within a maximum of 6 months of the E-commerce event.

## 4. In-App postback {#inapp-postback}

AppMetrica sends an in-app postback when it receives an event about in-app purchases and subscriptions from the app.

Purchase postbacks are sent within a maximum of 6 months of the in-app purchase event.

## 5. Ad revenue postback {#adrevenue-postback}

AppMetrica sends an ad revenue postback after receiving an ad impression event from the app.

Ad revenue postbacks are sent within a maximum of 6 months of the ad impression event.

## 6. Unattributed postbacks {#unattributed-postback}

For each type of postback, you can enable postback sending for all users' actions, regardless of whether their installation was attributed to the traffic source or not.

## Specification {#specification}

A postback is a GET or POST request sent over HTTP or HTTPS (recommended) to the postback URL specified in the tracker settings.

Sending the postback is considered unsuccessful if:

- The HTTP response code is something other than 200-x.
- The server didn't respond within 5 seconds.

It will be re-sent every 3 minutes. If the postback was't sent successfully within 24 hours of the first attempt, no more attempts will be made.

AppMetrica uses the postback request User-Agent `Mozilla/5.0 (compatible; YandexMetrika/2.0; +http://yandex.com/bots)`.

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
