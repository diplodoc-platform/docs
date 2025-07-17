# Quotas

In order to ensure maximum availability of the service, AppMetrica imposes limitations on the rate of API requests from users.

Two types of limits are used simultaneously:

- By IP — Defines the maximum allowed number of requests per second from a single IP address, set to 30.
- By `user_login` — Restricts the number of requests per day from a single user, set to 5000.

The request rate is calculated separately for each of the following groups of API methods:

- `client_read` — Reading parameters for an app or an AppMetrica user account. All the methods in the Management API belong to this group.
- `client_write` — Saving parameters for an app or an AppMetrica user account.
- `report_read` — Getting data from AppMetrica reports. This group includes the Reporting API methods.

## Exceeding quotas

If quotas are exceeded, all further actions by the user are temporarily blocked. In this case, the API returns a response with the HTTP status `420 Too Many Requests`. The message body contains information about the type of quota exceeded.

When an IP quota is exceeded, the user is unblocked when the number of API requests for the last second is less than 30.

When a user exceeds their `user_login` quota, they're automatically unblocked at 00:00 GMT.

{{ feedback }}

<a href="../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
