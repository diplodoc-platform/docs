# Introduction

{% note alert %}

The Data Stream API is available on paid plans.

{% endnote %}

Data Stream is a flow of data coming from the app and processed by AppMetrica. The stream is available for export as CSV (the [RFC 4180](https://tools.ietf.org/html/rfc4180) standard) or JSON files. You can set the list of fields for export by sending the [API request](ref/settings-post.md).

The stream is represented by a sequence of 5-minute data windows. You can call the API to download each window as a file in the format you specified during setup. All stream data is stored for 7 days. You can find out the data size and the composition of the fields using the API request.

Non-aggregated data collected for your app can be used to build custom reports or form audiences for retargeting. The following data is available for export:

- Events
- Installations
- Session start
- Push tokens
- Crashes
- Errors
- Clicks and impressions
- Revenue
- Purchases
- Ad Revenue
- Conversions
- Deeplinks

The Data Stream API conforms to the REST principles. Use the [Changing settings](ref/settings-post.md) request to configure data stream export, including event types, field sets, and filters. After you configure the stream, new data is written to files that you can download by sending the [Downloading data](ref/data.md) request.

{% note info %}

The modified settings are applied to new data only. The already generated files don't change.

{% endnote %}

## When to use the Data Stream API {#audiencs}

The Data Stream API can be useful if:

- You need to export data regularly.
- You have a large app or a large package of projects.
- Your export volume exceeds 500,000 records at a time.
- You require frequent exports without limitations.

## Real-time data {#real-time-data}

Usually, the last two five-minute windows gradually grow in size because new data is added to them. That's why we recommend that you download the stream with a 10-minute delay at least. To check whether the data has been updated after downloading, you can view the `update_timestamp` field in the response to the [Stream status](ref/status.md) request. Note that windows may be skipped when the Data Stream service is out of order. In this case, no data is lost, but the first windows will have a larger data size.

{% note info %}

When the Data Stream service is under maintenance, data will be written to files generated after maintenance is completed. That is why they may have a larger size. Even so, all the data is saved and the `event_timestamp` is accurate in all records.

{% endnote %}

## Features and limitations {#plus}

#|
|| Real-time data delay | 10 minutes to stabilize the last pair of five-minute windows ||
|| Request processing queue | No. Files are available immediately ||
|| Data availability for export | History is unavailable once the stream is configured ||
|| File lifetime | 7 days ||
|| Configuring export fields | Yes ||
|| Filtering events by name | Yes, using whitelist and blacklist ||
|| Export format | CSV, JSON ||
|| Compression support | Yes, using gzip encoding ||
|| Requests per day | Up to 50,000 ||
|| Number of parallel downloads | Up to 10 ||
|#

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
