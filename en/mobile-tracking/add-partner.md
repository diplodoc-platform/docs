# Adding a media source

AppMetrica actively partners with advertising platforms to advertise apps. AppMetrica partners are listed in the section [List of advertising networks](../ad-network/integrations/ad-networks-and-technologies.md).

In the service, you can find them under **{{ tracking }}** → **{{ media-sources }}**. If necessary, you can add a media source yourself:

1. Go to **{{ tracking }}** → **{{ media-sources }}** and click **{{ media-source-new }}**.

2. In the window that opens, fill in the information and click **{{ create }}**.

The new media source will be available in the list. You can find media sources you have added by sorting them with the **{{ your }}** button or using the search bar.

![](../../_images/new-publisher-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

{% note info %}

When a media source is deleted, all the report data is saved and available when viewing reports for previous time periods. However, you won't be able to create a new tracker for a deleted media source.

{% endnote %}

## Adding a postback template {#postback-template}

You can create a postback template on the page for the media source (click **{{ create-postback-template }}**).  In the template, choose the type of event that will trigger sending the postback, and form the [postback URL](*postback URL). You can use this link when [setting up the tracker's postback](add-tracker.md) for this media source.

We recommend using [macros](postback-specification.md) for forming the URL.

The template can be helpful if you want to use it in multiple trackers.

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*postback URL]: A link for sending an event message (about an install or a target event). The event recipient is a partner. You can [send additional parameters](postback-specification.md) to the postback URL.
