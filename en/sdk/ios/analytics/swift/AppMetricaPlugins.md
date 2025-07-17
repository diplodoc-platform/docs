# AppMetricaPlugins protocol

The `AppMetricaPlugins` protocol is an extension of `AppMetricaCrashes`.

You can get an instance of the object that implements `AppMetricaPlugins` by calling the [pluginExtension](AppMetricaCrashes.md#method_pluginExtension) method in [AppMetricaCrashes](AppMetricaCrashes.md).

One `AppMetricaPlugins` instance is created for each reporter. You can request it every time or store a reference for future use.

## Instance methods {#instance_summary}

#|
|| [reportUnhandledException(_:onFailure:)](#method_reportUnhandledException_onFailure) | Sends a message about an unhandled error. ||
|| [reportError(_:message:onFailure:)](#method_reportError_message_onFailure) | Sends an error message. ||
|| [reportError(:withIdentifier:message:details:onFailure:)](#method_reportErrorWithIdentifier_message_details_onFailure) | Sends an error message with a short description. ||
|#

## Method descriptions {#method_detail}

### reportUnhandledException(_:onFailure:) {#method_reportUnhandledException_onFailure}

```swift translate=no
class func reportUnhandledException(_ errorDetails: PluginErrorDetails?, onFailure: ((_ error: (any Error)?) -> Void)? = nil)
```

Sends a  message about an unhandled error. For more information, see [PluginErrorDetails](PluginErrorDetails.md).

**Parameters:**

#|
|| `errorDetails` | Object that describes the error. ||
|| `OnFailure` | Callback method to call if an error occurs while sending the message. The `error` is passed as an argument. ||
|#

### reportError(_:message:onFailure:) {#method_reportError_message_onFailure}

```swift translate=no
class func reportError(_ errorDetails: PluginErrorDetails?, message: String?, onFailure: ((_ error: (any Error)?) -> Void)? = nil)
```

Sends a custom error message. Errors are grouped using `backtrace`. To change the grouping parameter, use [reportErrorWithIdentifier:message:details:onFailure:](#method_reportErrorWithIdentifier_message_details_onFailure). For more information, see [PluginErrorDetails](PluginErrorDetails.md).

**Parameters:**

#|
|| `errorDetails` | Object with error details. ||
|| `message` | Short error description. ||
|| `OnFailure` | Callback method to call if an error occurs while sending the message. The `error` is passed as an argument. ||
|#

### reportError(:withIdentifier:message:details:onFailure:) {#method_reportErrorWithIdentifier_message_details_onFailure}

```swift translate=no
class func reportError(withIdentifier identifier: String?, message: String?, details errorDetails: PluginErrorDetails?, onFailure: ((_ error: (any Error)?) -> Void)? = nil)
```

Sends an error message with a short description. Errors are grouped by the passed ID. To group them using `backtrace` instead, use the [reportError:message:onFailure:](#method_reportError_message_onFailure) method. For more information, see [PluginErrorDetails](PluginErrorDetails.md).


**Parameters:**

#|
|| `identifier` | ID used for grouping. ||
|| `message` | Short error description. ||
|| `errorDetails` | Object with error details.  ||
|| `OnFailure` | Callback method to call if an error occurs while sending the message. The `error` is passed as an argument. ||
|#
