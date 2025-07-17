# Restrictions

## Profile number limit {#limit-profile}

The maximum number of profiles allowed per device is 500. Once this limit is exceeded, new profiles can't be created.

## Custom event limit {#limit-events}

AppMetrica has daily limits on custom events sent via the SDK and Post API. The daily limit for the Free pricing plan is 3,250,000 events.

Limits take into account all events sent via the SDK using the `reportEvent` method and via the Post API (sent to `https://api.appmetrica.yandex.ru/logs/v1/import/events`). An event with nested parameters, regardless of their number and the level of nesting, is considered a single event.

The limit doesn't take into account basic events: [installations](../mobile-api/logs/endpoints.md#installations), [deeplink openings](../data-collection/deeplinks.md), [session starts](../mobile-api/logs/endpoints.md#sessions_starts), [Revenue events](../data-collection/about-revenue.md), [E-commerce events](../data-collection/about-ecommerce.md), [crash and error events](../data-collection/about-crashes-and-errors.md), and push notification events.

### How limits work {#how-limit-works}

The limit is set per day (24 hours) and limits the number of written (displayed in the interface, available in the Logs API) events during this time period. That means no more than 3,250,000 events can be written to AppMetrica at any given time in the last 24 hours with the Free pricing plan.

Events that are over the daily limit are buffered so that they can be sent to AppMetrica once the event queue is unloaded. (after less than 3,250,000 events have been sent in the last 24 hours). In the interface and the Logs API, buffered events appear as delayed data.

Postbacks for buffered events are sent only after the event is written. When events are written in AppMetrica, buffered events are written first, followed by newer events.

> **Example**
>
> On January 1, you sent 3,500,000 events: 3,250,000 of them became available in the interface and the Logs API, and 250,000 were buffered.
>
> On January 2, 250,000 events from the buffer were recorded in AppMetrica (became available in the interface and the Logs API). You sent another 3,500,000 events: this time, 500,000 were buffered (since the 250,000 events from January 1 had been recorded from the buffer), and 3,000,000 became available in the interface and the Logs API.
>
> On January 3, the 500,000 buffered events were recorded in AppMetrica (became available in the interface and Logs API). You sent another 2,000,000 events, all of which were recorded in AppMetrica.

### Which apps are covered by the limit {#which-apps-are-covered}

The limit applies to all apps in the organization and is cumulative for all apps. For example, if you have 10 apps and each one sends 400,000 events per day, that is a total of 4,000,000 events. In 24 hours, you will exceed the limit by 750,000 events.

### Deleting buffered events {#deleting-buffered-events}

If an event has been buffered for more than 14 days, all buffered events will be deleted. New custom events will no longer be accepted via the SDK and Post API.

### Increasing limits {#increasing-limits}

If you want to extend custom event limits for your organization, enable the Custom or Pro pricing plan. To do this, go to the organization's personal account and select a pricing plan. Learn more about {% if locale == 'ru' %}[pricing plans](pricing/ru-currency.md){% endif %}{% if locale == 'en' %}[pricing plans](pricing/uae-currency.md){% endif %}.

## Useful links {#useful-links}

- [AppMetrica events](../data-collection/about-events.md)
- [How to reduce the number of events sent](../troubleshooting/limit-events.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

