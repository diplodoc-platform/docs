# E-commerce report

The **E-commerce** report shows what actions users take when making purchases. For example, opening a page, viewing a product profile, adding an item to the cart, placing an order.

To collect statistics on E-commerce events, configure sending events in the app. For more information, see [{#T}](../data-collection/about-ecommerce.md#send-ecommerce).

{% include notitle [segments](_includes/segments.md) %}

To build a report, you need to choose the time period, the audience segment, dimensions, and metrics.

## Report period {#period}

The report is formed for a specific time period. The default period is one week.

{% include [period](_includes/period.md) %}

## Dimensions and metrics {#groups-annd-metrics}

{% include notitle [groups-metrics](_includes/groups-metrics.md) %}

## Dimensions {#group}

{% include notitle [audience-group](_includes/audience-group.md) %}

{% include notitle [geo-group](_includes/geo-group.md) %}

{% cut "E-commerce" %}

- **Product name**.
- **Product ID**.
- **Has promocode**.
- **Product promocode**.
- **Search queries**.
- **Screen name**.
- **Referrer type**.
- **Referrer ID**.
- **Screen parameters**.
- **Product parameters**.
- **Order parameters**.
- **Order ID**.
- **Product category, level 1**.
- ...
- **Product category, level 10**.

{% endcut %}

{% include notitle [date-event-group](_includes/date-event-group.md) %}

{% include notitle [app-group](_includes/app-group.md) %}

{% include notitle [profile-attributes](_includes/profile-attributes.md) %}

### Metrics {#measure}

{% cut "Ecommerce, financial metrics" %}

- **Income**.
- **Average order value** (AOV).
- **Average revenue per user** ([ARPU](*ARPU)).
- **Average revenue per paying user** ([ARPPU](*ARPPU)).
- **Average product price**.
- **Original product cost**.
- **Actual product cost**.
- **Average original product price**.
- **Average actual product price**.

{% endcut %}

{% cut "Ecommerce, virtual money" %}

- **Income**.
- **Average order value** (AOV).
- **Average revenue per user** ([ARPU](*ARPU)).
- **Average revenue per paying user** ([ARPPU](*ARPPU)).
- **Average product price**.
- **Original product cost**.
- **Actual product cost**.
- **Average original product price**.
- **Average actual product price**.

{% endcut %}

{% cut "Ecommerce, actions" %}

- **Product card views**.
- **Users who viewed a product card**.
- **Product page views**.
- **Users who viewed a product page**.
- **Adds to cart**.
- **Products added to cart**.
- **Users who added product to cart**.
- **Products removed from cart**.
- **Users who removed product from cart**.
- **Products bought**.
- **Users who made purchases**.
- **Purchased products per user**.
- **Orders**.
- **Purchases per user**.

{% endcut %}

## Data export {#export}

{% include notitle [export](_includes/export-api.md) %}

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*ARPPU]: {{ arppu }}

[*ARPU]: {{ arpu }}
