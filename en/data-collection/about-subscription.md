# In-app subscriptions

{% if tld == "com" %}

{% note info "" %}

This feature is available with the Custom and Pro [plans](../common/pricing/uae-currency.md#apphud). [Learn more](apphud/apphud-about.md) about enabling Apphud.

{% endnote %}

With AppMetrica, you can set up purchase and subscription tracking through Apphud and gain access to advanced data collection capabilities. This integration allows you to:

- Track subscriptions, including renewals, refunds, and cancellations.
- Process all scenarios, such as updates, drops in rating, proportional refunds, and repeat activations.
- Calculate revenue, accounting for the App Store fee, VAT, and currency conversion rates.

{% endif %}

{% if tld == "ru" %}

<!-- {% note warning %}

This feature is discontinued and will no longer receive updates. Data accuracy not guaranteed.

AppMetrica provides an [alternative tracking technology](https://appmetrica.yandex.com/docs/en/data-collection/apphud/apphud-about) available in certain regions.

{% endnote %} -->

One type of mobile app monetization is auto-renewable subscriptions from the App Store or Google Play. In AppMetrica, you can automatically track:

- Subscription puchases.
- Subscription status updates.
- Metrics calculated based on these events.
   AppMetrica also automatically tracks [non-auto-renewable in-app purchases](about-revenue.md) made through the App Store or Google Play (consumable purchases, non-consumable purchases, and non-auto-renewable purchases).

Subscriptions that are started not through the App Store or Google Play (users subscribing through third-party payment systems) are not tracked automatically.

{% endif %}

## Subscription-related AppMetrica events {#events-subscriptions}

Data about subscribing and updating the subscription status is collected as events with additional parameters.

**List of available events**

| **Event in AppMetrica** | **Subscription action description** |
| ----------- | ----------- |
| `Trial subscription started` | Starting a subscription with a trial period. |
| `Intro subscription started` | Starting a subscription with an intro offer. |
| `Promo subscription started` | Starting a subscription with a promo offer. |
| `Subscription converted` | Paying the full subscription fee after an introductory offer. |
| `Subscription started` | Starting a subscription without introductory offers. |
| `Subscription renewed` | Paying for a new subscription period. |
| `Subscription cancelled` | Cancelling a subscription. After this event, the user may have a paid period left, but no more fees will be charged. |
| `Subscription uncancelled` | Subscription activation event from Apple ID settings. |
| `Subscription expired` | The subscription expired. |
| `Subscription billing issues` | Error when paying for subscription renewal. |
| `Refund` | A refund for a subscription or a one-time purchase. |

The list of events also contains a **One-time purchase** event.

## AppMetrica reports where subscription data is available {#reports-subscription}

**[In-app and Ad Revenue](../mobile-reports/revenue-report.md) report**

:   The report lets you estimate revenue from different types of purchases and advertising revenue separately/as a total. Revenue can be grouped by purchase type and `product_id`.

**[User Acquisition](../mobile-reports/user-acquisition-report.md) and [Remarketing](../mobile-reports/remarketing-report.md) reports**

:   The report lets you estimate revenue from different traffic sources to calculate the ROI.

    {% note info "" %}

    All metrics in the **User Acquisition** and **Remarketing** reports are calculated for the entire user lifetime. When the report period is limited, for the **User Acquisition** the date of application installation is used, and for the **Remarketing** — the date of re-engagement.

    {% endnote %}

**[Funnels](../mobile-reports/funnels-report.md)**

:   The report lets you assess subscription or subscription cancellation conversions.

**[Cohorts](../mobile-reports/cohort-report.md)**

:   The report lets you evaluate accumulated revenue data (or data for day N) and purchase renewability.

## Metrics that can be obtained using subscription data {#metrics}

**Installation to subscription conversion**

:   Use the [Funnels](../mobile-reports/funnels-report.md) report. Select the **Install** event as the first step and the **Subscription started** event as the second step.

{% include [note-conversion](_includes/note-conversion.md) %}

**Trial subscription to full-cost subscription conversion**

:   Use the [Funnels](../mobile-reports/funnels-report.md) report. Select the **Trial subscription started** event as the first step and the **Subscription converted** event as the second step.

{% include [note-conversion](_includes/note-conversion.md) %}

**Payment renewability**

:   - Use the [In-app and Ad Revenue](../mobile-reports/revenue-report.md) report. Select the **Purchases per paying user** metric. This metric shows the number of payments for the selected reporting period.

    - Use the [User Acquisition](../mobile-reports/user-acquisition-report.md) report. Select the **Purchases per paying user metric**. This metric shows the number of payments per user for the entire user lifetime.

    - Use the [Cohort Analysis](../mobile-reports/cohort-report.md) report. Select **Calculate: purchases**, add the **In-app Revenue** → **Product** segment by user, and select the necessary subscription IDs (Product). In each cell, the top number shows the accumulation of renew purchase events per customer on day N.

**Monthly Recurring Revenue (MRR)**

:   Use the [In-app and Ad Revenue](../mobile-reports/revenue-report.md) report. Select the **Revenue Type** and **Product** grouping, add the **In-app Revenue** → **Product** segment by user, and select subscription IDs only. The **Subscription** grouping shows renewable revenue. If you have subscriptions for more than a month, divide the revenue from them by the subscription duration in months.

    {% note info "" %}

    To calculate the **Churned MRR**, add the **In-app Revenue** → **In-App Purchase events** segmentation and select the **Subscription cancelled** and **Subscription expired** events.

    To calculate a **New MRR**, add the **In-app Revenue** → **In-App Purchase events** segmentation and select start subscription events.

    {% endnote %}

**Revenue from various subscriptions/purchases**

:   Use the [In-app and Ad Revenue](../mobile-reports/revenue-report.md) report. Select the **Product** grouping and the **In-app Revenue** metric.

**Highlight paying users**

:   In any report, you can analyze only paying users for the selected period. Select the **In-app Revenue** → **Purchase amount** segmentation and a value that is greater than 0. The report will only provide data on the users who made purchases.

**Send a push newsletter to unsubscribed users**

When setting up a push campaign, add the **In-app Revenue** → **In-App Purchase events** segmentation and select the **Subscription cancelled** event.

**Evaluate ARPU**

:   - Use the [User Acquisition](../mobile-reports/user-acquisition-report.md) report. Select the **In-app Revenue** → **In-app ARPU** metric. This metric shows revenue from in-app purchases per user for the entire user lifetime.

    - Use the [Cohort analysis](../mobile-reports/cohort-report.md) report. Choose **Calculate: In-app Revenue**. In each cell, the top number shows the cumulative ARPU on day N.

## Learn more {#learn-more}

- [Ad Revenue](about-adrevenue.md)
- [In-app purchases](about-revenue.md)
   {% if tld == "ru" %}
- [Google Play in-app subscriptions](subscription-android.md)
- [App Store in-app purchases](subscription-ios.md)
   {% endif %}

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*consumable]: This type of purchase can be made multiple times. For example, this could be extra lives or energy points in a game.

[*non-consumable]: This type of purchase can only be made once. For example, this could be a character in a game or a movie on a streaming site.
