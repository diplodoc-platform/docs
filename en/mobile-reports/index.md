# Reports

In the [AppMetrica web interface](http://appmetrika.yandex.{{ domain }}/), you can view statistics on mobile app usage. To collect statistics, you need to [integrate the AppMetrica SDK in the app](../common/quick-start.md).

To view statistics, select **{{ reports }}** in the menu and click the desired report.

The reports are divided into groups according to the topic. In addition to groups by topics, there are also the following general groups:

- **{{ all-reports }}**: Alphabetical list of reports.
- **{{ saved }}**: Reports [saved](save-reports.md) by you and other users. Next to each report, you'll see the avatar of the user who saved it. When you hover over a user's avatar, you'll see their username.
- **{{ popular }}**: Reports you view most frequently. Each user gets a personalized list of their most popular reports. When you are just getting started and your personal list hasn’t been generated yet, you’ll see a default set of reports.

{% note info "" %}

If you have any ideas or suggestions on how to improve reports, please share them with us! You can access the feedback form from any report: click ![](../../_images/icon-feedback.svg) in the upper-right corner of the report page.

{% endnote %}

The data that is displayed in the reports can be exported by using the [Reporting API](../mobile-api/api_v1/intro.md). The API request text can be copied from the report interface, e.g [report on audience](audience-report.md).

Reports in AppMetrica:

- Marketing

  - [User Acquisition](user-acquisition-report.md)
  - [User Acquisition SKAdNetwork](user-acquisition-skadnetwork.md)
  - [Remarketing](remarketing-report.md)
  - [Push campaigns](push-campaign.md)
  - [Conversions](conversions-report.md)

- Product

  - [Events](events-report.md)
  - [Funnels](funnels-report.md)
  - [Retention analysis](retention-report.md)
  - [Cohort analysis](cohort-report.md)
  - [Engagement](engagement-report.md)
  - [Audience](audience-report.md)
  - [Profiles](profile-report.md)
  - [List of profiles](profile-list.md)

- Monetization

  - [In-app and Ad Revenue](revenue-report.md)
  - [E-commerce](ecommerce-report.md)

- Technologies

  - App versions
  - Operating systems
  - Manufacturers
  - Device models
  - Device type
  - Interface language
  - Screens
  - Root status
  - SDK Version
  - KitVersion
  - Operators
  - Connection type

- Crashes and errors

  - [Crashes](crashes-and-errors.md)
  - [Errors](crashes-and-errors.md)
  - [ANRs](anr.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
