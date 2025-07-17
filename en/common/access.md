# Managing app access

To give another user access to your statistics:

1. In the **{{ settings }}** section for your app, go to the **{{ manage-access }}** tab.
2. Enter the Yandex email address (login) of the user to grant access to.  If this person doesn't have a Yandex account, they will have to [create one](https://passport.yandex.{{ domain }}/passport?mode=register).
3. Choose the access level in the drop-down list:

   - **Read only** — The user can view settings and statistics for your app and create and edit [funnels](../mobile-reports/funnels-report.md). They can't edit funnels that were created by other users.

   - **Read/Edit** — The user has full access to app management (except deleting the app).

      You can also add access for an agency and specify events and advertising partners that might be of interest to the agency. There are several access levels available:

   - **Agency: read only** — The user can only view app settings and statistics for selected traffic sources and target events.

   - **Agency: read/edit** — The user can change app settings, configure and create trackers, and view statistics for selected traffic sources and target events.

4. Click **{{ button-add }}**. An email message will be sent to the specified address with a link to the app statistics in the AppMetrica web interface.

## What a user can do with guest access {#guest-access}

#|
|| **Action** | **Read only** | **Read/edit** | **Agency: read** | **Agency: read/edit** ||
|| View the "Traffic sources" report | ![]({{ check }}) | ![]({{ check }}) | ![]({{ check }}) | ![]({{ check }}) ||
|| View all reports | ![]({{ check }}) | ![]({{ check }}) | ![]({{ cross }}) | ![]({{ cross }}) ||
|| View revenue metrics in the [User Acquisition](../mobile-reports/user-acquisition-report.md) and [Remarketing](../mobile-reports/remarketing-report.md) reports | ![]({{ check }}) | ![]({{ check }}) | ![]({{ check }}) | ![]({{ check }}) ||
|| Add new [funnels](../mobile-reports/funnels-report.md) | ![]({{ check }}) | ![]({{ check }}) | ![]({{ cross }}) | ![]({{ cross }}) ||
|| Edit your [funnels](../mobile-reports/funnels-report.md) | ![]({{ check }}) | ![]({{ check }}) | ![]({{ cross }}) | ![]({{ cross }}) ||
|| Edit [funnels](../mobile-reports/funnels-report.md) that were created by other users | ![]({{ cross }}) | ![]({{ check }}) | ![]({{ cross }}) | ![]({{ cross }}) ||
|| Segmentation | ![]({{ check }}) | ![]({{ check }}) | ![]({{ check }}) | ![]({{ check }}) ||
|| Create push campaigns | ![]({{ cross }}) | ![]({{ check }}) | ![]({{ cross }}) | ![]({{ cross }}) ||
|| View destination URLs | ![]({{ check }}) | ![]({{ check }}) | ![]({{ check }}) | ![]({{ check }}) ||
|| View deeplinks | ![]({{ check }}) | ![]({{ check }}) | ![]({{ check }}) | ![]({{ check }}) ||
|| View test devices | ![]({{ check }}) | ![]({{ check }}) | ![]({{ check }}) | ![]({{ check }}) ||
|| Edit existing destination URLs | ![]({{ cross }}) | ![]({{ check }}) | ![]({{ cross }}) | ![]({{ check }}) ||
|| Edit existing deeplinks | ![]({{ cross }}) | ![]({{ check }}) | ![]({{ cross }}) | ![]({{ check }}) ||
|| Edit existing test devices | ![]({{ cross }}) | ![]({{ check }}) | ![]({{ cross }}) | ![]({{ cross }}) ||
|| Add new destination URLs | ![]({{ cross }}) | ![]({{ check }}) | ![]({{ cross }}) | ![]({{ check }}) ||
|| Add new deeplinks | ![]({{ cross }}) | ![]({{ check }}) | ![]({{ cross }}) | ![]({{ check }}) ||
|| Add new test devices | ![]({{ cross }}) | ![]({{ check }}) | ![]({{ cross }}) | ![]({{ check }}) ||
|| Add comments to crash logs | ![]({{ check }}) | ![]({{ check }}) | ![]({{ cross }}) | ![]({{ cross }}) ||
|| Change the app name | ![]({{ cross }}) | ![]({{ check }}) | ![]({{ cross }}) | ![]({{ cross }}) ||
|| View the app's API key | ![]({{ cross }}) | ![]({{ check }}) | ![]({{ cross }}) | ![]({{ cross }}) ||
|| Add new trackers | ![]({{ cross }}) | ![]({{ check }}) | ![]({{ cross }}) | ![]({{ check }}) ||
|| Grant access to other users | ![]({{ cross }}) | ![]({{ check }}) | ![]({{ cross }}) | ![]({{ cross }}) ||
|| Remove app | ![]({{ cross }}) | ![]({{ cross }}) | ![]({{ cross }}) | ![]({{ cross }}) ||
|#

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
