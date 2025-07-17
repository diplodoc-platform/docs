This attribution type correctly detects the source that brought users to your app and accurately links app installs to ad interactions, whether they're a click or an impression.

For more information about attribution methods, see [AppMetrica tracking technology](../technology.md) and [Impression attribution](../vta-tracking-specification.md).

{% cut "Available fields" %}

![](../../../_images/attribution-desc-{{ locale }}.png){style="border: solid 1px #cccccc; max-width: 800px;"}  

- **Fingerprint** — Time interval of attribution (the time between the click and first start). AppMetrica uses it for the [Device Fingerprint Matching](../technology.md) attribution. The default value is 24 hours.
   Acceptable values are from 1 to 24 hours.

- **Device ID / Google Referrer** — Time interval of attribution, that is used for the [Device Identifier Matching](../technology.md) attribution. The default value is 10 days.
   Acceptable values are from 1 to 10 days for clicks and up to 24 hours for impressions.

- **Impression attribution**, also known as post-view attribution or view-through attribution (VTA), accounts for cases where a user didn't navigate to the app store by clicking an ad but still installed your app shortly after viewing it. The option is enabled by default. For more information, see [Impression attribution](../vta-tracking-specification.md).

- **Reattribution** — Attribution of reinstalls by pre-existing users. This option is disabled by default. For more information, see [Attributing app installs](../policy.md#reattribution).

   {% note info "" %}

   For test devices, reattribution is always enabled (regardless of the option status). For more information about adding test devices, see [Testing attribution](../testing-attribution.md).

   {% endnote %}

{% endcut %}
