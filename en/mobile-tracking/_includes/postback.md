[Postbacks](*Postbacks) are usually necessary when running CPI/CPA campaigns. You can add up to 5 postbacks per tracker.

{% cut "Available fields" %}

![](../../../_images/postback-desc-{{locale}}.png){style="border: solid 1px #cccccc;"}

- **Postback destination** — The partner who will receive the postback.
    If you want to collect your own statistics, you can send the postback to your own server. To do this, [add a media source](../add-partner.md).

- **Event** — The target event that triggers sending the postback to the media source.

    Possible event types:
    - **Install postback**: Send the postback after an attributed install.
    - **Event postback**: Send the postback after an attributed conversion.
    - **E-commerce postback**: E-commerce event.
    - **Purchase postback**: In-app revenue event.
    - **Ad revenue postback**: Ad revenue event.

- **Postback URL** — The postback link. AppMetrica allows transmitting [custom tracking parameters](../postback-specification.md) to the [postback URL](*PostbackURL). By default, the postback URL contains parameters from the media source settings. To change the parameters, click **Edit** (changes will be saved in the media source settings).

    You can set the corresponding option to send the postback only for the first target event. All subsequent events will be ignored.

    {% note info %}

    Some advertising partners can set a permanent Postback URL for their network. In this case, the postback is sent to the partner regardless of other settings. It can't be edited.

    {% endnote %}

- **Re-engagement window** — The maximum amount of time that can pass between the install and the target event. A postback won't be sent to the media source if the target event takes more than the specified time.
- **Send postback on actions of all users** — Postback will be sent for every app user's target event, regardless of the installation source.

   {% note info "" %}

   If you select this option, the attribution source for sending postback is ignored. The partner will receive events from all sources but without attribution parameters.

   To send both attributed and unattributed postbacks, create two postbacks: one with the enabled option and the other with the disabled option.

   {% endnote %}

{% endcut %}
