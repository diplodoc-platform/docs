# API resources

#|
|| **Operation** | **Method and resource** ||
|| Creating a group | [POST /push/v1/management/groups](post-groups.md) ||
|| Getting a list of groups | [GET /push/v1/management/groups](get-groups.md) ||
|| Getting a group | [GET /push/v1/management/group/{groupId}](get-group-id.md) ||
|| Updating a group | [PUT /push/v1/management/group/{groupId}](put-group-id.md) ||
|| Archiving a group | [DELETE /push/v1/management/group/{groupId}](delete-group-id.md) ||
|| Unarchiving a group | [POST /push/v1/management/group/{groupId}/restore](post-group-id.md) ||
|| Sending batch push messages | [POST /push/v1/send-batch](post-send-batch.md) ||
|| Checking a sending status by transferId | [GET /push/v1/status/{transferId}](get-status-id.md) ||
|| Checking a sending status by clientTransferId | [GET /push/v1/status/{groupId}/{clientTransferId}](get-status-group-id.md) ||
|#

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
