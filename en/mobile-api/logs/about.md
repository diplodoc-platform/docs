# Logs API

You can use the Logs API to obtain non-aggregated data from your AppMetrica application. This data is useful for building custom reports or forming audiences for retargeting. The following tracking data is available:

- [Clicks/impressions](endpoints.md#clicks)
- [Openings via deeplink](endpoints.md#deeplinks)
- [Postbacks](endpoints.md#postback)

As well as app information:

- [Installs](endpoints.md#installations), including from partners.
- [Events](endpoints.md#events).
- [Profiles](endpoints.md#profiles).
- [In-app purchases](endpoints.md#revenue).
- [Push tokens](endpoints.md#push-tokens).
- [Crashes](endpoints.md#crashes).
- [Errors](endpoints.md#errors).
- [Session starts](endpoints.md#sessions_starts).
- [Ad Revenue](endpoints.md#ad_revenue).
- [E-commerce](endpoints.md#ecommerce).

The API is implemented as a RESTful HTTP interface. You can build a request for specific data fields and set filters for the data query. AppMetrica queues the request and prepares a file for downloading when ready.

## Data export in the AppMetrica web interface {#export-data}

The **data export** tool lets you download your app data in CSV or JSON format, as well as form requests to the Logs API for further use if you don't have enough expertise for making requests.

To download a file or form a request, just go to the **Apps** → **Data export** section and fill in the necessary fields. For example:

- **Date range** — The time period to get data for.
- **Date dimension** — The time on the device or the time the event was received on the server. These might be different if the event occurred on a device that wasn't connected to the internet. In this case, it is sent to the server after the device is connected to the internet.
- **Data fields** — The data you want to get (for example, the time of an app install).
- **Filtering** — To exclude certain data from the report (for example, to get statistics only on [organic sources](../../common/glossary.md)).
- **Result format** — CSV or JSON.

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-api/data-logs.png){style="border: solid 1px #cccccc; max-width: 800px;"}

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
