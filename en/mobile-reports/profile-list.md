# Profile list

The report displays the full list of user profiles in a table. You can use the report to evaluate statistics by profile attributes and go to the profile card.

To customize the set of columns, click **{{ profile-report-column-button }}** and select the required attributes from the list.

You can select specific users for the report using [segmentation](segmentation.md).

You can see detailed information about a specific profile in the profile card. Click the profile to go to the card.

## Profile card {#profile-card}

The profile card displays:

- A list of attributes and their values.
- Event timeline by session.

You can use the profile cards to learn about typical users who complete the target event. You can use this data for advertising and push campaigns. You can also use the event history to understand what helps or hinders conversion and what leads to a crash or an error in the app.

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-reports/profile-card.png)

The event timeline displays:

- Sent custom events that have been configured in the application.
- Events that have been sent automatically by the AppMetrica SDK: application start, crashes, and errors.

The event timeline is displayed for a specific time period (a week by default). The date range can be set via the ![](../../_images/button-date-{{locale}}.png =x30) dropdown element.

To view the passed values of the events or the log description, click on the event or error in the list.

### See also

- [User profile](../data-collection/about-profiles.md)
- [User profile attributes](../data-collection/profile-attributes.md)
- [Configuring sending profile attributes](../data-collection/about-profiles.md#profile-settings)
- [Profiles report](profile-report.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
