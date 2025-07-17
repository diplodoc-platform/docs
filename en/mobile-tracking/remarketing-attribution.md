# Attributing remarketing campaigns

AppMetrica attributes [remarketing campaigns](*remarketing campaign). You can use a remarketing campaign to re-attract an audience, for example, to return users to the app so they complete a target action.

AppMetrica attributes returning users ([re-engagement](*re-engagement)) and new installations if users haven't installed the app previously. Re-engagement metrics are shown in the [Remarketing](../mobile-reports/remarketing-report.md) report, and new installations are shown in the [User Acquisition](../mobile-reports/user-acquisition-report.md) report.

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-tracking/remarketing-attribution.png)

AppMetrica saves the attribution history and doesn't overwrite install source data. Thus, after a remarketing campaign, the user has two sources: one for the installation, and one for re-engagement. When you create a remarketing tracker, you can disable sending CPA postbacks to installation partners.

To enable attribution of remarketing campaigns, you should prepare your app and create a remarketing tracker. For more information, see [How to create a remarketing campaign in AppMetrica](../troubleshooting/troubleshooting.md#remarketing-campaign).

## Learn more {#learn-more}

- [How to create a remarketing tracker](add-remarketing-tracker.md)
- [Remarketing report](../mobile-reports/remarketing-report.md)
- [Tracking link structure and parameters](tracking-specification.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*remarketing campaign]: An ad campaign aimed at getting users to come back to an app they previously installed. For more information, see [Creating a remarketing tracker](add-remarketing-tracker.md).

[*re-engagement]: {{ re-engagement }}.
