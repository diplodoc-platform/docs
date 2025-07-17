# Deferred deeplinks support

A deferred deeplink is used to transfer parameters to the application at the first start. These parameters can be used to perform actions in the application (to open specific application screen, to display certain content, etc.) depending on the source that led the user.

Unlike regular deeplinks, deferred deeplinks only work at the first application launch.

{% note info "" %}

Deferred deeplinks work only on Android devices.

{% endnote %}

## How deferred deeplinks work  {#process}

The following scheme shows the deferred deeplinks workflow:

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-sdk-dg/deferred-deeplink.png)

1. A user clicks on a tracking link that contains parameters for a deferred deeplink.
1. The tracking URL directs the user to the application store.
1. The user downloads the application.
1. After the first application start, the deferred deeplink parameters are sent to the application. You should perform a [request](android-operations.md#deferreddeeplink-request) to get the parameters.

## How to set up a deferred deeplink {#setup}

1. Specify the link in [tracker](../../../mobile-tracking/add-tracker.md) in the **Deeplink** field — the link will work both as a regular deeplink and as a deferred one.

2. Process the receipt of the deeplink or parameters in your application. For example, call up navigation on the desired screen by executing [request](android-operations.md#deferreddeeplink-request). 
    
    If you are requesting deferred deeplink parameters, make sure that these parameters are available in the deeplink.

{% note warning "" %}

Parameters from the tracking link are not automatically transmitted to the deeplink, but they can be transmitted according to [instructions](../../../mobile-tracking/tracking-specification.md#passing-params). You can transfer parameters in this way to both a regular deeplink and a deferred one.

{% endnote %}

## Error descriptions {#errors}

The `DeferredDeeplinkListener` and `DeferredDeeplinkParametersListener` interfaces contain descriptions of errors that may occur when making the request:

**NOT_A_FIRST_LAUNCH**

The parameters or deferred deeplink can't be obtained since they can only be requested at the initial application start.

The first launch of the application is the session of the process (runtime environment, virtual machine) during which the user first requests the parameters. If the deeplink is present at the time of the request, the listener is invoked synchronously in the same thread. At the next start of the process, the library no longer sees the deferred deeplink and the `NOT_A_FIRST_LAUNCH` error is returned.

**PARSE_ERROR**

Depending on the interface, the error means the following:

* If the `DeferredDeeplinkListener` interface is used: couldn't find the deferred deeplink. This may happen if the referrer didn't contain the `appmetrica_deep_link` parameter.
* If the `DeferredDeeplinkParametersListener` interface is used: the deferred deeplink doesn't contain valid parameters.
   The `PARSE_ERROR` error is returned if one of the following conditions is not met:

   * INSTALL_REFERRER must contain the `appmetrica_deep_link` parameter.
   * The `appmetrica_deep_link` parameter value must contain the valid URI.
   * There must be at least one query parameter in the deeplink URI.

   A valid deeplink example: `sampleapp://samplepath?sampleparam1=samplevalue1`.

## Learn more {#learn-more}

[Requesting deferred deeplink parameters](android-operations.md#deferreddeeplink-parameters-request)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
