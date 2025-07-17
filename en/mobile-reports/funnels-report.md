# Funnels

The report shows the conversion rate for specified combinations of user actions. Configure 1 to 10 steps by including one or more events from the app in each step.

The conversion rate is the percentage of users who performed a targeted action. AppMetrica counts absolute and relative conversions.

{% cut "Example of absolute conversion" %}

Absolute conversion is the conversion rate from the first to the Nth step. Let's create a three-step funnel:

|  | Step 1 | Step 2 | Step 3 |
| ----- | ----- | ----- | ----- |
| Action | Opened the app | Went to the item info | Added the item to the cart |
| Number of users | 53750 | 10338 | 1290 |
| Absolute conversion | 100% | 19.3% | 2.4% |

Of all users, 1290 added the item to the cart, the absolute conversion in this case is 2.4%.

{% endcut %}

{% cut "Example of relative conversion" %}

Relative conversion is the conversion rate between adjacent steps. Let's add another step to the funnel from the previous example:

|  | Step 1 | Step 2 | Step 3 | Step 4 |
| ----- | ----- | ----- | ----- | ----- |
| Action | Opened the app | Went to the item info | Added the item to the cart | Went to the checkout |
| Number of users | 53750 | 10338 | 1290 | 774 |
| Relative conversion | 100% | 19.3% | 12.5% | 60% |

Of the 1290 users, 774 went to the cart for checkout after adding the item. The relative conversion here is 60%.

{% endcut %}

Funnels help you compare conversion to a target action on different versions of the app, evaluate the dynamics of the conversion of a behavioral scenario, or find out for which section of the audience the app function was needed — the number and percentage.

An **Ad Revenue Event** indicates the fact of receiving revenue from advertising monetization. Learn more about how to configure [transmission of data about advertising monetization (Ad Revenue)](../data-collection/about-adrevenue.md).

## Create a funnel {#create}

To create a new report, click **{{ funnels-button-create }}**.

To edit or copy a funnel, use the buttons ![]({{ edit-icon }}) and ![]({{ copy-icon }}).

{% note alert %}

Users with **Read only** access can only edit and delete their own funnels. For more information, see [Managing app access](../common/access.md).

{% endnote %}

1. Enter a title in the **Funnel name** field.
2. Set 1 to 10 steps using the **{{ funnels-button-add-step }}** and ![]({{ trash-icon }}).

   Enter a name for each step or leave the field empty. Add one or more events via an exclusive "OR".

3. If the app sends multi-level events, in the **Selected events** section, configure filtering by keys and values using the ![]({{ filter-icon }}) button.
4. Check the options in the **Detailed settings** section:

   - **Events between steps** — whether to count the conversion to the next step if an arbitrary event occurred between steps.

      {% cut "Example" %}

      Let's create a three-step funnel:

      | Step 1 | Step 2 | Step 3 |
      | ----- | ----- | ----- |
      | Opened the app | Went to the item info | Added the item to the cart |

      Between step 2 and step 3,  an additional "Added item to favorites" event takes place. In order to count the conversion in **Step 3**, enable the option **Events between steps**.

      {% endcut %}

   - **Event registration** — whether the steps should be completed based on the results of all sessions for the selected period, or strictly within a single session.
   - **Counting metrics** — the calculation of users does not take into account the use of the app in the background, as well as data from devices without configured profiles.

The funnel is ready. Make sure that you have added all possible stages where the target audience is screened out.

## View the report {#view}

To get started, select a funnel from the list or create a new one. The first part of the report displays the final conversion rate, as well as input data and funnel parameters.

1. To filter users, use [segmentation](segmentation.md).
2. Set a time period.
3. Configure the output table:

   - Enable one or more groups using the **{{ dimensions-button }}** button.

      The data will be nested in rows in the order you select them.

      {% cut "Example" %}

      Add the dimensions **Period** → **Date**, **Application** → **Version** and you will get a table with a list of dates. Clicking on the day will open the list of versions of the app. To sort by day in ascending or descending order, click **Date** in the table header. You can group data this way to analyze how the conversion rate changes.

      {% endcut %}

   - To specify the conversion type, use the **{{ funnels-tab-abs-rel }}** option.
   - Set the table display mode to linear or tree view (DrillDown) using the ![]({{ tab__flat-tree }}) option.

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
