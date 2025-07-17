# Creating a segment

{% note alert "" %}

You can configure targeting for Yandex Direct ad campaigns based on AppMetrica segments. To do this, save a segment in AppMetrica and add it to [Yandex Audience](https://yandex.ru/support/audience/segments/app-metrica.html). For more information, see [How to set up retargeting](https://yandex.com/adv/news/how-to-set-up-retargeting-for-ads-for-mobile-apps).

{% endnote %}

To create a new segment:

1. Go to one of the reports in the AppMetrica interface.
2. Click **{{segment-not-selected}}** → **{{any-segment}}** and add conditions. Conditions can be enabled and disabled.

   ![](../../_images/segment-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

3. Click **{{apply}}**. To save the resulting segment, click **{{save-as}}** and enter the segment's name.

Use the same button to add report-level filters for the corresponding reports.

## Example of segmentation {#example}

Obtain session statistics with the following criteria:

- User installed the app while located in Russia.
- User starts the app on a tablet connected via Wi-Fi.
- User completed the **New event** event while located in a different country.

Follow these steps in the AppMetrica interface:

1. Go to the **Audience** report.
2. Click **{{segment-not-selected}}** → **{{any-segment}}**
3. Set custom conditions:
   1. First condition **Installation** → **Geography of installation** → **Russia** → **Apply**.
   2. Second condition **Device** → **Device type** → **Tablet** → **Apply**.

4. Set the report conditions:

   1. First condition → **Events** → **New event** → **Apply**.
   2. Second condition → **Geography** → **Exclude** → **Russia** → **Apply**.
   3. Third condition → **Network** → **Connection type** → **Wi-Fi** → **Apply**.

5. To save a segment, click **Saved segments** → **Save segment**.

This will give you statistics about users who meet your criteria.

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
