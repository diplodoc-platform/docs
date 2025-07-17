# Restrictions

The Post API has the following restrictions on loading data:

- You can upload events only if the difference between the event date (`event_timestamp`) and the upload date is no more than 14 days.
- You can upload events for identifiers that were previously sent via the SDK.
- You can upload events for profiles that have been updated at least once in the past six months.
- The maximum size of an uploaded file is 1 GB.
- You can upload up to 100,000 events in a single request.
- If `profile_id` was assigned in the first and only session, you can upload an event for it only when you log in to the app again.

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
