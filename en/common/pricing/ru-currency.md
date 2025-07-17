---
noIndex: true

content: noindex
name: robots
---

# Pricing plans for RU

Organization owners are responsible for monitoring limits and activating pricing plans. For each plan, the cost is given per organization. Plan limits apply to all organization apps.

The approximate plan cost is given per month. For more information, see [Calculating the service cost](#calc).

AppMetrica has three pricing plans:

1. The **Free** plan offers basic features:
    - [Custom events](../../data-collection/about-events.md): up to 100 million per month / 3.25 million per day.
    - [A/B experiments](../varioqub-app-about.md): up to two at a time.
    - [Flag configuration](../varioqub-app-about.md): up to 100 at a time.
    - [In-app subscription tracking](../../data-collection/about-subscription.md).
    - Basic event tracking.
    - Standard reports and API access.
    - Analysis of all types of [Revenue](../../mobile-reports/revenue-report.md).
    - [Push campaigns](../../push/index.md).

    You can't purchase additional tools or extend the limits with this plan.

1. The **Custom** plan can be tailored to your individual needs. It offers the same basic features as the **Free** plan but allows purchasing extra tools and extending limits. The plan's cost depends on the [options](#pro-upgrade) you choose.

1. The **Pro** plan lets you maximize the value you get from AppMetrica, greatly expanding the service's capabilities:

    - [Custom events](../../data-collection/about-events.md): up to 20,000 million per month / 650 million per day.
    - [A/B experiments](../varioqub-app-about.md): up to ten at a time.
    - [Flag configuration](../varioqub-app-about.md): up to 500 at a time.
    - [In-app subscription tracking](../../data-collection/about-subscription.md).
    - Basic event tracking.
    - Standard reports and API access.
    - Analysis of all types of [Revenue](../../mobile-reports/revenue-report.md).
    - [Push campaigns](../../push/index.md).
    - 100 [workspaces](../../mobile-reports/workspaces.md).
    - 500 [saved reports](../../mobile-reports/save-reports.md).
    - [LTV and Churn predictions](https://appmetrica.yandex.com/en/about/blog/ltv-churn-predictions/how-to-guide).
    - Personal support via a dedicated chat.
    - [Data Stream API](../../mobile-api/datastream/about.md): up to 200 million events per month.

    This package costs RUB 278,400 per month. If needed, you can purchase [additional tools](#pro-upgrade) and extend the limits further.

## Additional options available for purchase {#pro-upgrade}

With the **Custom** and **Pro** plans, you can purchase:

#|
|| **Features** | **Limits** | **Custom, RUB** | **Pro, RUB** ||
|| [Custom events](../../data-collection/about-events.md), monthly limit[^(a)^](#a) | 300 million per month / 9.75 million per day  |  38,000 | <br/><br/><br/><br/><br/><br/>278,400 ||
|| ^ | 900 million per month / 29,52 million per day  |  76,000 | ^ ||
|| ^ | 2,000 million per month / 65 million per day | 85,000 | ^ ||
|| ^ | 5,000 million per month / 162.5 million per day | 93,000 | ^ ||
|| ^ | 10,000 million per month / 325 million per day | 116,000 | ^ ||
|| ^ | 15,000 million per month / 487.5 million per day | 140,000 | ^ ||
|| ^ | 20,000 million per month / 650 million per day | Pro only | ^ ||
|| [Data Stream API](../../mobile-api/datastream/about.md), monthly event limit[^(b)^](#b) | 200 million  | 110,000 | 0 (included in the plan) ||
|| ^ | 400 million  | 127,600 |  17,600 ||
|| ^ | 600 million  | 144,100 |  34,100 ||
|| ^ | 800 million  | 161,700 |  51,700 ||
|| ^ | 1,000 million  | 178,200 |  68,200 ||
|| ^ | 1,500 million  | 218,900 | 108,900 ||
|| ^ | 2,000 million  | 258,500 | 148,500 ||
|| ^ | 2,500 million  | 295,900 | 185,900 ||
|| ^ | 3,000 million  | 330,000 | 220,000 ||
|| ^ | 3,500 million  | 366,300 | 256,300 ||
|| ^ | 4,000 million  | 399,300 | 289,300 ||
|| ^ | 4,500 million  | 430,100 | 320,100 ||
|| ^ | 5,000 million  | 459,800 | 349,800 ||
|| ^ | > 5,000 million  | negotiated on an individual basis | > ||
|| [Workspaces](../../mobile-reports/workspaces.md) | 100[^(c)^](#c)  | <br/>15,200  | <br/>0 (included in the plan)  ||
|| [Saved reports](../../mobile-reports/save-reports.md)| 500[^(c)^](#c)  | ^ | ^ ||
|| [Flag configuration](../varioqub-app-about.md) | 500[^(d)^](#d)  | 7,200 | 0 (included in the plan) ||
|| ^ | 2000[^(e)^](#e) | 15,200 |  15,200 ||
|| Simultaneous [A/B experiments](../varioqub-app-about.md) | 10[^(f)^](#f)  |  15,200 | 0 (included in the plan) ||
|| ^ | 100[^(g)^](#g)  |  39,200 |  24,000 ||
|| {% if tld == "ru" %}[Anti-fraud](../fraud-score.md){% else %}Anti-fraud{% endif %}[^(h)^](#h), monthly install limit | 30,000  |  58,800 |  58,800 ||
|| ^ | 100,000  | 118,800 | 118,800 ||
|| ^ | 250,000  | 238,800 | 238,800 ||
|| ^ | 500,000  | 454,800 | 454,800 ||
|| ^ | 1,000,000 | 864,000 | 864,000 ||
|| ^ | > 1,000,000 | negotiated on an individual basis | >  ||
|#

{#a}

^(a)^ The cost of the service when exceeding the limit is 62 RUB for each full 1 million events. You can enable this option in your account.

{#b}

^(b)^ If the monthly limit is exceeded, the service cost is RUB 100 for every 1,000,000 events exported using the Data Stream API during that month.

{#c}

^(c)^ For each app within the organization.

{#d}

^(d)^ Up to 5 conditions for each.

{#e}

^(e)^ Up to 20 conditions for each.

{#f}

^(f)^ Up to 20 flags for each.

{#g}

^(g)^ Up to 50 flags for each.

{% if tld == "ru" %}

{#h}

^(h)^ This option is only available for legal entities registered in Russia.

{% endif %}

## Calculating the service cost {#calc}

### The cost of activated services is calculated on a daily basis {#daily}

Calculation formula:

```
Cost per day of providing services = Plan / Number of days in the current month
```

Services are considered provided if the plan is activated as of 12:00 GMT+3 on the current day.

### The cost of provided services is calculated for a calendar month {#monthly}

Calculation formula:

```
Cost of services per calendar month = Cost per day of services provided * Number of days with services provided
```

For example, you activated the Pro plan at 14:00 GMT+3 on June 15. In this case, as of 11:59 GMT+3 on July 1, the cost of your services for June amounted to:

```
Actual cost = (RUB 278,400 / 30) * 15 = RUB 139,200
```

All prices include VAT.{% if tld == 'ru' %} To manage your payments, consider using [Yandex Balance](https://yandex.ru/support/balance/en/).{% endif %}

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}


<style>
.dc-doc-page .yfm table tr:nth-child(2n) {
    background: var(--g-color-base-background);
}
</style>
