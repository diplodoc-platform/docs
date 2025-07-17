# Limiting custom events

## What limits are there in AppMetrica? {#limits}

The free AppMetrica plan has daily limits for custom events sent via the SDK and the Post API. The daily limit is 3,250,000 events.

## What events are limited? {#list-events}

The limits only apply to custom events (events that you named and sent via the SDK or Post API). An event with nested parameters, regardless of their number and the level of nesting, is considered a single event.

Basic events — installations, deeplink openings, session starts, Revenue events, Ecommerce events, crash and error events, and push notification events — don't count toward the limit. Sending custom attributes doesn't count either.

## What happens to events over the limit? {#unlimits}

Events that are over the daily limit are buffered so that they can be sent to AppMetrica once the event queue is unloaded. In the interface and the Logs API, buffered events appear as delayed data.

**Example**
:   On January 1, you sent 3,500,000 events. 3,250,000 of them became available in the interface and the Logs API, while 250,000 were buffered.

    On January 2, 250,000 events from the buffer were recorded in AppMetrica (became available in the interface and the Logs API). You sent another 3,500,000 events: this time, 500,000 were buffered (since the 250,000 events from January 1 had been recorded from the buffer), and 3,000,000 became available in the interface and the Logs API.

    On January 3, the 500,000 buffered events were recorded in AppMetrica (became available in the interface and Logs API). You sent another 2,000,000 events, all of which were recorded in AppMetrica.

If you regularly exceed the limit, and your events stay buffered for 14 days, AppMetrica stops accepting custom events from the SDK and via the Post API, and your buffered events won't be recorded.

You can resume collection of custom events if you're on a Custom or Pro plan. To resume collection, [contact support](feedback-new.md).

## I have multiple apps. Is there a separate limit for each app? {#more-apps}

No, the limit is the same for all apps belonging to one organization.

## What's an organization in AppMetrica? {#organization}

An organization is a user who owns one or more AppMetrica tags. The owner is specified in the app settings.

AppMetrica offers a company account where you can see your current event limits, manage access, provide company's payment details, and, if needed, purchase an extended tariff.

## Can I transfer an app to another organization? {#organization-switch}

Yes. For example, if your company's AppMetrica tags were created by different users or some of the tags were created by an agency, you can link the tags to your organization in your organization account.

In the list of apps, click **...** and select **Transfer app to another organization**. Your account must have the rights to the organization that you want to transfer the app to.

## Can I create multiple AppMetrica organizations for a single legal entity? {#several-organizations}

No. You can only use a legal entity for one AppMetrica organization.

## Are there any limits for the Logs API? {#logs-api-limits}

No. However, if you regularly export large amounts of data, we recommend using the [Data Stream API](../mobile-api/datastream/about.md).

## How do I check how many custom events I have? {#value-events}

You can see the number of custom events that you're currently sending to AppMetrica in your personal account. To do this, open the **Organization** tab on the sidebar. The chart takes into account all the events of the organization's apps by the date of their processing in AppMetrica. The data in the table takes into account app events for the last 30 days.

## How do I increase the limit? {#up-limits}

In your personal account, you can select and pay for the volume of events suitable for your apps. Lear more about the {% if locale == 'ru' %}[pricing plans](https://ads.yandex.com/analytics/pricing/ru){% endif %}{% if locale == 'en' %}[pricing plans](https://ads.yandex.com/analytics/pricing){% endif %}.

## How do I optimize the number of sent events to avoid going over the limit? {#optimize}

You can optimize your sent events in several ways:

1. Check if your app has duplicate events. For example, the events "Clicking the button to go to the second step of onboarding" and Viewing the screen of the second step of onboarding apply to the same user action: moving on to the second step of onboarding. If this is the case, you can stop sending these events via the SDK.

2. Check if your app has events that are sent many times and apply to the same user action. For example, if your app requires you to click the same button multiple times in a row. Instead of sending an event for each button click, you can send a single event with an additional parameter: the number of clicks.

3. Check if your app has events that duplicate standard AppMetrica events: for example, installations, session starts, deeplink openings, In-app purchases, Ad revenue, Ecommerce events, crash and error events, and push campaign events. If you have custom events that duplicate standard ones, you can stop tracking them at the SDK level.


## I have leftover events from old versions of my app that I no longer use and that don't exist in newer versions of the app. How can I prevent them from counting toward the event limit? {#old-events}

If your app has events that you don't use for analytics, you can disable their collection in the AppMetrica settings.

Go to **Settings** → **Events** and find the event you don't need. In the **Events collection** block, select the **Collecting disabled** mode.

After that, disabled events will no longer be collected or count toward the limit. However, all previously sent events remain in the reports and count toward the limit.

## How much does a paid AppMetrica pricing plan cost? {#cost}

The cost depends on the volume of events you send and the additional features that you need, such as the A/B testing service, customized dashboards, or the Data Stream API. Select the pricing plan that suits you best on the {% if locale == 'ru' %}[pricing plan page](https://ads.yandex.com/analytics/pricing/ru){% endif %}{% if locale == 'en' %}[pricing plan page](https://ads.yandex.com/analytics/pricing){% endif %}.

## If I have many buffered events and I extend my limit in the "Custom" pricing plan, will all of my buffered events be loaded into AppMetrica? {#up-custom}

When you purchase an extended event limit in the "Custom" pricing plan, you get an increased daily limit for recorded events. Your buffered events start exporting more quickly when you send fewer events to AppMetrica than your daily limit. However, this doesn't mean that all of your buffered events will be recorded in AppMetrica after you purchase an extended limit in the "Custom" pricing plan.

## How do I pay? {#bill}

Currently, you can only pay by invoice. Specify your company's details in your personal account, click **Top up balance**, download the invoice, and make the payment. You can also check the acceptance certificate in Yandex Balance at the end of each month.

## Can I select or change my pricing plan later? {#tariff}

Yes, you can select and change the pricing plan in your personal account at any time.

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
