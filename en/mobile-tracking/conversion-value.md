# Managing the Conversion Value

The conversion value in SKAdNetwork is a way to measure the actions that a user performed after installation.

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-tracking/conversion-value-path.png){style="border: solid 1px #cccccc; max-width: 800px;"}

## How it works {#how-it-works}

The app determines the actions that need to be measured, and calls the  [updateConversionValue](https://developer.apple.com/documentation/storekit/skadnetwork/3566697-updateconversionvalue) method to update the conversion value. The method transmits integers from 0 to 63 to advertisers and advertising networks, so it is impossible to track the actions of a particular user.

Since it is impossible to associate the conversion value with a specific user, it is measured in comparison with other data channels by efficiency.

Within 24 hours after it starts working, the app sends the first conversion values. They are updated every 24 hours, but are taken into account only when the conversion value increases.

The conversion value will be updated until it reaches the maximum or 24 hours have passed since the last increase. As soon as the conversion value is fixed, its [postback](*postback) is sent to the advertising network within a day.

## Our solution {#our-solution}

AppMetrica offers several methods for measuring the conversion value. Choose the one that suits you best:

- **Conversions** evaluates the conversion rate of any 6 target events.
- **Number of events** calculates how many target events users have completed on average and in total.
- **Revenue** calculates the total amount of purchases, ARPU, the number and share of paying users (based on Revenue or E-commerce events).

Configure the desired option directly in the interface, and the AppMetrica SDK will automatically measure and send the conversion value to SKAdNetwork.

Advantages:

- You don't need to spend time on development and testing (SDK version 4.0.0 is enough).
- If the conversion measurement method changes, you don't need to update the app. The new method is applied on all versions simultaneously and automatically.

## Choosing an app {#app-choice}

An app should have uniform rules for measuring the conversion value. The "another conversion scheme is linked" warning means that your app also uses another APIKey, that has another measurement configured.

For one APIKey in several apps, you can apply the same conversion value measurement scheme.

## Types of measurement {#value-types}

The chosen type sets which actions in the app affect the conversion value.

### Conversions {#advancement}

The model reflects the number and share of users who achieved a set event. For each of the 6 free slots, you can choose a regular, revenue, or e-commerce event.

{% cut "Example" %}

To evaluate the efficiency of two channels, set up 2 events: trial and paid subscriptions. Conversion shows the first channel brings in a 20% conversion rate on the first stage and 5% on the second stage, and the second channel brings in 15% on the first stage and 7% on the second.

{% endcut %}

### Events count {#quantity}

The model shows the total number of events and the average per user. You can track their number up to 63 times or increase the maximum by changing the step size.

{% cut "Example" %}

The target action is completing the level. The model allows you to estimate the total number of events for all users and how many levels are passed on average by players attracted by different channels.

{% endcut %}

**Step size** measures the number of events until the next step. By default, it is equal to 1, but you can increase it when measuring a large number of events.

{% cut "Example" %}

The target action in your app is viewing photos. During the first day, users on average view several hundred photos. But the maximum conversion value is 63, which means that when calculating it, it will be the same for the majority. To get around this restriction, count every 5, this lets you track 315 actions at most (the first action with a value of 1, then 6 actions — a value of 2, and so on).

{% endcut %}

### Revenue {#value-types}

The model shows revenue, the number and share of paying users, and ARPU. Revenue in all currencies is converted to the chosen unit. Transactions for the measurement period are summed up.

{% note info %}

The maximum possible revenue value is 63 units. If 1 unit of measurement is $0.50, then the minimum fixed revenue is $0.50, the next one is $1, and the maximum for the period is $32.

{% endnote %}

**Data source** determines whether the revenue is calculated based on the revenue or e-commerce events.

**Step size** sets the minimum and accuracy of the measured revenue. The minimum is one unit, and the maximum is 63 units.

{% cut "Example" %}

The average advertising revenue per user in the first 3 days ranges from a few cents to one and a half dollars. To get a calculation that is close to reality, set the unit to $0.02, then the revenue will be calculated from $0.02 to $1.26.

{% endcut %}

## Measurement period {#period}

The advertising network won't receive a postback as long as the conversion value continues to increase more often than once a day. When measuring constantly growing metrics, such as the number of events or revenue, it may be useful to limit the period during which AppMetrica sends the conversion value.

{% cut "Example" %}

Your users view dozens, and sometimes hundreds of posts per day, so you use a step size of 10, the maximum is, respectively, 621 post views. For users who consistently view 10-15 posts a day, the conversion value will be measured for almost 2 months, and all this time you won't even know about them.

{% endcut %}

The period restriction makes sense if you plan to change the measurement object. Since the SKAdNetwork postback does not contain data about this, the value calculated according to the previous model, but received at the time of the new one, may distort the results.

{% cut "Example" %}

You measure the number of event A. On Monday, a user installs your app and the conversion value increases every day. On Wednesday, the model changes to revenue. The user continues to use the app until Friday inclusive, and stops at the  weekend. At the end of the week, a postback comes with a conversion value of 10, which is taken as $10 of revenue from this user, although in reality there was no revenue. If you limit the period to 2 days, this won't happen.

{% endcut %}

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*postback]: A GET request to a specified URL, which is known as the postback URL. The request can include specific parameters. You can add up to 5 requests per campaign. For more information, see the [postback policy](policy.md).
