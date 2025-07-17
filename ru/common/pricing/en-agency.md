---
noIndex: true

content: noindex
name: robots
---
{% if locale == 'en' %}

# Pricing plans for agencies (WW)

Organization owners are responsible for monitoring limits and activating pricing plans.

For each plan, the cost is given per organization. Plan limits apply to all organization apps.

The approximate plan cost is given per month. For more information, see [Calculating the service cost](#calc).

## Custom plan {#custom}

**Custom events**

- USD 441 per month: Up to 9,750,000 [custom events](../../data-collection/about-events.md) per day.
- USD 891 per month: Up to 29,520,000 [custom events](../../data-collection/about-events.md) per day.
- USD 1,341 per month: Unlimited [custom events](../../data-collection/about-events.md) per day.

Additional options available for purchase:

**Workspaces**

- USD 171 per month: 100 workspaces and 100 saved reports for each app in the organization.

**Configuration of flags**
- USD 81 per month: 500 flags, 5 conditions available for each one.
- USD 171 per month: 2,000 flags, 20 conditions available for each one.

**A/B experiments**

- USD 171 per month: 10 simultaneous experiments, each one with up to 20 flags + pro features.
- USD 441 per month: 50 simultaneous experiments, each one with up to 100 flags + pro features.

**Data Stream API**

- USD 810 per month: Up to 200,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 1,044 per month: Up to 400,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 1,179 per month: Up to 600,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 1,269 per month: Up to 800,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 1,458 per month: Up to 1,000,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 1,791 per month: Up to 1,500,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 2,115 per month: Up to 2,000,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 2,421 per month: Up to 2,500,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 2,700 per month: Up to 3,000,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 2,997 per month: Up to 3,500,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 3,267 per month: Up to 4,000,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 3,519 per month: Up to 4,500,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 3,762 per month: Up to 5,000,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).

If the monthly limit is exceeded, the service cost is USD 0.8 for each full 1,000,000 events exported using the Data Stream API during that month.

## Pro plan {#pro}

The cost is USD 2,550 per month.

**This includes:**

- [Custom events](../../data-collection/about-events.md): 20 billions per month / 645 161 290 per day.
- Events exported using the [Data Stream API](../../mobile-api/datastream/about.md): up to 200 millions per month.
- Extended support to the organization owner and administrators.<!-- https://st.yandex-team.ru/DOCSUP-64329 - Subscription status tracking, regardless of their total cost. -->
- Option to enable importing events that show the predicted probability of user churn and events that show the relative predicted user LTV.
- 100 workspaces.
- 100 saved reports.

Additional **Pro** plan options available for purchase:

**Configuration of flags**

- USD 85 per month: 2,000 flags, 20 conditions available for each one + pro features.

**A/B experiments**

- USD 255 per month: 100 simultaneous experiments, each one with up to 50 flags.

**Data Stream API**

- USD 136 per month: Up to 400,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 279 per month: Up to 600,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 399 per month: Up to 800,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 527 per month: Up to 1,000,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 841 per month: Up to 1,500,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 1,147 per month: Up to 2,000,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 1,436 per month: Up to 2,500,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 1,700 per month: Up to 3,000,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 1,980 per month: Up to 3,500,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 2,235 per month: Up to 4,000,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 2,474 per month: Up to 4,500,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).
- USD 2,703 per month: Up to 5,000,000,000 events per month exported using the [Data Stream API](../../mobile-api/datastream/about.md).

If the monthly limit is exceeded, the service cost is USD 0.77 for each full 1,000,000 events exported using the Data Stream API during that month.

## Calculating the service cost {#calc}

### The cost of activated services is calculated on a daily basis {#daily}

Calculation formula:

```
Cost per day of providing services = Plan / Number of days in the current month
```

Services are considered provided if the plan is activated as of 12:00 GMT+3 on the current day.

### The cost of provided services is calculated for a calendar month {#monthly}

Calculation formula:

```
Cost of services per calendar month = Cost per day of services provided * Number of days with services provided
```

For example, you activated the Pro plan at 14:00 GMT+3 on June 15. In this case, as of 11:59 GMT+3 on July 1, the cost of your services for June amounted to:

`Actual = (USD 232,000 / 30) * 15 = USD 139,200`.

All prices are inclusive of VAT.

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}

{% endif %}
