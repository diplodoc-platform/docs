You can export data from a report. 

{% note info "" %}

The data is exported based on the selected report settings: segmentation, dimension, and time period.

{% endnote %}

![](../../../_images/export-data-ua-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 400px;"}

In the upper-right corner click ![](../../../_images/icon-export.svg) and select the action: 

- **Export full report in CSV** to export data from the table in `CSV` format.
- **Chart → CSV** to export data from the chart in `CSV` format.
- **Chart → PNG** to export chart images in `PNG` format.
- **Copy chart API request** — Displays the query text for exporting data from the chart using the [Reporting API](../../mobile-api/logs/about.md). 
- **Copy table API request** — Displays the query text for exporting data from the table using the [Reporting API](../../mobile-api/logs/about.md). 

You can use this query to build your own dashboard or create automated data export scripts.

{% note info %}

If you are getting the text of the query for the first time, make sure that the browser doesn't block the pop-up authorization window. In the authorization window, allow AppMetrica to access the data.

{% endnote %}
