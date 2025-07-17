# Conversions

In AppMetrica, you can configure conversion rules for E-Commerce, Ad revenue, Revenue, and custom events. To set up access for events which you'll use to configure conversion rules, navigate to the [{{ manage-access }}](../common/access.md) section.

To view your configured rules, go to **{{ tracking }}** → **{{ conversions }}**.

![](../../_images/conversions-list-{{ locale }}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

The list displays the rules that were created during a specified period. You can view all rules or only those for a specific type of event.

By default, apps have rules for Revenue, Ad Revenue, and E-Commerce events configured, with all events included and an unlimited attribution window.

To find a rule by its name or note, click **{{ find-conversion }}** above the list.

Rule parameters are set when the rule is created. After that, only the rule name and comment can be edited. To do this, click ![](../../_images/dots.svg) → **{{ edit }}** next to the rule name.

If you no longer need a rule, you can archive it. To do this, click ![](../../_images/dots.svg) → **{{ to-archive }}** next to the rule name. You can switch between the list of active and archived rule versions.

Not all rules can be archived: for example, you can't archive the default rules. If you attempt to archive such a rule, a warning message will appear.

## Creating a conversion rule {#add-conversion}

1. Click **{{ add-conversion }}** to open the rule creation window.

1. Enter a name for your rule. If needed, provide a brief note.

1. Select the event type, then choose the specific event for which you want to count conversions. You don't need to specify an event for the Ad Revenue type.

1. Specify an attribution window, which is the number of days that can pass between an installation or re-engagement and a conversion. Acceptable values are from 1 to 180 days. If no value is specified, the event will have an unlimited attribution window.

1. Select an attribution method:

    - **{{ all-events }}**: Count all target events. Each conversion is attributed separately — to an advertising partner (if the event occurs within the attribution window) or to organic traffic (in other cases).

    - **{{ first-event-only }}**: Count only the first target event on the device, regardless of whether the user clicked an ad or came from organic search results. Subsequent events are ignored.

1. Click **{{ save }}**.

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
