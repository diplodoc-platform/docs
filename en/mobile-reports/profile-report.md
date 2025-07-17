# Profiles report

The report shows the distribution of users by the specified attributes.

{% include notitle [segments](_includes/segments.md) %}

{% note alert "" %}

When building a report, you can't specify a time period: only the current value of the attribute is displayed. To track the history of changes to an attribute, you should configure sending a [custom event](../data-collection/about-events.md) along with the attribute.

{% endnote %}

To build a report, you need to choose the desired audience segment and an attribute for analysis.

{% cut "Why do I see multiple profiles for a single user?" %}

Most likely, you didn't provide the user profile ID when initializing the library. In this case, the AppMetrica SDK creates a technical profile with an ID of `appmetrica_device_id`. Calling the `setUserProfileID` method with the new ID creates a new profile, yet the technical profile still remains.

To prevent the creation of a technical profile, tweak how you send the ID when initializing the library using the extended config. On [Android](../sdk/android/analytics/android-operations.md#initialize), you can do that by calling the `withUserProfileID` method; on [iOS](../sdk/ios/analytics/ios-operations.md#initialize), edit the `userProfileID` property.

{% endcut %}

## Dimensions {#group} 

The data in the report is grouped by system and user attributes values.

For custom attributes with the [counter](../data-collection/profile-attributes.md#number) and [number](../data-collection/profile-attributes.md#counter) types, you can set the length of the grouping interval. It is useful when you have a large sample of values, and you need to assess the distribution of users by groups of values.

You can set the length of the interval manually. For example, for a sample from 0 to 99, you can set 25 as the length of the interval. The values are grouped in four intervals: 0–24, 25–49, 50–74, 75–99.

{% note info %}

Attribute values are always grouped from 0.

{% endnote %}

To set the interval length:

1. Click on the line ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-reports/profiles__report_group.png) under the attribute name.
2. Set the interval and click **Apply**.

To display all values, enable **No grouping** when setting the interval.

## Metrics {#measure}

Some metrics are displayed as sparklines in the list of attribute values under the chart. The vertical axis shows the number of users and the horizontal axis shows the number of days (sessions). The numbers on the sparklines are [median values](*median values) of metrics. They are marked with dots.

The following metrics are available for analysis:

- **Users**. The number of users with the specified attribute value. The only data source for the chart.

- **Days since installation**. The number of days since installation. It is considered from the time when the profile appeared.

- **Days since last session**. The number of days since the last launch.

- **Sessions**. Total number of sessions.

![](../../_images/profile-report-{{ locale }}.png){style="max-width: 800px;"}

## See also {#learn-more}

- [User profile](../data-collection/about-profiles.md)
- [User profile attributes](../data-collection/profile-attributes.md)
- [Configuring sending profile attributes](../data-collection/about-profiles.md#profile-settings)
- [Profile list](profile-list.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*median values]: The middle value in a sample. This means one half of the sample values are greater than this one, while the other half are less. For example, for the {23, 32, 24, 26, 40} sample the median is equal to 26. To determine the median value, arrange the sample items in ascending or descending order and take the middle item: {23, 24, **26**, 32, 40}. If the sample has an even number of items, the median is half the sum of the two middle items.
