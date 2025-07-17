# Tracking Petal Ads campaigns

AppMetrica tracks Petal Ads campaigns.

To enable tracking, link your AppMetrica and Petal Ads accounts via the `Petal Ads Link ID` used to attribute the installation source.

To work with Petal Ads campaigns:

## Step 1. Get a Petal Ads Link ID {#get-link-id}

1. Open Petal Ads, then go to {% if locale == 'en' %}**Tools** → **Events and assets**{% endif %}.
2. On the {% if locale == 'en' %}**Events and assets**{% endif %} page, click {% if locale == 'en' %}**+Add asset**{% endif %}.
3. Select the asset type {% if locale == 'en' %}**App (Applicable to Android apps)**{% endif %} and click {% if locale == 'en' %}**Next**{% endif %}.
4. Select the app from the list. In the {% if locale == 'en' %}**Analytics tool**{% endif %} line, select **AppMetrica** and click {% if locale == 'en' %}**Submit**{% endif %}.
5. On the {% if locale == 'en' %}**Events and assets**{% endif %} page, you can see the added asset and its **Link ID**. This **Link ID** is used to create a tracker.

   ![](../../_images/link-id-petal-ads-{{ locale }}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

6. On the right of the screen, click {% if locale == 'en' %}**+Add event**{% endif %}.

   {% note info %}

   If {% if locale == 'en' %}**Smart tracking**{% endif %} is enabled, you don't need to add an event.

   If {% if locale == 'en' %}**Smart tracking**{% endif %} is disabled, you need to import each event on the ad network side. To do this, click {% if locale == 'en' %}**+Add event**{% endif %} and select the event corresponding to the specified postback.

   {% endnote %}

7. Select {% if locale == 'en' %}**Activation**{% endif %} as the event type and {% if locale == 'en' %}**Analytics tool tracking**{% endif %} as data source, then click **OK**.

## Step 2. Create a tracker in AppMetrica {#create-tracker}

1. Go to **Campaign details** and choose **Petal Ads** as a media source.
2. In the section that opens, specify the **Petal Ads Link ID** you obtained in [Step 1](#get-link-id).
3. _(Optional)_ To track conversions in Petal Ads, set up sending target events in the **Postback settings** of AppMetrica. More information about setting up [postbacks](add-tracker.md#step5).

   {% note alert %}

   You don't need to configure **Install postback** for Petal Ads.

   {% endnote %}

4. For Petal Ads partners, postback templates are pre-configured, and you can select the ones you need.

   ![](../../_images/petal-ads-postback-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
