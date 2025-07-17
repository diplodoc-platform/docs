## Modules {#modules}

* `AppMetricaCore`: The mandatory main SDK module. It must be connected for working with AppMetrica.
* `AppMetricaAdSupport`: The module is used to collect IDs, including IDFA.
* `AppMetricaCrashes`: The module is intended for detecting crashes and sending errors.
* `AppMetricaWebKit`: The module enables you to send events from JavaScript code in WebView.

## Excluding the module for children {#for-kids}

{% note info %}

If your app is intended for children, connect modules without the use of `AppMetricaAdSupport`.

{% endnote %}

