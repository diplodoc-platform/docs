# Saving reports

{% include [note-workspaces](_includes/note-workspaces.md) %}

The AppMetrica interface consists of two parts: reports and workspaces. All reports have a default state, which is a set of standard groups and metrics. When you change groups or metrics in AppMetrica, they're saved as a custom set that will be restored the next time you open the report to the state in which you last left it .

If your tasks require that you regularly change report configurations, you can save your configuration for quicker access to the data. Saved information includes the group set, selected grouping values, graph metrics, table metrics, and data segments.

You can find all your saved reports under **{{ saved }}**.

## Saving a report {#save}

After making your changes to a report, you can save it.

{% note info "" %}

Not all reports can be modified or saved.

{% endnote %}

1. In the upper-right corner of the report, select ![](../../_images/dots.svg) → **{{ save-as }}**.
2. In the form, enter the name of your report and save it.

## Changing a saved report {#update}

When using a saved report, you can make changes to it. If you've changed the report settings (the set of metrics, groups, data segments, graph metrics, or selected grouping values), you can either save the changes to the existing report, or as a new one. If you don't save the changes, they'll be reset after you exit the report.

You can also change the name of the saved report on the report page.

## Access rights {#access}

Users with "Read only" access can save custom reports and view reports saved by other users, though they can't edit them.

Users with "Read/write" access can save and edit saved reports no matter who created them.

## Restrictions {#restrictions}

You can save up to 500 reports for a single app. If you have any reports that you no longer need, you can delete them: 

1. In the left side menu, select **{{ reports }}** → **{{ saved }}**.
1. Find the report you want to delete, and on the right click ![](../../_images/dots.svg) → **{{ delete }}**. 

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
