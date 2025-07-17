# Error descriptions

This section lists the error codes returned by the Management API.

## Error format {#errors_description}

```javascript translate=no
{
    "errors" : [ {
        "error_type" : error_type ,
        "message" : string ,
        "location" : string
    }, ... ],
    "code" : int ,
    "message" : string
}
```

#|
|| **Parameters** | **Description** ||
|| `errors` | List of errors that occurred. ||
|| `code` | HTTP status. ||
|| `message` | Reason. ||
|| `errors.error_type` | Type of error. ||
|| `errors.message` | Reason for the error. ||
|| `errors.location` | Place where the error occurred. ||
|#

## Error codes

| Error code | Description |
| ----- | ----- |
| backend_error (503) | Server error. |
| invalid_parameter (400) | Invalid parameter set. |
| not_found (404) | The specified object was not found. |
| missing_parameter (400) | A required parameter was omitted. |
| access_denied (403) | Access denied. |
| unauthorized (401) | Unauthorized user. |
| quota (429) | Exceeded the limit on the number of API requests. |
| query_error (400) | Request is too complex. |
| conflict (409) | Data inconsistency. |
| invalid_json (400) | The transmitted JSON has an invalid format. |

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
