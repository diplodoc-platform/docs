# AMAAppMetricaPlugins protocol

The `AMAAppMetricaPlugins` protocol is an extension of `AMAAppMetricaCrashes`.

You can get an instance of the object that implements `AMAAppMetricaPlugins` by calling the [pluginExtension](AMAAppMetricaCrashes.md#method_pluginExtension) method in [AMAAppMetricaCrashes](AMAAppMetricaCrashes.md).

One `AMAAppMetricaPlugins` instance is created for each reporter. You can request it every time or store a reference for future use.

## Instance methods {#instance_summary}

#|
|| [-reportUnhandledException:onFailure:](#method_reportUnhandledException_onFailure) | Sends an unhandled error message. ||
|| [-reportError:message:onFailure:](#method_reportError_message_onFailure) | Sends an error message. ||
|| [-reportErrorWithIdentifier:message:details:onFailure:](#method_reportErrorWithIdentifier_message_details_onFailure) | Sends an error message with a short description. ||
|#

## Method descriptions {#method_detail}

### -reportUnhandledException:onFailure: {#method_reportUnhandledException_onFailure}

```objectivec translate=no
- (void)reportUnhandledException:(AMAPluginErrorDetails *)errorDetails
                       onFailure:(nullable void (^)(NSError *error))onFailure
reportUnhandledException(exception:onFailure:);
```

Sends a  message about an unhandled error. For more information, see [AMAPluginErrorDetails](AMAPluginErrorDetails.md).

**Parameters:**

#|
|| `errorDetails` | Object that describes the error. ||
|| `OnFailure` | Callback method to call if an error occurs while sending the message. The `error` is passed as an argument. ||
|#

### -reportError:message:onFailure: {#method_reportError_message_onFailure}

```objectivec translate=no
- (void)reportError:(AMAPluginErrorDetails *)errorDetails
            message:(nullable NSString *)message
          onFailure:(nullable void (^)(NSError *error))onFailure
reportError(error:message:onFailure:);
```

Sends a custom error message. Errors are grouped using `backtrace`. To change the grouping parameter, use [reportErrorWithIdentifier:message:details:onFailure:](#method_reportErrorWithIdentifier_message_details_onFailure). For more information, see [AMAPluginErrorDetails](AMAPluginErrorDetails.md).

**Parameters:**

#|
|| `errorDetails` | Object with error details. ||
|| `message` | Short error description. ||
|| `OnFailure` | Callback method to call if an error occurs while sending the message. The `error` is passed as an argument. ||
|#

### -reportErrorWithIdentifier:message:details:onFailure: {#method_reportErrorWithIdentifier_message_details_onFailure}

```objectivec translate=no
- (void)reportErrorWithIdentifier:(NSString *)identifier
                          message:(nullable NSString *)message
                          details:(nullable AMAPluginErrorDetails *)errorDetails
                        onFailure:(nullable void (^)(NSError *error))onFailure
reportError(identifier:message:error:onFailure:);
```

Sends an error message with a short description. Errors are grouped by the passed ID. To group them using `backtrace` instead, use the [reportError:message:onFailure:](#method_reportError_message_onFailure) method. For more information, see [AMAPluginErrorDetails](AMAPluginErrorDetails.md).


**Parameters:**

#|
|| `identifier` | ID used for grouping. ||
|| `message` | Short error description. ||
|| `errorDetails` | Object with error details.  ||
|| `OnFailure` | Callback method to call if an error occurs while sending the message. The `error` is passed as an argument. ||
|#
