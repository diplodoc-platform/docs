# Limits

The Data Stream API is not available if you:
- Use a free plan.
- Reached the monthly limit on the number of exported events.

Once you exceed the limit, the events export continues for another 7 days, but you aren't able to download the events. Also, the download API returns an error with the `400` HTTP code. If you don't increase the limit after 7 days, event export is stopped and new data is lost.

The limit is updated and export is resumed on the 1st of each month (if you still have the Data Stream API enabled under your pricing plan).

To use the Data Stream API over the limit, enable the option to pay for each additional million events.

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
