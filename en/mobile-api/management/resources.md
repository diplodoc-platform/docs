# API resources

#|
|| **Operation** | **Description** ||
|| [GET /management/v1/application/{id}](applications/getapplication.md) | Returns information about the specified app. ||
|| [GET /management/v1/applications](applications/getapplicationslist.md) | Returns information about apps available to the user. ||
|| [GET /management/v1/metadata/application/categories](applications/get-categories.md) | Returns a list of all app categories. ||
|| [POST /management/v1/applications](applications/createapplication.md) | Adds an app to AppMetrica. ||
|| [PUT /management/v1/application/{id}](applications/updateapplication.md) | Updates the settings of the specified app. ||
|| [POST /management/v1/application/{id}/grants](applications/access/grant.md) | Grants a certain user or agency permissions to access statistics. ||
|| [PUT /management/v1/application/{id}/grant](applications/access/edit.md) | Updates the previously granted permissions. ||
|| [GET /management/v1/tracking/partners](applications/access/list-partners.md) | Returns a list of partners. ||
|| [GET /v1/traffic/sources/events?appId={id}](applications/access/list-events.md) | Returns a list of custom events. ||
|| [DELETE /management/v1/application/{id}/grant?user_login={login}](applications/access/delete.md) | Removes the previously granted permissions. ||
|| [DELETE /management/v1/application/{id}](applications/deleteapplication.md) | Deletes the specified app. ||
|| [GET /management/v1/application/{id}/events_certs_fingerprints/android](fingerprints/fingerprints-android-get.md) | {{ fingerptints-get }} ||
|| [POST /management/v1/application/{id}/events_certs_fingerprints/android/add](fingerprints/fingerprints-android-post.md) | {{ fingerptints-post }} ||
|| [DELETE /management/v1/application/{id}/events_certs_fingerprints/android/{fingerprint_id}](fingerprints/fingerprints-android-delete.md) | {{ fingerptints-delete }} ||
|| [GET /management/v1/logsapi/status](logs-api-status.md) | Checks the availability of the [Logs API](../logs/about.md). ||
|#

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
