# Crashes and errors

{% note alert %}

Crash and error reports are very much alike. Therefore, information about them is provided in a single document.

{% endnote %}

You can find the report in the menu on the left, under **{{technology}}**. The report displays information about [Crashes/errors](../data-collection/about-crashes-and-errors.md).

You can use the report to determine which crashes and errors occur most often. Use this information to prepare fixes.

To receive information by email, [set up notifications](../data-collection/crash-mails.md).

You can select specific users for the report using [segmentation](segmentation.md).

## Report period {#period}

The report is formed for a specific time period. The default period is one week.

{% include [period](_includes/period.md) %}

## Dimension {#group}

The data in the report can be grouped by:

- Crash or error group For more information, see [Crashes and errors](../data-collection/about-crashes-and-errors.md).
- App version
- OS version
- Device
- Manufacturer

## Metrics {#measure}

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/crash-report-list.png){style="border: solid 1px #cccccc; max-width: 800px;"}

The following metrics are available for analysis:

- **Crashes/Errors** — The number of crashes or errors.
- **Devices** — The number of devices that registered a crash or error at least once during the selected reporting period.
- **% of all devices** — The percentage of devices that registered the crash or error out of the total number of devices running the app during the selected time period.
- **Detected in version** — The app version where the crash or error was registered for the first time.
- **Last reproduction** — The app version where the crash or error was last registered.

From the **Lists of crashes** page, you can go to the page with information about a crash group. To do this, click the name of the crash group.

## Crash and error symbolication {#symbolization}

If no mapping or dSYM file was uploaded when building the app, the list of groups displays a warning about unsymbolicated crashes.

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/dsym-warning.png){style="border: solid 1px #cccccc; max-width: 800px;"}

To symbolicate them, upload the [Uploading dSYM files on iOS](../data-collection/upload-dsym.md). You can view the list of missing files on the **Settings** → **Crashes** page of your app in AppMetrica.

{% note info %}

You can't upload missing mapping files for previous app builds.

{% endnote %}

## Viewing the crash log and error log {#show-crash-log}

To view the crash log:

1. On the **Crash logs and errors** page, click on the name of the crash group.
2. In the table, click **Open crash log/Open error log**.

The log shows information about the device and crash or error.

To view the events that preceded the crash or error, go from the log to a profile card. To do this, click **View session events**.

## Adding a comment {#comment}

If necessary, you can leave comments on the crash or error. This can be useful if the report is viewed by multiple developers. For example, you can add a link to an issue in a comment in Yandex Tracker.

To add a comment, open the appropriate group and enter your text in the **Comment** field.

## Closing a crash or error {#close-crash}

You can close fixed crashes and errors to filter them out of the report. If a closed crash is detected in versions where it wasn't previously detected, the crash is re-opened.

To close a crash or error, open the appropriate group. In the upper-right corner of the **Crash group status/Error group status** block, set **Closed** mode.

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/crash-group-status.png){style="border: solid 1px #cccccc; max-width: 800px;"}

## Data export {#export}

You can export the crash log description to a TXT file. To do this, open the appropriate crash group and click **Open crash log/Open error log** → **Export**.

### See also

- [Crashes and errors](../data-collection/about-crashes-and-errors.md)
- [Uploading mapping files and debugging symbols on Android](../data-collection/upload-mapping.md)
- [Uploading dSYM files on iOS](../data-collection/upload-dsym.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
