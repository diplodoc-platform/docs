# Usage examples

## Library initialization with the extended configuration {#initialize}

To initialize the library with the extended startup configuration:

{% list tabs group=instructions %}

- Swift

   1. Initialize an instance of the `AppMetricaConfiguration` class.
   2. Specify the configuration settings using methods of the `AppMetricaConfiguration` class. For example, enable logging or set a session timeout.
   3. Pass the `AppMetricaConfiguration` instance to the `activate(with:)` method of the `AppMetrica` class.

   The parameters of the extended configuration are applied from the time of library initialization. To configure the library while the app is running, use the `AppMetrica` class methods.

   ```swift translate=no
   func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey : AnyObject]? = nil) -> Bool {
       // Creating an extended library configuration.
       if let configuration = AppMetricaConfiguration(apiKey: "API key") {
           // Setting up the configuration. For example, to enable logging.
           configuration.areLogsEnabled = true
           // ...
           // Initializing the AppMetrica SDK.
           AppMetrica.activate(with: configuration)
       }
   }
   ```

- Objective-c

   1. Initialize an instance of the `AMAAppMetricaConfiguration` class.
   2. Specify the configuration settings using methods of the `AMAAppMetricaConfiguration` class. For example, enable logging or set a session timeout.
   3. Pass the `AMAAppMetricaConfiguration` instance to the `+activateWithConfiguration:` method of the `AMAAppMetrica` class.

   The parameters of the extended configuration are applied from the time of library initialization. To configure the library while the app is running, use the `AMAAppMetrica` class methods.

   ```obj-c translate=no
   - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
   {
       // Creating an extended library configuration.
       AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithAPIKey:@"API key"];
       // Setting up the configuration. For example, to enable logging.
       configuration.logsEnabled = YES;
       // ...
       // Initializing the AppMetrica SDK.
       [AMAAppMetrica activateWithConfiguration:configuration];
       return YES;
   }
   ```

{% endlist %}

{% cut "What is an API key?" %}

{{ api-key }}

{% endcut %}

## Sending statistics to an additional API key {#reporter-different-apikey}

Sending data to an additional API key allows you to collect own statistics for these API keys. You can use this to control access to information for other users. For example, to provide access to statistics for analysts you can duplicate sending marketing data for the additional API key. Thus they will only have access to the information they need.

To send data to an additional API key, you must use reporters. Just like for the main API key, you can set up an extended startup configuration for a reporter, send events, profile information, and data about in-app purchases. The reporter can work without the AppMetrica SDK initialization.

### Step 1. (Optional) Initialize a reporter with an extended configuration {#reporter-different-apikey-initialize}

{% note warning %}

The reporter with the extended configuration should be initialized before the first call to the reporter. Otherwise, the reporter will be initialized without a configuration.

{% endnote %}

To initialize a reporter with an extended configuration:

{% list tabs group=instructions %}

- Swift

   1. Initialize an instance of the `MutableReporterConfiguration` class.
   2. Specify the configuration settings using methods of the `MutableReporterConfiguration` class. For example, enable logging or set a session timeout.
   3. Pass the `MutableReporterConfiguration` instance to the `activateReporter(with:)` method of the `AppMetrica` class.
   4. This configuration is used for a reporter with the specified API key. You can set up your own configuration for each additional API key.

   ```swift translate=no
   // Creating an extended library configuration.
   // To create it, pass an API key that is different from the app's API key.
   if let reporterConfiguration = MutableReporterConfiguration(apiKey: "API key") {
       // Setting up the configuration. For example, to enable logging.
       reporterConfiguration.areLogsEnabled = true
       // ...
       // Initializing a reporter.
       AppMetrica.activateReporter(with: reporterConfiguration)
   }
   ```

- Objective-c

   1. Initialize an instance of the `AMAMutableReporterConfiguration` class.
   2. Specify the configuration settings using methods of the `AMAMutableReporterConfiguration` class. For example, enable logging or set a session timeout.
   3. Pass the `AMAMutableReporterConfiguration` instance to the `+activateReporterWithConfiguration:` method of the `AMAAppMetrica` class.
   4. This configuration is used for a reporter with the specified API key. You can set up your own configuration for each additional API key.

   ```obj-c translate=no
   // Creating an extended library configuration.
   // To create it, pass an API key that is different from the app's API key.
   AMAMutableReporterConfiguration *reporterConfiguration = [[AMAMutableReporterConfiguration alloc] initWithAPIKey:@"API key"];
   // Setting up the configuration. For example, to enable logging.
   reporterConfiguration.logsEnabled = YES;
   // ...
   // Initializing a reporter.
   [AMAAppMetrica activateReporterWithConfiguration:[reporterConfiguration copy]];
   ```

{% endlist %}

{% cut "What is an API key?" %}

{{ api-key }}

{% endcut %}

### Step 2. Configure sending data using a reporter {#reporter-different-apikey-send}

To send statistics data to another API key:

{% list tabs group=instructions %}

- Swift

   1. Use the `reporter(for:)` method of the `AppMetrica` class to get the instance that implements the `AppMetricaReporting` protocol.

      If the reporter was not initialized with the extended configuration, calling this method will initialize the reporter for the specified API key.

   2. Use methods of the `AppMetricaReporting` protocol to send events and revenue.
   3. To ensure that sessions are tracked correctly, set up sending session start and pause events for each reporter.


   ```swift translate=no
   guard let reporter = AppMetrica.reporter(for: "API key") else {
       print("REPORT ERROR: Failed to create AppMetrica reporter")
       return // or return someDefaultValue or throw someError
   }
   reporter.resumeSession()
   // ...
   reporter.reportEvent(name: "Updates installed", onFailure: { (error) in
       print("REPORT ERROR: %@", error.localizedDescription)
   })
   // ...
   reporter.pauseSession()
   ```

- Objective-C

   1. Use the `+reporterForAPIKey:` method of the `AMAAppMetrica` class to get the instance that implements the `AMAAppMetricaReporting` protocol.

      If the reporter was not initialized with the extended configuration, calling this method will initialize the reporter for the specified API key.

   2. Use methods of the `AMAAppMetricaReporting` protocol to send events and revenue.
   3. To ensure that sessions are tracked correctly, set up sending session start and pause events for each reporter.

   ```obj-c translate=no
   id<AMAAppMetricaReporting> reporter = [AMAAppMetrica reporterForAPIKey:@"API key"];
   [reporter resumeSession];
   // ...
   [reporter reportEvent:@"Updates installed" onFailure:^(NSError *error) {
       NSLog(@"REPORT ERROR: %@", [error localizedDescription]);
   }];
   // ...
   [reporter pauseSession];
   ```

{% endlist %}

{% cut "What is an API key?" %}

{{ api-key }}

{% endcut %}

## Tracking app crashes {#set-report-crash}

Reports on app crashes are sent by default.

To disable automatic tracking, pass the configuration in which sending crashes is disabled to the crash module.

{% list tabs group=instructions %}

- Swift

   To do this, set the `false` value for the `autoCrashTracking` property of the `AppMetricaCrashesConfiguration` configuration.

   ```swift translate=no
   // Creating a crashes configuration.
   let configuration = AppMetricaCrashesConfiguration()
   // Disabling sending the information on crashes of the application.
   configuration.autoCrashTracking = false
   // Set the configuration for AppMetricaCrashes.
   AppMetricaCrashes.crashes().setConfiguration(configuration)
   ```

- Objective-C

   To do this, set the `NO` value for the `autoCrashTracking` property of the `AMAAppMetricaCrashesConfiguration` configuration.

   ```obj-c translate=no
   // Creating a crashes configuration.
   AMAAppMetricaCrashesConfiguration *configuration = [[AMAAppMetricaCrashesConfiguration alloc] init];
   // Disabling sending the information on crashes of the application.
   configuration.autoCrashTracking = NO;
   // Set the configuration in AppMetricaCrashes.
   [[AMAAppMetricaCrashes crashes] setConfiguration:configuration];
   ```

{% endlist %}

## Determining the location {#track-location}

AppMetrica can determine the location of a device. Location accuracy depends on the configuration that the library uses for initialization:

1. With the `locationTracking` option enabled. For iOS, the option is enabled by default.

   The location is determined with accuracy to the city. You can retrieve this information in [reports](../../../mobile-reports/index.md) and via the [Logs API](../../../mobile-api/logs/about.md).

   The app requests GPS access. Battery consumption may increase.

2. With the `locationTracking` option disabled.

   The location is determined by the IP address with accuracy to the country. You can retrieve this information in [reports](../../../mobile-reports/index.md) and via the [Logs API](../../../mobile-api/logs/about.md).

   The app requests GPS access. Battery consumption does not increase.

   {% note info %}

   If you have enabled IP address masking, AppMetrica determines location with the accuracy to the country by the unmasked part of the IP address.

   {% endnote %}

By default, the AppMetrica SDK is initialized with `locationTracking` enabled, but it doesn't request permission to get location data. You should implement this using methods of the [CLLocationManager](https://developer.apple.com/documentation/corelocation/cllocationmanager?language=objc) class.

{% list tabs group=instructions %}

- Swift

   To initialize a library with `locationTracking` disabled, set the `locationTracking` property of the `AppMetricaConfiguration` configuration to `false`.

   ```swift translate=no
   // Creating an extended library configuration.
   if let configuration = AppMetricaConfiguration(apiKey: "API key") {
       // Disabling sending information about the location of the device.
       configuration.locationTracking = false
       // Initializing the AppMetrica SDK.
       AppMetrica.activate(with: configuration)
   }
   ```

   To disable `locationTracking` after initializing the library, use the `isLocationTrackingEnabled` property of the `AppMetrica` class:

   ```swift translate=no
   AppMetrica.isLocationTrackingEnabled = false
   ```

- Objective-C

   To initialize a library with `locationTracking` disabled, set the `locationTracking` property of the `AMAAppMetricaConfiguration` configuration to `NO`.

   ```obj-c translate=no
   // Creating an extended library configuration.
   AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithAPIKey:@"API key"];
   // Disabling sending information about the device location.
   configuration.locationTracking = NO;
   // Initializing the AppMetrica SDK.
   [AMAAppMetrica activateWithConfiguration:configuration];
   ```

   To disable `locationTracking` after initializing the library, use the `+setLocationTrackingEnabled:` method of the `AMAAppMetrica` class:

   ```obj-c translate=no
   AMAAppMetrica.locationTrackingEnabled = NO;
   ```

{% endlist %}

## Setting device location manually {#location-manual}

Before sending custom information about the device location, make sure that reporting is enabled.

By default, the device location is detected by the library.

{% list tabs group=instructions %}

- Swift

   To send custom device location, pass the [CLLocation](https://developer.apple.com/documentation/corelocation/cllocation) instance to the `customLocation` property of the `AppMetrica` class.

   ```swift translate=no
   func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
       AppMetrica.customLocation = locations.last
   }
   ```

   To send custom device location using the startup configuration, pass the [CLLocation](https://developer.apple.com/documentation/corelocation/cllocation) instance to the `customLocation` property of the `AppMetricaConfiguration` configuration.

   ```swift translate=no
   // Creating an extended library configuration.
   if let configuration = AppMetricaConfiguration(apiKey: "API key") {
     // Set a custom location.
     configuration.customLocation = CLLocation(latitude: 0, longitude: 0)
     // Initializing the AppMetrica SDK.
     AppMetrica.activate(with: configuration)
   }
   ```

- Objective-C

   To send custom device location, pass the [CLLocation](https://developer.apple.com/documentation/corelocation/cllocation) instance to the `setCustomLocation` method of the `AMAAppMetrica` class.

   ```obj-c translate=no
   - (void)locationManager:(CLLocationManager *)manager
       didUpdateToLocation:(CLLocation *)newLocation
              fromLocation:(CLLocation *)oldLocation
   {
       AMAAppMetrica.customLocation = newLocation;
   }
   ```

   To send custom device location using the startup configuration, pass the [CLLocation](https://developer.apple.com/documentation/corelocation/cllocation) instance to the `customLocation` property of the `AMAAppMetricaConfiguration` configuration.

   ```obj-c translate=no
   // Creating an extended library configuration.
   AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithAPIKey:@"API key"];
   // Set a custom location.
   configuration.customLocation = [[CLLocation alloc] initWithLatitude:0 longitude:0];
   // Initializing the AppMetrica SDK.
   [AMAAppMetrica activateWithConfiguration:configuration];
   ```

{% endlist %}

## Sending a custom event {#report-event}

{% list tabs group=instructions %}

- Swift

   To send a custom event without nested parameters, pass the following parameters to the `reportEvent(name:onFailure:)` method of the `AppMetrica` class:

   * `name`: Short name or description of the event.
   * `onFailure`: The block the error is passed to. If you do not want to track the error, pass `nil` for this block.

   ```swift translate=no
   var message = "Updates installed"
   AppMetrica.reportEvent(name: message, onFailure: { (error) in
       print("DID FAIL TO REPORT EVENT: %@", message)
       print("REPORT ERROR: %@", error.localizedDescription)
   })
   ```

- Objective-C

   To send a custom event without nested parameters, pass the following parameters to the `+reportEvent:onFailure:` method of the `AMAAppMetrica` class:

   * `message`: Short name or description of the event.
   * `onFailure`: The block the error is passed to. If you do not want to track the error, pass `nil` for this block.

   ```obj-c translate=no
   NSString *message = @"Updates installed";
   [AMAAppMetrica reportEvent:message onFailure:^(NSError *error) {
       NSLog(@"DID FAIL REPORT EVENT: %@", message);
       NSLog(@"REPORT ERROR: %@", [error localizedDescription]);
   }];
   ```

{% endlist %}

## Sending a custom event with nested parameters {#report-event-params}

{% list tabs group=instructions %}

- Swift

   To send a custom event with nested parameters, pass the following parameters to the `reportEvent(name:parameters:onFailure:)` method of the `AppMetrica` class:

   * `name`: Short name or description of the event.
   * `parameters`: Nested parameters as key-value pairs.

      The AppMetrica web interface displays up to five nesting levels for events. So if an event has six or more levels, only the top five are shown in the report. You can use the [Reporting API](../../../mobile-api/api_v1/intro.md) to export up to ten levels.

   * `onFailure`: The block the error is passed to. If you do not want to track the error, pass `nil` for this block.

   ```swift translate=no
   var message = "Updates installed"
   let params = ["key1": "value1", "key2": "value2"]
   AppMetrica.reportEvent(name: message, parameters: params, onFailure: { (error) in
       print("DID FAIL REPORT EVENT: %@", message)
       print("REPORT ERROR: %@", error.localizedDescription)
   })
   ```

- Objective-C

   To send a custom event with nested parameters, pass the following parameters to the `+reportEvent:parameters:onFailure:` method of the `AMAAppMetrica` class:

   * `message`: Short name or description of the event.
   * `parameters`: Nested parameters as key-value pairs.

      The AppMetrica web interface displays up to five nesting levels for events. So if an event has six or more levels, only the top five are shown in the report. You can use the [Reporting API](../../../mobile-api/api_v1/intro.md) to export up to ten levels.

   * `onFailure`: The block the error is passed to. If you do not want to track the error, pass `nil` for this block.

   ```obj-c translate=no
   NSString *message = @"Updates installed";
   NSDictionary *params = @{@"key1": @"value1", @"key2": @"value2"};
   [AMAAppMetrica reportEvent:message parameters:params onFailure:^(NSError *error) {
       NSLog(@"DID FAIL REPORT EVENT: %@", message);
       NSLog(@"REPORT ERROR: %@", [error localizedDescription]);
   }];
   ```

{% endlist %}

For more information about events, see [Events](../../../data-collection/about-events.md).

## Sending an event from the WebView's JavaScript code{#js-event}

The AppMetrica SDK lets you send client events from JavaScript code. To do this, you need to connect the `AppMetricaWebKit` module via the dependency management system that you're using.

{% list tabs group=instructions %}

- Swift

   Add the import:
   ```swift translate=no
   import AppMetricaWebKit
   ```

   Initialize the sending by calling the `setupWebViewReporting(with:onFailure:)` method:

   ```swift translate=no
   let userController = WKUserContentController()
   AppMetrica.setupWebViewReporting(with: JSController(userContentController:userController), onFailure: nil)
   userController.add(myHandler, name: myScriptName)
   let configuration = WKWebViewConfiguration()
   configuration.userContentController = userController;
   let webView = WKWebView(frame: .zero, configuration: configuration)
   ```

- Objective-C

   Add the import:

   ```obj-c translate=no
   #import <AppMetricaWebKit/AppMetricaWebKit.h>
   ```

   Initialize the sending by calling the `+setupWebViewReporting:onFailure:` method:

   ```obj-c translate=no
   WKUserContentController *userController = [[WKUserContentController alloc] init];
   [AMAAppMetrica setupWebViewReporting:[[AMAJSController alloc] initWithUserContentController:userController] onFailure:nil];
   [userController addScriptMessageHandler:myHandler name:myScriptName];
   WKWebViewConfiguration *configuration = [[WKWebViewConfiguration alloc] init];
   configuration.userContentController = userController;
   WKWebView *webView = [[WKWebView alloc] initWithFrame:CGRectZero configuration:configuration];
   ```

{% endlist %}

Call this method before loading any content. We recommend calling this method before creating a webview and before adding your scripts to [WKUserContentController](https://developer.apple.com/documentation/webkit/wkusercontentcontroller).

To send an event from JavaScript code, use the `reportEvent(name, value)` method in the AppMetrica interface:

```javascript translate=no
function buttonClicked() {
  AppMetrica.reportEvent('Button clicked!', '{}');
}
```

Arguments of the `reportEvent` method:

* `name`: A string. Can't be `null` or empty.
* `value`: A JSON string. Can be `null`.

## Sending a custom error message {#send-report-error}

To send an error message, you need to connect the `AppMetricaCrashes` module via the dependency management system that you're using.

{% list tabs group=instructions %}

- Swift

   To send a custom error message, add the import:

   ```swift translate=no
   import AppMetricaCrashes
   ```

   Then use the methods of the `AppMetricaCrashes` class and the `AppMetricaCrashReporting` protocol:

   * `report(error:onFailure:)`
   * `report(error:options:onFailure:)`
   * `report(nserror:onFailure:)`
   * `report(nserror:options:onFailure:)`

   To send error messages, you can use the standard [NSError](https://developer.apple.com/documentation/foundation/nserror?changes=_1) class, the simplified `AppMetricaError` class, or the `ErrorRepresentable` protocol.

- Objective-C

   To send a custom error message, add the import:

   ```obj-c translate=no
   #import <AppMetricaCrashes/AppMetricaCrashes.h>
   ```

   Then use the methods of the `AMAAppMetricaCrashes` class and the `AMAAppMetricaCrashReporting` protocol:

   * `-reportError:onFailure:`
   * `-reportError:options:onFailure:`
   * `-reportNSError:onFailure:`
   * `-reportNSError:options:onFailure:`

   To send error messages, you can use the standard [NSError](https://developer.apple.com/documentation/foundation/nserror?changes=_1) class, the simplified `AMAError` class, or the `AMAErrorRepresentable` protocol.

{% endlist %}

### Example with NSError {#send-report-error-nserror}

If errors are sent using the [NSError](https://developer.apple.com/documentation/foundation/nserror?changes=_1&language=objc) class, they're grouped by the [domain](https://developer.apple.com/documentation/foundation/nserror/1413924-domain?changes=_1) domain and the [code](https://developer.apple.com/documentation/foundation/nserror/1409165-code?changes=_1) error code.

{% list tabs group=instructions %}

- Swift

   ```swift translate=no
   let firstError = NSError(domain: "io.appmetrica.error-a", code: 12, userInfo: [
       BacktraceErrorKey: Thread.callStackReturnAddresses,
       NSLocalizedDescriptionKey: "Error A"
   ])
   AppMetricaCrashes.crashes().report(nserror: firstError)
   ```

- Objective-C

   ```obj-c translate=no
   NSError *firstError = [NSError errorWithDomain:@"io.appmetrica.error-a"
                                             code:12
                                         userInfo:@{
                                              AMABacktraceErrorKey: NSThread.callStackReturnAddresses,
                                              NSLocalizedDescriptionKey: @"Error A"
                                         }];
   [[AMAAppMetricaCrashes crashes] reportNSError:firstError onFailure:nil];
   ```

{% endlist %}

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/domain-groups.png){style="border: solid 1px #cccccc;"}

### Example with AppMetricaError {#send-report-error-appmetricaerror}

{% list tabs group=instructions %}

- Swift

   If errors are sent using the `AppMetricaError` class or the `ErrorRepresentable` protocol, they're grouped by the `identifier`.

   ```swift translate=no
   let underlyingError = AppMetricaError(identifier: "Underlying AMAError")
   let error = AppMetricaError(
       identifier: "AMAError identifier",
       message: "Another custom message",
       parameters: [
           "foo": "bar"
       ],
       backtrace: Thread.callStackReturnAddresses,
       underlyingError: underlyingError
   )
   AppMetricaCrashes.crashes().report(error: error)
   ```

- Objective-C

   If errors are sent using the `AMAError` class or the `AMAErrorRepresentable` protocol, they're grouped by the `identifier`.

   ```obj-c translate=no
   AMAError *underlyingError = [AMAError errorWithIdentifier:@"Underlying AMAError"];
   AMAError *error = [AMAError errorWithIdentifier:@"AMAError identifier"
                                           message:@"Another custom message"
                                        parameters:@{ @"foo": @"bar" }
                                         backtrace:NSThread.callStackReturnAddresses
                                   underlyingError:underlyingError];
   [[AMAAppMetricaCrashes crashes] reportError:error onFailure:nil];
   ```

{% endlist %}

Don't use variable values as grouping IDs. Otherwise, the number of groups increases and it becomes difficult to analyze them.

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/id-groups.png){style="border: solid 1px #cccccc;"}

## Sending ProfileId {#send-profile-id}

If you don't configure `ProfileId` sending in the SDK, the web interface displays the `appmetrica_device_id` value.

{% list tabs group=instructions %}

- Swift

   To send the `ProfileId`, use the `userProfileID` property of the `AppMetrica` class.

   ```swift translate=no
   AppMetrica.userProfileID = "id"
   ```

- Objective-C

   To send the `ProfileId`, use the `+setUserProfileID:` method of the `AMAAppMetrica` class.

   ```obj-c translate=no
   AMAAppMetrica.userProfileID = @"id";
   ```

{% endlist %}

## Sending events from the buffer {#send-events-buffer}

AppMetrica SDK does not send an event immediately after it occurred. The library stores event data in the buffer. The `SendEventsBuffer` method initiates sending data from the buffer and flushes it. Use the method to force sending stored events after passing important checkpoints of user scenarios.

{% list tabs group=instructions %}

- Swift

   ```swift translate=no
   AppMetrica.sendEventsBuffer()
   ```

- Objective-C

   ```obj-c translate=no
   [AMAAppMetrica sendEventsBuffer];
   ```

{% endlist %}

{% note alert "" %}

If you use this method frequently, this may result in increased internet traffic and energy consumption.

{% endnote %}

## Sending profile attributes {#send-attribute-profile}

{% list tabs group=instructions %}

- Swift

   To send profile attributes, pass the following parameters to the `reportUserProfile(_:onFailure:)` method of the `AppMetrica` class:

   * `userProfile`: The `UserProfile` instance that contains an array of attribute updates. Profile attributes are created by methods of the `ProfileAttribute` class.
   * `onFailure`: The block the error is passed to. If you do not want to track the error, pass `nil` for this block.

   ```swift translate=no
   let profile = MutableUserProfile()
   // Updating a single user profile attribute.
   let timeLeftAttribute = ProfileAttribute.customCounter("time_left")
   profile.apply(timeLeftAttribute.withDelta(-4.42))
   // Updating multiple attributes.
   profile.apply(from: [
       // Updating predefined attributes.
       ProfileAttribute.name().withValue("John"),
       ProfileAttribute.gender().withValue(GenderType.male),
       ProfileAttribute.birthDate().withAge(24),
       ProfileAttribute.notificationsEnabled().withValue(false),
       // Updating custom attributes.
       ProfileAttribute.customString("born_in").withValueIfUndefined("Moscow"),
       ProfileAttribute.customString("address").withValueReset(),
       ProfileAttribute.customNumber("age").withValue(24),
       ProfileAttribute.customCounter("logins_count").withDelta(1),
       ProfileAttribute.customBool("has_premium").withValue(true)
   ])
   // ProfieID is set using the method of the AppMetrica class.
   AppMetrica.userProfileID = "id"

   // Sending profile attributes.
   AppMetrica.reportUserProfile(profile, onFailure: { (error) in
       print("REPORT ERROR: %@", error.localizedDescription)
   })
   ```

- Objective-C

   To send profile attributes, pass the following parameters to the `+reportUserProfile:onFailure:` method of the `AMAAppMetrica` class:

   * `userProfile`: The `AMAUserProfile` instance that contains an array of attribute updates. To create profile attributes, use methods of the `AMAProfileAttribute` class.
   * `onFailure`: The block the error is passed to. If you do not want to track the error, pass `nil` for this block.

   ```obj-c translate=no
   AMAMutableUserProfile *profile = [[AMAMutableUserProfile alloc] init];
   // Updating a single user profile attribute.
   id<AMACustomCounterAttribute> timeLeftAttribute = [AMAProfileAttribute customCounter:@"time_left"];
   [profile apply:[timeLeftAttribute withDelta:-4.42]];
   // Updating multiple attributes.
   [profile applyFromArray:@[
       // Updating predefined attributes.
       [[AMAProfileAttribute name] withValue:@"John"],
       [[AMAProfileAttribute gender] withValue:AMAGenderTypeMale],
       [[AMAProfileAttribute birthDate] withAge:24],
       [[AMAProfileAttribute notificationsEnabled] withValue:NO],
       // Updating custom attributes.
       [[AMAProfileAttribute customString:@"born_in"] withValueIfUndefined:@"Moscow"],
       [[AMAProfileAttribute customString:@"address"] withValueReset],
       [[AMAProfileAttribute customNumber:@"age"] withValue:24],
       [[AMAProfileAttribute customCounter:@"logins_count"] withDelta:1],
       [[AMAProfileAttribute customBool:@"has_premium"] withValue:YES]
   ]];
   // ProfieID is set using the method of the AMAAppMetrica class.
   [AMAAppMetrica setUserProfileID:@"id"];

   // Sending profile attributes.
   [AMAAppMetrica reportUserProfile:[profile copy] onFailure:^(NSError *error) {
       NSLog(@"Error: %@", error);
   }];
   ```

{% endlist %}



## Sending E-commerce events {#send-ecommerce}

AppMetrica doesn't let you segment E-commerce events into test and non-test events. If you use the main API key for debugging purchases, the test events are included in general statistics. Therefore, to debug E-commerce event sending, use a reporter to send statistics to the additional API key.

### Step 1. Configure sending E-commerce events to the test API key {#send-ecommerce-test-key}

For different user actions, there are appropriate types of e-commerce events. To create a specific event type, use the appropriate `ECommerce` class method.

The examples below show how to send specific types of events:

{% cut "Opening a page" %}

{% list tabs group=instructions %}

- Swift

   ```swift translate=no
   // Creating a screen object.
   let screen = ECommerceScreen(
           name: "ProductCardScreen",
           categoryComponents: ["Promos", "Hot deal"],
           searchQuery: "danissimo maple syrup",
           payload: ["full_screen": "true"]
   )
   // Sending an e-commerce event.
   if let reporter = AppMetrica.reporter(for: "Testing API key") {
      reporter.reportECommerce(.showScreenEvent(screen: screen))
   }
   ```

- Objective-C

   ```obj-c translate=no
   // Creating a screen object.
   AMAECommerceScreen *screen = [[AMAECommerceScreen alloc] initWithName:@"ProductCardScreen"
                                                      categoryComponents:@[ @"Promos", @"Hot deal" ]
                                                             searchQuery:@"danissimo maple syrup"
                                                                 payload:@{ @"full_screen": @"true" }];
   // Sending an e-commerce event.
   id<AMAAppMetricaReporting> reporter = [AMAAppMetrica reporterForAPIKey:@"Testing API key"];
   [reporter reportECommerce:[AMAECommerce showScreenEventWithScreen:screen] onFailure:nil];
   ```

{% endlist %}

{% endcut %}

{% cut "Viewing a product card" %}

{% list tabs group=instructions %}

- Swift

   ```swift translate=no
   // Creating a screen object.
   let screen = ECommerceScreen(
           name: "ProductCardScreen",
           categoryComponents: ["Promos", "Hot deal"],
           searchQuery: "danissimo maple syrup",
           payload: ["full_screen": "true"]
   )
   // Creating an actualPrice object.
   let actualPrice = ECommercePrice(
           fiat: .init(unit: "USD", value: .init(string: "4.53")),
           internalComponents: [
               .init(unit: "wood", value: .init(string: "30570000")),
               .init(unit: "iron", value: .init(string: "26.89")),
               .init(unit: "gold", value: .init(string: "5.1")),
           ]
   )
   // Creating a product object.
   let product = ECommerceProduct(
           sku: "779213",
           name: "Danissimo curd product 5.9%, 130 g",
           categoryComponents: ["Groceries", "Dairy products", "Yogurts"],
           payload: ["full_screen": "true"],
           actualPrice: actualPrice,
           originalPrice: .init(
                   fiat: .init(unit: "USD", value: .init(string: "5.78")),
                   internalComponents: [
                       .init(unit: "wood", value: .init(string: "30590000")),
                       .init(unit: "iron", value: .init(string: "26.92")),
                       .init(unit: "gold", value: .init(string: "5.5")),
                   ]
           ),
           promoCodes: ["BT79IYX", "UT5412EP"]
   )
   // Sending an e-commerce event.
   if let reporter = AppMetrica.reporter(for: "Testing API key") {
      reporter.reportECommerce(.showProductCardEvent(product: product, screen: screen))
   }
   ```

- Objective-C

   ```obj-c translate=no
   // Creating a screen object.
   AMAECommerceScreen *screen = [[AMAECommerceScreen alloc] initWithName:@"ProductCardScreen"
                                                      categoryComponents:@[ @"Promos", @"Hot deal" ]
                                                             searchQuery:@"danissimo maple syrup"
                                                                 payload:@{ @"full_screen": @"true" }];
   // Creating an actualPrice object.
   AMAECommerceAmount *actualFiat =
           [[AMAECommerceAmount alloc] initWithUnit:@"USD" value:[NSDecimalNumber decimalNumberWithString:@"4.53"]];
   AMAECommerceAmount *woodActualPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"wood" value:[NSDecimalNumber decimalNumberWithString:@"30570000"]];
   AMAECommerceAmount *ironActualPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"iron" value:[NSDecimalNumber decimalNumberWithString:@"26.89"]];
   AMAECommerceAmount *goldActualPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"gold" value:[NSDecimalNumber decimalNumberWithString:@"5.1"]];
   AMAECommercePrice *actualPrice = [[AMAECommercePrice alloc] initWithFiat:actualFiat
                                                         internalComponents:@[ woodActualPrice, ironActualPrice, goldActualPrice ]];
   // Creating an originalPrice object.
   AMAECommerceAmount *originalFiat =
           [[AMAECommerceAmount alloc] initWithUnit:@"USD" value:[NSDecimalNumber decimalNumberWithString:@"5.78"]];
   AMAECommerceAmount *woodOriginalPrice =
            [[AMAECommerceAmount alloc] initWithUnit:@"wood" value:[NSDecimalNumber decimalNumberWithString:@"30590000"]];
   AMAECommerceAmount *ironOriginalPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"iron" value:[NSDecimalNumber decimalNumberWithString:@"26.92"]];
   AMAECommerceAmount *goldOriginalPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"gold" value:[NSDecimalNumber decimalNumberWithString:@"5.5"]];
   AMAECommercePrice *originalPrice = [[AMAECommercePrice alloc] initWithFiat:originalFiat
                                                           internalComponents:@[ woodOriginalPrice, ironOriginalPrice, goldOriginalPrice ]];
   // Creating a product object.
   AMAECommerceProduct *product = [[AMAECommerceProduct alloc] initWithSKU:@"779213"
                                                                      name:@"Danissimo curd product 5.9%, 130 g"
                                                        categoryComponents:@[ @"Groceries", @"Dairy products", @"Yogurts" ]
                                                                   payload:@{ @"full_screen" : @"true" }
                                                               actualPrice:actualPrice
                                                             originalPrice:originalPrice
                                                                promoCodes:@[ @"BT79IYX", @"UT5412EP" ]];
   // Sending an e-commerce event.
   id<AMAAppMetricaReporting> reporter = [AMAAppMetrica reporterForAPIKey:@"Testing API key"];
   [reporter reportECommerce:[AMAECommerce showProductCardEventWithProduct:product screen:screen] onFailure:nil];
   ```

{% endlist %}

{% endcut %}

{% cut "Viewing a product page" %}

{% list tabs group=instructions %}

- Swift

   ```swift translate=no
   // Creating a screen object.
   let screen = ECommerceScreen(
           name: "ProductCardScreen",
           categoryComponents: ["Promos", "Hot deal"],
           searchQuery: "danissimo maple syrup",
           payload: ["full_screen": "true"]
   )
   // Creating an actualPrice object.
   let actualPrice = ECommercePrice(
           fiat: .init(unit: "USD", value: .init(string: "4.53")),
           internalComponents: [
               .init(unit: "wood", value: .init(string: "30570000")),
               .init(unit: "iron", value: .init(string: "26.89")),
               .init(unit: "gold", value: .init(string: "5.1")),
           ]
   )
   // Creating a product object.
   let product = ECommerceProduct(
           sku: "779213",
           name: "Danissimo curd product 5.9%, 130 g",
           categoryComponents: ["Groceries", "Dairy products", "Yogurts"],
           payload: ["full_screen": "true"],
           actualPrice: actualPrice,
           originalPrice: .init(
                   fiat: .init(unit: "USD", value: .init(string: "5.78")),
                   internalComponents: [
                       .init(unit: "wood", value: .init(string: "30590000")),
                       .init(unit: "iron", value: .init(string: "26.92")),
                       .init(unit: "gold", value: .init(string: "5.5")),
                   ]
           ),
           promoCodes: ["BT79IYX", "UT5412EP"]
   )
   // Creating a referrer object.
   let referrer = ECommerceReferrer(type: "button", identifier: "76890", screen: screen)
   // Sending an e-commerce event.
   if let reporter = AppMetrica.reporter(for: "Testing API key") {
      reporter.reportECommerce(.showProductDetailsEvent(product: product, referrer: referrer))
   }
   ```

- Objective-C

   ```obj-c translate=no
   // Creating a screen object.
   AMAECommerceScreen *screen = [[AMAECommerceScreen alloc] initWithName:@"ProductCardScreen"
                                                      categoryComponents:@[ @"Promos", @"Hot deal" ]
                                                             searchQuery:@"danissimo maple syrup"
                                                                 payload:@{ @"full_screen": @"true" }];

   // Creating an actualPrice object.
   AMAECommerceAmount *actualFiat =
           [[AMAECommerceAmount alloc] initWithUnit:@"USD" value:[NSDecimalNumber decimalNumberWithString:@"4.53"]];
   AMAECommerceAmount *woodActualPrice =
            [[AMAECommerceAmount alloc] initWithUnit:@"wood" value:[NSDecimalNumber decimalNumberWithString:@"30570000"]];
   AMAECommerceAmount *ironActualPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"iron" value:[NSDecimalNumber decimalNumberWithString:@"26.89"]];
   AMAECommerceAmount *goldActualPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"gold" value:[NSDecimalNumber decimalNumberWithString:@"5.1"]];
   AMAECommercePrice *actualPrice = [[AMAECommercePrice alloc] initWithFiat:actualFiat
                                                         internalComponents:@[ woodActualPrice, ironActualPrice, goldActualPrice ]];
   // Creating an originalPrice object.
   AMAECommerceAmount *originalFiat =
           [[AMAECommerceAmount alloc] initWithUnit:@"USD" value:[NSDecimalNumber decimalNumberWithString:@"5.78"]];
   AMAECommerceAmount *woodOriginalPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"wood" value:[NSDecimalNumber decimalNumberWithString:@"30590000"]];
   AMAECommerceAmount *ironOriginalPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"iron" value:[NSDecimalNumber decimalNumberWithString:@"26.92"]];
   AMAECommerceAmount *goldOriginalPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"gold" value:[NSDecimalNumber decimalNumberWithString:@"5.5"]];
   AMAECommercePrice *originalPrice = [[AMAECommercePrice alloc] initWithFiat:originalFiat
                                                           internalComponents:@[ woodOriginalPrice, ironOriginalPrice, goldOriginalPrice ]];
   // Creating a product object.
   AMAECommerceProduct *product = [[AMAECommerceProduct alloc] initWithSKU:@"779213"
                                                                      name:@"Danissimo curd product 5.9%, 130 g"
                                                         categoryComponents:@[ @"Groceries", @"Dairy products", @"Yogurts" ]
                                                                  payload:@{ @"full_screen" : @"true" }
                                                               actualPrice:actualPrice
                                                             originalPrice:originalPrice
                                                                promoCodes:@[ @"BT79IYX", @"UT5412EP" ]];
   // Creating a referrer object.
   AMAECommerceReferrer *referrer = [[AMAECommerceReferrer alloc] initWithType:@"button"
                                                                    identifier:@"76890"
                                                                        screen:screen];
   // Sending an e-commerce event.
   id<AMAAppMetricaReporting> reporter = [AMAAppMetrica reporterForAPIKey:@"Testing API key"];
   [reporter reportECommerce:[AMAECommerce showProductDetailsEventWithProduct:product referrer:referrer] onFailure:nil];
   ```

{% endlist %}

{% endcut %}

{% cut "Adding or removing an item to/from the cart" %}

{% list tabs group=instructions %}

- Swift

   ```swift translate=no
   // Creating a screen object.
   let screen = ECommerceScreen(
           name: "ProductCardScreen",
           categoryComponents: ["Promos", "Hot deal"],
           searchQuery: "danissimo maple syrup",
           payload: ["full_screen": "true"]
   )
   // Creating an actualPrice object.
   let actualPrice = ECommercePrice(
           fiat: .init(unit: "USD", value: .init(string: "4.53")),
           internalComponents: [
               .init(unit: "wood", value: .init(string: "30570000")),
               .init(unit: "iron", value: .init(string: "26.89")),
               .init(unit: "gold", value: .init(string: "5.1")),
           ]
   )
   // Creating a product object.
   let product = ECommerceProduct(
           sku: "779213",
           name: "Danissimo curd product 5.9%, 130 g",
           categoryComponents: ["Groceries", "Dairy products", "Yogurts"],
           payload: ["full_screen": "true"],
           actualPrice: actualPrice,
           originalPrice: .init(
                   fiat: .init(unit: "USD", value: .init(string: "5.78")),
                   internalComponents: [
                       .init(unit: "wood", value: .init(string: "30590000")),
                       .init(unit: "iron", value: .init(string: "26.92")),
                       .init(unit: "gold", value: .init(string: "5.5")),
                   ]
           ),
           promoCodes: ["BT79IYX", "UT5412EP"]
   )
   // Creating a referrer object.
   let referrer = ECommerceReferrer(type: "button", identifier: "76890", screen: screen)
   // Creating a cartItem object.
   let addedItems = ECommerceCartItem(
           product: product,
           quantity: .init(string: "1"),
           revenue: actualPrice,
           referrer: referrer
   )
   // Sending an e-commerce event.
   if let reporter = AppMetrica.reporter(for: "Testing API key") {
      reporter.reportECommerce(.addCartItemEvent(cartItem: addedItems))
      // Or:
      reporter.reportECommerce(.removeCartItemEvent(cartItem: addedItems))
   }
   ```

- Objective-C

   ```obj-c translate=no
   // Creating a screen object.
   AMAECommerceScreen *screen = [[AMAECommerceScreen alloc] initWithName:@"ProductCardScreen"
                                                      categoryComponents:@[ @"Promos", @"Hot deal" ]
                                                             searchQuery:@"danissimo maple syrup"
                                                                 payload:@{ @"full_screen": @"true" }];
   // Creating an actualPrice object.
   AMAECommerceAmount *actualFiat =
           [[AMAECommerceAmount alloc] initWithUnit:@"USD" value:[NSDecimalNumber decimalNumberWithString:@"4.53"]];
   AMAECommerceAmount *woodActualPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"wood" value:[NSDecimalNumber decimalNumberWithString:@"30570000"]];
   AMAECommerceAmount *ironActualPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"iron" value:[NSDecimalNumber decimalNumberWithString:@"26.89"]];
   AMAECommerceAmount *goldActualPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"gold" value:[NSDecimalNumber decimalNumberWithString:@"5.1"]];
   AMAECommercePrice *actualPrice = [[AMAECommercePrice alloc] initWithFiat:actualFiat
                                                         internalComponents:@[ woodActualPrice, ironActualPrice, goldActualPrice ]];
   // Creating an originalPrice object.
   AMAECommerceAmount *originalFiat =
           [[AMAECommerceAmount alloc] initWithUnit:@"USD" value:[NSDecimalNumber decimalNumberWithString:@"5.78"]];
   AMAECommerceAmount *woodOriginalPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"wood" value:[NSDecimalNumber decimalNumberWithString:@"30590000"]];
   AMAECommerceAmount *ironOriginalPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"iron" value:[NSDecimalNumber decimalNumberWithString:@"26.92"]];
   AMAECommerceAmount *goldOriginalPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"gold" value:[NSDecimalNumber decimalNumberWithString:@"5.5"]];
   AMAECommercePrice *originalPrice = [[AMAECommercePrice alloc] initWithFiat:originalFiat
                                                           internalComponents:@[ woodOriginalPrice, ironOriginalPrice, goldOriginalPrice ]];
   // Creating a product object.
   AMAECommerceProduct *product = [[AMAECommerceProduct alloc] initWithSKU:@"779213"
                                                                      name:@"Danissimo curd product 5.9%, 130 g"
                                                        categoryComponents:@[ @"Groceries", @"Dairy products", @"Yogurts" ]
                                                                   payload:@{ @"full_screen" : @"true" }
                                                               actualPrice:actualPrice
                                                             originalPrice:originalPrice
                                                                promoCodes:@[ @"BT79IYX", @"UT5412EP" ]];
   // Creating a referrer object.
   AMAECommerceReferrer *referrer = [[AMAECommerceReferrer alloc] initWithType:@"button"
                                                                    identifier:@"76890"
                                                                        screen:screen];
   // Creating a cartItem object.
   NSDecimalNumber *quantity = [NSDecimalNumber decimalNumberWithString:@"1"];
   AMAECommerceCartItem *addedItems = [[AMAECommerceCartItem alloc] initWithProduct:product
                                                                           quantity:quantity
                                                                            revenue:actualPrice
                                                                           referrer:referrer];
   // Sending an e-commerce event.
   id<AMAAppMetricaReporting> reporter = [AMAAppMetrica reporterForAPIKey:@"Testing API key"];
   [reporter reportECommerce:[AMAECommerce addCartItemEventWithItem:addedItems] onFailure:nil];
   // Or:
   [reporter reportECommerce:[AMAECommerce removeCartItemEventWithItem:addedItems] onFailure:nil];
   ```

{% endlist %}

{% endcut %}

{% cut "Starting and completing a purchase" %}

{% list tabs group=instructions %}

- Swift

   ```swift translate=no
   // Creating a screen object.
   let screen = ECommerceScreen(
           name: "ProductCardScreen",
           categoryComponents: ["Promos", "Hot deal"],
           searchQuery: "danissimo maple syrup",
           payload: ["full_screen": "true"]
   )
   // Creating an actualPrice object.
   let actualPrice = ECommercePrice(
           fiat: .init(unit: "USD", value: .init(string: "4.53")),
           internalComponents: [
               .init(unit: "wood", value: .init(string: "30570000")),
               .init(unit: "iron", value: .init(string: "26.89")),
               .init(unit: "gold", value: .init(string: "5.1")),
           ]
   )
   // Creating a product object.
   let product = ECommerceProduct(
           sku: "779213",
           name: "Danissimo curd product 5.9%, 130 g",
           categoryComponents: ["Groceries", "Dairy products", "Yogurts"],
           payload: ["full_screen": "true"],
           actualPrice: actualPrice,
           originalPrice: .init(
                   fiat: .init(unit: "USD", value: .init(string: "5.78")),
                   internalComponents: [
                       .init(unit: "wood", value: .init(string: "30590000")),
                       .init(unit: "iron", value: .init(string: "26.92")),
                       .init(unit: "gold", value: .init(string: "5.5")),
                   ]
           ),
           promoCodes: ["BT79IYX", "UT5412EP"]
   )
   // Creating a referrer object.
   let referrer = ECommerceReferrer(type: "button", identifier: "76890", screen: screen)
   // Creating a cartItem object.
   let addedItems = ECommerceCartItem(
           product: product,
           quantity: .init(string: "1"),
           revenue: actualPrice,
           referrer: referrer
   )
   // Creating an order object.
   let order = ECommerceOrder(
           identifier: "88528768",
           cartItems: [addedItems],
           payload: ["black_friday": "true"]
   )
   // Sending an e-commerce event.
   if let reporter = AppMetrica.reporter(for: "Testing API key") {
      reporter.reportECommerce(.beginCheckoutEvent(order:order))
      reporter.reportECommerce(.purchaseEvent(order: order))
   }
   ```

- Objective-C

   ```obj-c translate=no
   // Creating a screen object.
   AMAECommerceScreen *screen = [[AMAECommerceScreen alloc] initWithName:@"ProductCardScreen"
                                                      categoryComponents:@[ @"Promos", @"Hot deal" ]
                                                             searchQuery:@"danissimo maple syrup"
                                                                 payload:@{ @"full_screen": @"true" }];
   // Creating an actualPrice object.
   AMAECommerceAmount *actualFiat =
           [[AMAECommerceAmount alloc] initWithUnit:@"USD" value:[NSDecimalNumber decimalNumberWithString:@"4.53"]];
   AMAECommerceAmount *woodActualPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"wood" value:[NSDecimalNumber decimalNumberWithString:@"30570000"]];
   AMAECommerceAmount *ironActualPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"iron" value:[NSDecimalNumber decimalNumberWithString:@"26.89"]];
   AMAECommerceAmount *goldActualPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"gold" value:[NSDecimalNumber decimalNumberWithString:@"5.1"]];
   AMAECommercePrice *actualPrice = [[AMAECommercePrice alloc] initWithFiat:actualFiat
                                                         internalComponents:@[ woodActualPrice, ironActualPrice, goldActualPrice ]];
   // Creating an originalPrice object.
   AMAECommerceAmount *originalFiat =
           [[AMAECommerceAmount alloc] initWithUnit:@"USD" value:[NSDecimalNumber decimalNumberWithString:@"5.78"]];
   AMAECommerceAmount *woodOriginalPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"wood" value:[NSDecimalNumber decimalNumberWithString:@"30590000"]];
   AMAECommerceAmount *ironOriginalPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"iron" value:[NSDecimalNumber decimalNumberWithString:@"26.92"]];
   AMAECommerceAmount *goldOriginalPrice =
           [[AMAECommerceAmount alloc] initWithUnit:@"gold" value:[NSDecimalNumber decimalNumberWithString:@"5.5"]];
   AMAECommercePrice *originalPrice = [[AMAECommercePrice alloc] initWithFiat:originalFiat
                                                           internalComponents:@[ woodOriginalPrice, ironOriginalPrice, goldOriginalPrice ]];
   // Creating a product object.
   AMAECommerceProduct *product = [[AMAECommerceProduct alloc] initWithSKU:@"779213"
                                                                      name:@"Danissimo curd product 5.9%, 130 g"
                                                        categoryComponents:@[ @"Groceries", @"Dairy products", @"Yogurts" ]
                                                                   payload:@{ @"full_screen" : @"true" }
                                                               actualPrice:actualPrice
                                                             originalPrice:originalPrice
                                                                promoCodes:@[ @"BT79IYX", @"UT5412EP" ]];
   // Creating a referrer object.
   AMAECommerceReferrer *referrer = [[AMAECommerceReferrer alloc] initWithType:@"button"
                                                                    identifier:@"76890"
                                                                        screen:screen];
   // Creating a cartItem object.
   NSDecimalNumber *quantity = [NSDecimalNumber decimalNumberWithString:@"1"];
   AMAECommerceCartItem *addedItems = [[AMAECommerceCartItem alloc] initWithProduct:product
                                                                           quantity:quantity
                                                                            revenue:actualPrice
                                                                           referrer:referrer];
   // Creating an order object.
   AMAECommerceOrder *order = [[AMAECommerceOrder alloc] initWithIdentifier:@"88528768"
                                                                  cartItems:@[ addedItems ]
                                                                    payload:@{ @"black_friday" : @"true"}];
   // Sending an e-commerce event.
   id<AMAAppMetricaReporting> reporter = [AMAAppMetrica reporterForAPIKey:@"Testing API key"];
   [reporter reportECommerce:[AMAECommerce beginCheckoutEventWithOrder:order] onFailure:nil];
   [reporter reportECommerce:[AMAECommerce purchaseEventWithOrder:order] onFailure:nil];
   ```

{% endlist %}

{% endcut %}

### Step 2. Check the test application's report {#send-ecommerce-test-app}

Make in-app test purchases. After a while, check the E-commerce report in the AppMetrica interface. Make sure that the report shows E-commerce events.

For more information about the report, see [E-commerce](../../../mobile-reports/ecommerce-report.md).

### Step 3. Configure sending events to the main API key {#send-ecommerce-key}

After successful testing, configure sending E-commerce events to the main API key.

{% list tabs group=instructions %}

- Swift

   To send the `ECommerce` object to the main API key, use the `reportECommerce(_:onFailure:)` method of the `AppMetrica` class.

   ```swift translate=no
   // ...
   // Sending an e-commerce event.
   AppMetrica.reportECommerce(.showScreenEvent(screen: screen))
   ```

- Objective-C

   To send the `AMAECommerce` instance to the main API key, use the `+reportECommerce:onFailure:` method of the `AMAAppMetrica` class.

   ```obj-c translate=no
   // ...
   // Sending an e-commerce event.
   [AMAAppMetrica reportECommerce:[AMAECommerce showScreenEventWithScreen:screen] onFailure:nil];
   ```

{% endlist %}

## Sending Revenue {#send-revenue}

AppMetrica supports validation of purchases implemented using the [StoreKit](https://developer.apple.com/documentation/storekit) library. Validation lets you filter purchases made from hacked apps. If validation is enabled and a purchase fails it, this purchase isn't shown in reports.

{% note info %}

To validate purchases, enable the validation in the settings.

{% endnote %}

### Step 1. Test sending Revenue {#send-revenue-test}

AppMetrica doesn't let you segment between test and non-test revenue. If you use the main API key for debugging purchases, the test purchases are included in general statistics. Therefore, to debug Revenue sending, use a reporter to send statistics to the additional API key.

This section outlines the steps for sending Revenue to the additional API key:

{% cut "With validation" %}

To validate purchases on iOS, configure sending the `transactionID` field and `receiptData` where you implement the transaction completion:

{% list tabs group=instructions %}

- Swift

   1. Initialize the `MutableRevenueInfo` instance.
   2. To validate a purchase, specify `transactionID` and `receiptData`. You should receive them before invoking `SKPaymentQueue.default ().finishTransaction(transaction)`.
   3. Send the `MutableRevenueInfo` instance to the test API key using the `AppMetricaReporting` reporter. For more information about reporters, see [Sending statistics to an additional API key](#reporter).

   ```swift translate=no
    func completeTransaction(_ transaction: SKPaymentTransaction) {
        // ...
        let price = NSDecimalNumber(string: "2100.5")
        // Initializing the Revenue instance.
        let revenueInfo = MutableRevenueInfo(priceDecimal: price, currency: "BYN")
        revenueInfo.productID = "TV soundbar"
        revenueInfo.quantity = 2
        revenueInfo.payload = ["source": "AppStore"]
        // Set purchase information for validation.
        if let url = Bundle.main.appStoreReceiptURL, let data = try? Data(contentsOf: url), let transactionID = transaction.transactionIdentifier {
            revenueInfo.transactionID = transactionID
            revenueInfo.receiptData = data
        }
        // Sending the Revenue instance using reporter.
        guard let reporter = AppMetrica.reporter(for: "Testing API key") else {
           print("Failed to create AppMetrica reporter")
           return
        }
        reporter.reportRevenue(revenueInfo, onFailure: { (error) in
            print("Revenue error: \(error.localizedDescription)")
        })
        // Remove the transaction from the payment queue.
        SKPaymentQueue.default().finishTransaction(transaction)
   }
   ```

- Objective-C

   1. Initialize the `AMAMutableRevenueInfo` instance.
   2. To validate a purchase, specify `transactionID` and `receiptData`. The must be received before `[[SKPaymentQueue defaultQueue] finishTransaction:transaction]` is invoked.
   3. Send the `AMAMutableRevenueInfo` instance to the test API key using the `AMAAppMetricaReporting` reporter. For more information about reporters, see [Sending statistics to an additional API key](#reporter).

   ```obj-c translate=no
    - (void)completeTransaction:(SKPaymentTransaction *)transaction
    {
        // ...
        NSDecimalNumber *price = [NSDecimalNumber decimalNumberWithString:@"2100.5"];
        // Initializing the Revenue instance.
        AMAMutableRevenueInfo *revenueInfo = [[AMAMutableRevenueInfo alloc] initWithPriceDecimal:price currency:@"BYN"];
        revenueInfo.productID = @"TV soundbar";
        revenueInfo.quantity = 2;
        revenueInfo.payload = @{ @"source": @"AppStore" };
        // Set purchase information for validation.
        revenueInfo.transactionID = transaction.transactionIdentifier;
        revenueInfo.receiptData = [NSData dataWithContentsOfURL:[[NSBundle mainBundle] appStoreReceiptURL]];
        // Sending the Revenue instance using reporter.
        id<AMAAppMetricaReporting> reporter = [AMAAppMetrica reporterForAPIKey:@"Testing API key"];
        [reporter reportRevenue:[revenueInfo copy] onFailure:^(NSError *error) {
            NSLog(@"Revenue error: %@", error);
        }];
        // Remove the transaction from the payment queue.
        [[SKPaymentQueue defaultQueue] finishTransaction:transaction];
    }
   ```

{% endlist %}

{% endcut %}

{% cut "Without validation" %}

To send information about a purchase without validation:

{% list tabs group=instructions %}

- Swift

   1. Initialize the `MutableRevenueInfo` instance.
   2. (Optional) To group purchases by `OrderID`, specify it in the `payload` property.

      {% note info %}

      If the `OrderID` is not specified, AppMetrica generates the ID automatically.

      {% endnote %}

   3. Send the `MutableRevenueInfo` instance to the test API key using the `AppMetricaReporting` reporter. For more information about reporters, see [Sending statistics to an additional API key](#reporter).

   ```swift translate=no
    let price = NSDecimalNumber(string: "2100.5")
    // Initializing the Revenue instance.
    let revenueInfo = MutableRevenueInfo(priceDecimal: price, currency: "BYN")
    revenueInfo.productID = "TV soundbar"
    revenueInfo.quantity = 2
    // To group purchases, set the OrderID parameter in the payload property.
    revenueInfo.payload = ["OrderID": "Identifier", "source": "AppStore"]
    // Sending the Revenue instance using reporter.
    if let reporter = AppMetrica.reporter(for: "Testing API key") {
       reporter.reportRevenue(revenueInfo, onFailure: { (error) in
           print("Revenue error: \(error.localizedDescription)")
       })
    }
   ```

- Objective-C

   1. Initialize the `AMAMutableRevenueInfo` instance.
   2. (Optional) To group purchases by `OrderID`, specify it in the `payload` property.

      {% note info %}

      If the `OrderID` is not specified, AppMetrica generates the ID automatically.

      {% endnote %}

   3. Send the `AMAMutableRevenueInfo` instance to the test API key using the `AMAAppMetricaReporting` reporter. For more information about reporters, see [Sending statistics to an additional API key](#reporter).

   ```obj-c translate=no
    NSDecimalNumber *price = [NSDecimalNumber decimalNumberWithString:@"2100.5"];
    // Initializing the Revenue instance.
    AMAMutableRevenueInfo *revenueInfo = [[AMAMutableRevenueInfo alloc] initWithPriceDecimal:price currency:@"BYN"];
    revenueInfo.productID = @"TV soundbar";
    revenueInfo.quantity = 2;
    // Setting the OrderID parameter in the payload property to group purchases
    revenueInfo.payload = @{ @"OrderID": @"Identifier", @"source": @"AppStore" };
    // Sending the Revenue instance using reporter.
    id<AMAAppMetricaReporting> reporter = [AMAAppMetrica reporterForAPIKey:@"Testing API key"];
    [reporter reportRevenue:[revenueInfo copy] onFailure:^(NSError *error) {
        NSLog(@"Revenue error: %@", error);
    }];
   ```

{% endlist %}

{% endcut %}

### Step 2. Configure sending Revenue to the main API key {#send-revenue-key}

After successful testing, configure sending Revenue to the main API key.

{% list tabs group=instructions %}

- Swift

   To send the `MutableRevenueInfo` instance to the main API key, use the `reportRevenue(_:onFailure:)` method of the `AppMetrica` class.

   ```swift translate=no
   // ...
   // Sending the Revenue instance.
   AppMetrica.reportRevenue(revenueInfo, onFailure: { (error) in
       print("Revenue error: \(error)")
   })
   ```

- Objective-C

   To send the `AMAMutableRevenueInfo` instance to the main API key, use the `+reportRevenue:onFailure:` method of the `AMAAppMetrica` class.

   ```obj-c translate=no
   // ...
   // Sending the Revenue instance.
   [AMAAppMetrica reportRevenue:[revenueInfo copy] onFailure:^(NSError *error) {
      NSLog(@"Revenue error: %@", error);
   }];
   ```

{% endlist %}

## Sending Ad Revenue {#send-adrevenue}

### Step 1. Make sure that the SDK is activated {#send-adrevenue-activate}

Activation example:

{% list tabs group=instructions %}

- Swift

   ```swift translate=no
   let configuration = AppMetricaConfiguration.init(apiKey: "API key")
   AppMetrica.activate(with: configuration!)
   ```

- Objective-C

   ```objectivec translate=no
   AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithApiKey:@"API_key"];
   [AMAAppMetrica activateWithConfiguration:configuration];
   ```

{% endlist %}

### Step 2. Set up sending ad revenue data {#send-adrevenue-send}

{% list tabs %}

- AppLovin MAX

   1. Import the required modules:

      {% list tabs group=instructions %}

      - Swift

         ```swift translate=no
         import AppMetricaCore
         import AppLovinSDK
         ```

      - Objective-C

         ```objectivec translate=no
         #import <AppMetricaCore/AppMetricaCore.h>
         #import <AppLovinSDK/AppLovinSDK.h>
         ```

      {% endlist %}

   2. Add a helper extension for `MAAdFormat`:

      {% list tabs group=instructions %}

      - Swift

         ```swift translate=no
         extension MAAdFormat {
             var appMetricaAdType: AdType {
                 switch self {
                 case .banner: return .banner
                 case .interstitial: return .interstitial
                 case .rewarded: return .rewarded
                 case .native: return .native
                 case .mrec: return .mrec
                 case .appOpen: return .appOpen
                 default: return .other
                 }
             }
         }
         ```

      - Objective-C

         ```objectivec translate=no
         @implementation MAAdFormat (AppMetricaAdType)

         - (AMAAdType)appMetricaAdType {
             switch (self) {
                 case MAAdFormat.banner:
                     return AMAAdTypeBanner;
                 case MAAdFormat.interstitial:
                     return AMAAdTypeInterstitial;
                 case MAAdFormat.rewarded:
                     return AMAAdTypeRewarded;
                 case MAAdFormat.native:
                     return AMAAdTypeNative;
                 case MAAdFormat.mrec:
                     return AMAAdTypeMrec;
                 case MAAdFormat.appOpen:
                     return AMAAdTypeAppOpen;
                 default:
                     return AdTypeOther;
            }
         }

         @end
         ```

      {% endlist %}

   3. Implement `MAAdRevenueDelegate`:

      {% list tabs group=instructions %}

      - Swift

         ```swift translate=no
         class AdRevenueReporter: NSObject, MAAdRevenueDelegate {
             func didPayRevenue(for ad: MAAd) {
                 // Create a MutableAdRevenueInfo object
                 let adRevenueInfo = MutableAdRevenueInfo(adRevenue: NSDecimalNumber(value: ad.revenue), currency: "USD")

                 // Set additional properties
                 adRevenueInfo.adType = ad.format.appMetricaAdType
                 adRevenueInfo.adNetwork = ad.networkName
                 adRevenueInfo.adUnitID = ad.adUnitIdentifier
                 adRevenueInfo.adPlacementName = ad.placement
                 adRevenueInfo.precision = ad.revenuePrecision

                 // Additional information can be added to payload if needed
                 adRevenueInfo.payload = [
                     "adType": ad.format.label,
                     "countryCode": ALSdk.shared().configuration.countryCode,
                     "networkPlacement": ad.networkPlacement,
                     "original_ad_type": ad.format.label,
                 ]

                 // Report the ad revenue to AppMetrica
                 AppMetrica.reportAdRevenue(adRevenueInfo)
             }
         }

         ```

      - Objective-C

         ```objectivec translate=no
         #import <AppMetricaCore/AppMetricaCore.h>
         #import <AppLovinSDK/AppLovinSDK.h>
         ```

      {% endlist %}

- Digital Turbine (Fyber)

   1. Import the required modules:

      {% list tabs group=instructions %}

      - Swift

         ```swift translate=no
         import AppMetricaCore
         import FairBidSDK
         ```

      - Objective-C

         ```objectivec translate=no
         #import <AppMetricaCore/AppMetricaCore.h>
         #import <FairBidSDK/FairBidSDK.h>
         ```

      {% endlist %}

   2. Create a function for passing ad revenue data to AppMetrica:

      {% list tabs group=instructions %}

      - Swift

         ```swift translate=no
         func reportToAppMetrica(_ impressionData: FYBImpressionData, placementId: String, adType: AdType) {
             let revenue = impressionData.netPayout.map { NSDecimalNumber(decimal: $0.decimalValue) } ?? .zero
             let currency = impressionData.currency ?? "USD"

             let adRevenueInfo = MutableAdRevenueInfo(adRevenue: revenue, currency: currency)
             adRevenueInfo.adType = adType
             adRevenueInfo.adNetwork = impressionData.demandSource
             adRevenueInfo.adUnitID = impressionData.creativeId
             adRevenueInfo.precision = impressionData.priceAccuracy.appMetricaPrecision
             adRevenueInfo.payload = [
               "original_ad_type": String(impressionData.placementType.rawValue),
             ]

             AppMetrica.reportAdRevenue(adRevenueInfo) { error in
                 print("Failed to report ad revenue to AppMetrica: \(error)")
             }
         }
         ```

      - Objective-C

         ```objectivec translate=no
         void reportToAppMetrica(FYBImpressionData *impressionData, NSString *placementId, AdType adType) {
             NSDecimalNumber *revenue = impressionData.netPayout ? [[NSDecimalNumber alloc] initWithDecimal:impressionData.netPayout.decimalValue] : [NSDecimalNumber zero];
             NSString *currency = impressionData.currency ? impressionData.currency : @"USD";

             MutableAdRevenueInfo *adRevenueInfo = [[MutableAdRevenueInfo alloc] initWithAdRevenue:revenue currency:currency];
             adRevenueInfo.adType = adType;
             adRevenueInfo.adNetwork = impressionData.demandSource;
             adRevenueInfo.adUnitID = impressionData.creativeId;
             adRevenueInfo.precision = [impressionData.priceAccuracy appMetricaPrecision];
             adRevenueInfo.payload = @{
                 @"original_ad_type": @(impressionData.placementType)
             };

             [AppMetrica reportAdRevenue:adRevenueInfo completion:^(NSError *error) {
                 if (error) {
                     NSLog(@"Failed to report ad revenue to AppMetrica: %@", error);
                 }
             }];
         }
         ```

      {% endlist %}

   3. Add an extension for converting Fyber prices to the AppMetrica format:

      {% list tabs group=instructions %}

      - Swift

         ```swift translate=no
         extension FYBImpressionDataPriceAccuracy {
             var appMetricaPrecision: String {
                 switch self {
                 case .undisclosed: return "undisclosed"
                 case .predicted: return "predicted"
                 case .programmatic: return "programmatic"
                 @unknown default: return "unknown"
                 }
             }
         }
         ```

      - Objective-C

         ```objectivec translate=no
         @implementation NSNumber (FYBImpressionDataPriceAccuracyAppMetricaPrecision)

         + (NSString *)appMetricaPrecisionForFYBImpressionDataPriceAccuracy:(FYBImpressionDataPriceAccuracy)accuracy {
             switch (accuracy) {
                 case FYBImpressionDataPriceAccuracyUndisclosed:
                     return @"undisclosed";
                 case FYBImpressionDataPriceAccuracyPredicted:
                     return @"predicted";
                 case FYBImpressionDataPriceAccuracyProgrammatic:
                     return @"programmatic";
                 default:
                     return @"unknown";
             }
         }

         @end
         ```

      {% endlist %}

   4. Create a function for sending Offerwall impression reports to AppMetrica:

      {% list tabs group=instructions %}

      - Swift

         ```swift translate=no
         func reportOfferWallShowToAppMetrica(placementId: String) {
             let adRevenueInfo = MutableAdRevenueInfo(adRevenue: NSDecimalNumber.zero, currency: "USD")
             adRevenueInfo.adType = .other
             adRevenueInfo.adUnitID = placementId
             adRevenueInfo.payload = [
                 "original_ad_type": "offerWall"
             ]

             AppMetrica.reportAdRevenue(adRevenueInfo) { error in
                 print("Failed to report OfferWall show to AppMetrica: \(error)")
             }
         }
         ```

      - Objective-C

         ```objectivec translate=no
         - (void)reportOfferWallShowToAppMetricaWithPlacementId:(NSString *)placementId {
             AMAMutableAdRevenueInfo *adRevenueInfo = [[AMAMutableAdRevenueInfo alloc] initWithAdRevenue:[NSDecimalNumber zero] currency:@"USD"];

             adRevenueInfo.adType = AMAAdTypeOther;
             adRevenueInfo.adUnitID = placementId;
             adRevenueInfo.payload = @{
                 @"original_ad_type": @"offerWall"
             };

             [AMAYandexMetrica reportAdRevenueWithInfo:adRevenueInfo completionHandler:^(NSError * _Nullable error) {
                 if (error) {
                     NSLog(@"Failed to report OfferWall show to AppMetrica: %@", error);
                 }
             }];
         }
         ```

      {% endlist %}

   5. Create delegates and their corresponding methods for each ad format:

      {% list tabs group=instructions %}

      - Swift

         ```swift translate=no
         class YourBannerDelegate: NSObject, FYBBannerDelegate {
             func bannerDidShow(_ banner: FYBBannerAdView, impressionData: FYBImpressionData) {
                 reportToAppMetrica(impressionData, placementId: banner.options.placementId, adType: .banner)
             }
             // Implement other delegate methods as needed
         }

         class YourInterstitialDelegate: NSObject, FYBInterstitialDelegate {
             func interstitialDidShow(_ placementId: String, impressionData: FYBImpressionData) {
                 reportToAppMetrica(impressionData, placementId: placementId, adType: .interstitial)
             }
             // Implement other delegate methods as needed
         }

         class YourRewardedDelegate: NSObject, FYBRewardedDelegate {
             func rewardedDidShow(_ placementId: String, impressionData: FYBImpressionData) {
                 reportToAppMetrica(impressionData, placementId: placementId, adType: .rewarded)
             }
             // Implement other delegate methods as needed
         }

         class YourOfferWallDelegate: NSObject, OfferWallDelegate {
             func didShow(_ placementId: String?) {
                 reportOfferWallShowToAppMetrica(placementId: placementId ?? "unknown")
             }
             // Implement other delegate methods as needed
         }
         ```

      - Objective-C

         ```objectivec translate=no
         // YourBannerDelegate
         @interface YourBannerDelegate : NSObject <FYBBannerDelegate>
         @end

         @implementation YourBannerDelegate
         - (void)bannerDidShow:(FYBBannerAdView *)banner impressionData:(FYBImpressionData *)impressionData {
             [self reportToAppMetricaWithImpressionData:impressionData placementId:banner.options.placementId adType:AdTypeBanner];
         }
         // Implement other delegate methods as needed
         @end

         // YourInterstitialDelegate
         @interface YourInterstitialDelegate : NSObject <FYBInterstitialDelegate>
         @end

         @implementation YourInterstitialDelegate
         - (void)interstitialDidShowWithPlacementId:(NSString *)placementId impressionData:(FYBImpressionData *)impressionData {
             [self reportToAppMetricaWithImpressionData:impressionData placementId:placementId adType:AdTypeInterstitial];
         }
         // Implement other delegate methods as needed
         @end

         // YourRewardedDelegate
         @interface YourRewardedDelegate : NSObject <FYBRewardedDelegate>
         @end

         @implementation YourRewardedDelegate
         - (void)rewardedDidShowWithPlacementId:(NSString *)placementId impressionData:(FYBImpressionData *)impressionData {
             [self reportToAppMetricaWithImpressionData:impressionData placementId:placementId adType:AdTypeRewarded];
         }
         // Implement other delegate methods as needed
         @end

         // YourOfferWallDelegate
         @interface YourOfferWallDelegate : NSObject <OfferWallDelegate>
         @end

         @implementation YourOfferWallDelegate
         - (void)didShowWithPlacementId:(NSString *)placementId {
             // Assuming reportOfferWallShowToAppMetrica is implemented elsewhere
             [self reportOfferWallShowToAppMetricaWithPlacementId:placementId ? placementId : @"unknown"];
         }
         // Implement other delegate methods as needed
         @end
         ```

      {% endlist %}

- Google AdMob

   1. Import the required modules:

      {% list tabs group=instructions %}

      - Swift

         ```swift translate=no
         import AppMetricaCore
         import GoogleMobileAds
         ```

      - Objective-C

         ```objectivec translate=no
         #import <AppMetricaCore/AppMetricaCore.h>
         #import <GoogleMobileAds/GoogleMobileAds.h>
         ```

      {% endlist %}

   2. Add a helper extension for `GADAdValuePrecision`:

      {% list tabs group=instructions %}

      - Swift

         ```swift translate=no
         extension GADAdValuePrecision: CustomStringConvertible {
             public var description: String {
                 switch self {
                 case .precise: return "precise"
                 case .estimated: return "estimated"
                 case .publisherProvided: return "publisher_defined"
                 case .unknown: fallthrough
                 @unknown default: return "unknown"
                 }
             }
         }

         enum GAAdType: String {
             case banner = "bannerAd"
             case interstitial = "interstitialAd"
             case rewarded = "rewardedAd"
             case native = "nativeAd"
             case appOpen = "appOpenAd"
         }

         ```

      - Objective-C

         ```objectivec translate=no
         @interface GADAdValuePrecisionHelper : NSObject

         + (NSString *)stringFromAdValuePrecision:(GADAdValuePrecision)precision;

         @end

         @implementation GADAdValuePrecisionHelper

         + (NSString *)stringFromAdValuePrecision:(GADAdValuePrecision)precision {
             switch (precision) {
                 case GADAdValuePrecisionPrecise:
                     return @"precise";
                 case GADAdValuePrecisionEstimated:
                     return @"estimated";
                 case GADAdValuePrecisionPublisherProvided:
                     return @"publisher_defined";
                 case GADAdValuePrecisionUnknown:
                 default:
                     return @"unknown";
             }
         }

         @end

         typedef NSString *GAAdType NS_TYPED_ENUM;

         GAAdType GAAdTypeBanner = @"bannerAd";
         GAAdType GAAdTypeInterstitial = @"interstitialAd";
         GAAdType GAAdTypeRewarded = @"rewardedAd";
         GAAdType GAAdTypeNative = @"nativeAd";
         GAAdType GAAdTypeAppOpen = @"appOpen";
         ```

      {% endlist %}

   3. Implement the logic for loading ads and generating impression reports:

      {% list tabs group=instructions %}

      - Swift

         ```swift translate=no
         class ViewController: UIViewController, GADFullScreenContentDelegate {
             var rewardedAd: GADRewardedAd?

             func requestRewardedAd() {
                 let originalType: GAAdType = .rewarded
                 let adType: AdType = .rewarded

                 GADRewardedAd.load(
                     withAdUnitID: "AD_UNIT_ID", request: GADRequest()
                 ) { [weak self] (ad, error) in
                     if let error = error {
                         print("Rewarded ad failed to load with error: \(error.localizedDescription)")
                         return
                     }
                     if let ad = ad {
                         self?.rewardedAd = ad
                         self?.rewardedAd?.paidEventHandler = { adValue in
                             // Extract the impression-level ad revenue data
                             let value = adValue.value
                             let precision = adValue.precision
                             let currencyCode = adValue.currencyCode

                             // Get the ad unit ID
                             let adUnitId = ad.adUnitID

                             // Get additional response info
                             let responseInfo = ad.responseInfo
                             let loadedAdNetworkResponseInfo = responseInfo.loadedAdNetworkResponseInfo
                             let adSourceId = loadedAdNetworkResponseInfo?.adSourceID
                             let adSourceInstanceId = loadedAdNetworkResponseInfo?.adSourceInstanceID
                             let adSourceInstanceName = loadedAdNetworkResponseInfo?.adSourceInstanceName
                             let adSourceName = loadedAdNetworkResponseInfo?.adSourceName
                             let mediationGroupName = responseInfo.extrasDictionary["mediation_group_name"] as? String
                             let mediationABTestName = responseInfo.extrasDictionary["mediation_ab_test_name"] as? String
                             let mediationABTestVariant = responseInfo.extrasDictionary["mediation_ab_test_variant"] as? String

                             // Create AdRevenueInfo object
                             let adRevenueInfo = MutableAdRevenueInfo(adRevenue: value, currency: currencyCode)
                             adRevenueInfo.adType = adType
                             adRevenueInfo.adNetwork = adSourceName ?? "AdMob"
                             adRevenueInfo.adUnitID = adUnitId
                             adRevenueInfo.adPlacementID = adSourceId
                             adRevenueInfo.precision = precision.description

                             // Create payload with additional information
                             var payload: [String: String] = [
                                 "original_ad_type": originalType.rawValue
                             ]
                             if let adSourceInstanceId = adSourceInstanceId {
                                 payload["ad_source_instance_id"] = adSourceInstanceId
                             }
                             if let adSourceInstanceName = adSourceInstanceName {
                                 payload["ad_source_instance_name"] = adSourceInstanceName
                             }
                             if let mediationGroupName = mediationGroupName {
                                payload["mediation_group_name"] = mediationGroupName
                             }
                             if let mediationABTestName = mediationABTestName {
                                payload["mediation_ab_test_name"] = mediationABTestName
                             }
                             if let mediationABTestVariant = mediationABTestVariant {
                                payload["mediation_ab_test_variant"] = mediationABTestVariant
                             }

                             adRevenueInfo.payload = payload

                             // Report to AppMetrica
                             AppMetrica.reportAdRevenue(adRevenueInfo) { error in
                                 print("Failed to report ad revenue: \(error)")
                             }
                         }
                     }
                  }
             }
         }
         ```

      - Objective-C

         ```objectivec translate=no
         @interface ViewController : UIViewController <GADFullScreenContentDelegate>

         @property (nonatomic, strong) GADRewardedAd *rewardedAd;

         @end

         @implementation ViewController

         - (void)requestRewardedAd {
             GAAdType originalType = GAAdTypeRewarded;
             AMAAdType adType = AMAAdTypeRewarded;
             [GADRewardedAd loadWithAdUnitID:@"AD_UNIT_ID"
                                     request:[GADRequest request]
                           completionHandler:^(GADRewardedAd * _Nullable rewardedAd, NSError * _Nullable error) {

                 if (error) {
                     NSLog(@"Rewarded ad failed to load with error: %@", [error localizedDescription]);
                     return;
                 }

                 self.rewardedAd = rewardedAd;
                 __weak typeof(self) weakSelf = self; // Avoid strong reference cycles
                 self.rewardedAd.paidEventHandler = ^(GADAdValue *adValue) {
                     // Extract the impression-level ad revenue data
                     NSDecimalNumber *value = adValue.value;
                     GADAdValuePrecision precision = adValue.precision;
                     NSString *currencyCode = adValue.currencyCode;

                     // Get the ad unit ID
                     NSString *adUnitId = weakSelf.rewardedAd.adUnitID;

                     // Create AdRevenueInfo object
                     AMAMutableAdRevenueInfo *adRevenueInfo = [[AMAMutableAdRevenueInfo alloc] initWithAdRevenue:value.doubleValue currency:currencyCode];
                     adRevenueInfo.adType = adType;
                     adRevenueInfo.adNetwork = @"AdMob";
                     adRevenueInfo.adUnitID = adUnitId;
                     adRevenueInfo.precision = [NSString stringWithFormat:@"%ld", (long)precision];
                     adRevenueInfo.payload = @{
                         @"original_ad_type": originalType
                     };

                     // Report to AppMetrica
                     [AMAYandexMetrica reportAdRevenue:adRevenueInfo onFailure:^(NSError *error) {
                         NSLog(@"Failed to report ad revenue: %@", error);
                     }];
                 };
             }];
         }

         @end
         ```

      {% endlist %}

   #### Adapt the implementation for other ad formats {#send-adrevenue-format}

   1. Replace `GADRewardedAd` with an appropriate class:

      - Banner: `GADBannerView`
      - Interstitial: `GADInterstitialAd`
      - Native: `GADNativeAd`
      - AppOpen: `GADAppOpenAd`

   2. Change `originalType` and `adType` in the `requestRewardedAd` method:

      {% list tabs group=instructions %}

      - Swift

         ```swift translate=no
         // For banner ads
         let originalType: GAAdType = .banner
         let adType: AdType = .banner

         // For interstitial and rewarded interstitial ads
         let originalType: GAAdType = .interstitial
         let adType: AdType = .interstitial

         // For native ads
         let originalType: GAAdType = .native
         let adType: AdType = .native

         // For rewarded ads (current example)
         let originalType: GAAdType = .native
         let adType: AdType = .rewarded     

         // For app open ads
         let originalType: GAAdType = .appOpen
         let adType: AdType = .appOpen
         ```

      - Objective-C

         ```objectivec translate=no
         // For banner ads
         GAAdType originalType = GAAdTypeBanner;
         AMAAdType adType = AMAAdTypeBanner;

         // For interstitial and rewarded interstitial ads
         GAAdType originalType = GAAdTypeInterstitial;
         AMAAdType adType = AMAAdTypeInterstitial;

         // For native ads
         GAAdType originalType = GAAdTypeNative;
         AMAAdType adType = AMAAdTypeNative;

         // For rewarded ads (current example)
         GAAdType originalType = GAAdTypeRewarded;
         AMAAdType adType = AMAAdTypeRewarded;

         // For app open ads
         GAAdType originalType = GAAdTypeAppOpen;
         AMAAdType adType = AMAAdTypeOther;
         ```

      {% endlist %}

   3. Configure the `paidEventHandler` at the appropriate stage of the ad loading process for each format. The implementation of the handler itself remains the same.
   4. For banner ads, add the `paidEventHandler` directly to the `GADBannerView` instance:

      {% list tabs group=instructions %}

      - Swift

         ```swift translate=no
         bannerView.paidEventHandler = { adValue in
             // Use the same implementation as in the rewarded ad example
         }
         ```

      - Objective-C

         ```objectivec translate=no
         bannerView.paidEventHandler = ^(GADAdValue *adValue) {
             // Use the same implementation as in the rewarded ad example
         };
         ```

      {% endlist %}

   5. For interstitial, rewarded interstitial, and native ads, add the `paidEventHandler` to the ad loading completion handler as shown in the example with rewarded ads.

   {% note info %}

   Don't forget to replace `AD_UNIT_ID` with your actual AdMob ad unit ID for each ad format you use.

   {% endnote %}

- ironSource

   Ad revenue data from the ironSource SDK is passed to AppMetrica via the `AppMetricaIronSourceAdapter`:
   - The adapter must be initialized before activating ironSource.
   - AppMetrica should only be activated once during the app lifecycle. It doesn't matter if you do it before or after initializing the adapter.

   1. Import the required modules:

      {% list tabs group=instructions %}

      - Swift

         ```swift translate=no
         import AppMetricaCore
         import AppMetricaIronSourceAdapter
         import IronSource
         ```

      - Objective-C

         ```objectivec translate=no
         #import <AppMetricaCore/AppMetricaCore.h>
         #import <AppMetricaIronSourceAdapter/AppMetricaIronSourceAdapter.h>
         import <IronSource/IronSource.h>
         ```

      {% endlist %}

   2. Initialize the `AppMetricaIronSourceAdapter` before activating ironSource. You can usually do this in the app's initialization code. For example, in the `AppDelegate` structure or the `main App` for `SwiftUI` apps.

      {% list tabs group=instructions %}

      - Swift

         ```swift translate=no
         AppMetricaIronSourceAdapter.shared.initialize()
         ```

      - Objective-C

         ```objectivec translate=no
         [[AppMetricaIronSourceAdapter shared] initialize];
         ```

      {% endlist %}

   3. Configure and activate ironSource and AppMetrica:

      {% list tabs group=instructions %}

      - Swift

         ```swift translate=no
         // Initialize IronSource
         IronSource.initWithAppKey("YOUR_IRONSOURCE_APP_KEY", adUnits: [IS_BANNER, IS_INTERSTITIAL, IS_REWARDED_VIDEO])

         // Activate AppMetrica
         guard let configuration = AppMetricaConfiguration(apiKey: "YOUR_APPMETRICA_API_KEY") else { return }
         AppMetrica.activate(with: configuration)
         ```

      - Objective-C

         ```objectivec translate=no
         // Initialize IronSource
         [IronSource initWithAppKey:@"YOUR_IRONSOURCE_APP_KEY" adUnits:@[IS_BANNER, IS_INTERSTITIAL, IS_REWARDED_VIDEO]];

         // Activate AppMetrica
         AppMetricaConfiguration *configuration = [[AppMetricaConfiguration alloc] initWithApiKey:@"YOUR_APPMETRICA_API_KEY"];
         if (configuration == nil) {
             return;
         }
         [AppMetrica activateWithConfiguration:configuration];
         ```

   {% endlist %}

   {% note info %}

   The `AppMetricaIronSourceAdapter` automatically passes ad revenue data from ironSource to AppMetrica. You don't need to report impressions or revenue manually.

   {% endnote %}

- TopOn

   1. Import the required modules:

      {% list tabs group=instructions %}

      - Swift

         ```swift translate=no
         import AppMetricaCore
         import AnyThinkSDK
         import AnyThinkBanner
         import AnyThinkNative
         import AnyThinkInterstitial
         import AnyThinkRewardedVideo
         import AnyThinkMediaVideo
         ```

      - Objective-C

         ```objectivec translate=no
         #import <AppMetricaCore/AppMetricaCore.h>
         #import <AnyThinkSDK/AnyThinkSDK.h>
         import <AnyThinkBanner/AnyThinkBanner.h>
         import <AnyThinkNative/AnyThinkNative.h>
         import <AnyThinkInterstitial/AnyThinkInterstitial.h>
         import <AnyThinkRewardedVideo/AnyThinkRewardedVideo.h>
         import <AnyThinkMediaVideo/AnyThinkMediaVideo.h>
         ```

      {% endlist %}

   2. Create a function for passing ad revenue data to AppMetrica:

      {% list tabs group=instructions %}

      - Swift

         ```swift translate=no
         enum ATAdType: String {
             case rewarded = "rewardedAd"
             case interstitial = "interstitialAd"
             case splash = "splashAd"
             case banner = "bannerAd"
             case native = "nativeAd"
             case mediaVideo = "mediaVideoAd"
         }

         func reportToAppMetrica(
             _ extra: [AnyHashable: Any],
             placementID: String,
             adType: AdType,
             originalAdType: ATAdType
         ) {
             guard let revenue = extra[kATADDelegateExtraPublisherRevenueKey] as? Double,
                   let currency = extra[kATADDelegateExtraCurrencyKey] as? String else {
                 print("Missing required revenue information")
                 return
             }

             let adRevenueInfo = MutableAdRevenueInfo(adRevenue: NSDecimalNumber(value: revenue), currency: currency)

             adRevenueInfo.adType = adType
             adRevenueInfo.adNetwork = extra[kATADDelegateExtraNetworkNameKey] as? String
             adRevenueInfo.adUnitID = extra[kATADDelegateExtraAdunitIDKey] as? String
             adRevenueInfo.adPlacementID = placementID
             adRevenueInfo.precision = extra[kATADDelegateExtraPrecisionKey] as? String

             // Additional information in payload
             var payload: [String: String] = [
                 "original_ad_type": originalAdType.rawValue
             ]
             if let networkFirmId = extra[kATADDelegateExtraNetworkFirmIdKey] as? Int {
                 payload["network_firm_id"] = String(networkFirmId)
             }
             payload["adsource_id"] = extra[kATADDelegateExtraAdSourceIdKey] as? String
             // Add other relevant information to payload...

             adRevenueInfo.payload = payload

             AppMetrica.reportAdRevenue(adRevenueInfo) { error in
                 print("Failed to report ad revenue to AppMetrica: \(error)")
             }
         }
         ```

      - Objective-C

         ```objectivec translate=no
         typedef NSString *ATAdType NS_TYPED_ENUM;

         ATAdType ATAdTypeRewarded = @"rewardedAd";
         ATAdType ATAdTypeInterstitial = @"interstitialAd";
         ATAdType ATAdTypeSplash = @"splashAd";
         ATAdType ATAdTypeBanner = @"bannerAd";
         ATAdType ATAdTypeNative = @"nativeAd";
         ATAdType ATAdTypeMediaVideo = @"mediaVideoAd";

         - (void)reportToAppMetricaWithExtra:(NSDictionary<AnyHashable, id> *)extra
                                 placementID:(NSString *)placementID
                                      adType:(AdType)adType
                              originalAdType:(ATAdType)originalAdType {
             NSNumber *revenue = extra[kATADDelegateExtraPublisherRevenueKey];
             NSString *currency = extra[kATADDelegateExtraCurrencyKey];

             if (revenue == nil || currency == nil) {
                 NSLog(@"Missing required revenue information");
                 return;
             }

             MutableAdRevenueInfo *adRevenueInfo = [[MutableAdRevenueInfo alloc] initWithAdRevenue:[NSDecimalNumber decimalNumberWithDecimal:[revenue decimalValue]] currency:currency];

             adRevenueInfo.adType = adType;
             adRevenueInfo.adNetwork = extra[kATADDelegateExtraNetworkNameKey];
             adRevenueInfo.adUnitID = extra[kATADDelegateExtraAdunitIDKey];
             adRevenueInfo.adPlacementID = placementID;
             adRevenueInfo.precision = extra[kATADDelegateExtraPrecisionKey];

             // Additional information in payload
             NSMutableDictionary<NSString *, NSString *> *payload = [NSMutableDictionary new];
             payload[@"original_ad_type"] = originalAdType;
             NSNumber *networkFirmId = extra[kATADDelegateExtraNetworkFirmIdKey];
             if (networkFirmId != nil) {
                 payload[@"network_firm_id"] = [networkFirmId stringValue];
             }
             payload[@"adsource_id"] = extra[kATADDelegateExtraAdSourceIdKey];
             // Add other relevant information to payload...

             adRevenueInfo.payload = payload;

             [AppMetrica reportAdRevenue:adRevenueInfo completion:^(NSError * _Nullable error) {
                 if (error) {
                     NSLog(@"Failed to report ad revenue to AppMetrica: %@", error);
                 }
             }];
         }
         ```

      {% endlist %}

   3. Implement the corresponding delegate methods for each ad format:

      {% list tabs group=instructions %}

      - Swift

         ```swift translate=no
         class YourBannerDelegate: NSObject, ATBannerDelegate {
             func bannerView(_ bannerView: ATBannerView, didShowAdWithPlacementID placementID: String, extra: [AnyHashable : Any]) {
                 reportToAppMetrica(
                     extra,
                     placementID: placementID,
                     adType: .banner,
                     originalAdType: .banner
                 )
             }
             // Implement other delegate methods as needed
         }

         class YourNativeDelegate: NSObject, ATNativeADDelegate {
             func didShowNativeAd(in adView: ATNativeADView, placementID: String, extra: [AnyHashable : Any]) {
                 reportToAppMetrica(
                     extra,
                     placementID: placementID,
                     adType: .native,
                     originalAdType: .native
                 )
             }
             // Implement other delegate methods as needed
         }

         class YourInterstitialDelegate: NSObject, ATInterstitialDelegate {
             func interstitialDidShow(forPlacementID placementID: String, extra: [AnyHashable : Any]) {
                 reportToAppMetrica(
                     extra,
                     placementID: placementID,
                     adType: .interstitial,
                     originalAdType: .interstitial
                 )
             }
             // Implement other delegate methods as needed
         }

         class YourRewardedVideoDelegate: NSObject, ATRewardedVideoDelegate {
             func rewardedVideoDidShow(forPlacementID placementID: String, extra: [AnyHashable : Any]) {
                 reportToAppMetrica(
                     extra,
                     placementID: placementID,
                     adType: .rewarded,
                     originalAdType: .rewarded
                 )
             }
             // Implement other delegate methods as needed
         }

         class YourSplashDelegate: NSObject, ATSplashDelegate {
             func splashDidShow(forPlacementID placementID: String, extra: [AnyHashable : Any]) {
                 reportToAppMetrica(
                     extra,
                     placementID: placementID,
                     adType: .other,
                     originalAdType: .splash
                 )
             }
             // Implement other delegate methods as needed
         }

         class YourMediaVideoDelegate: NSObject, ATMediaVideoDelegate {
             func mediaVideoDidStartPlaying(forPlacementID placementID: String, extra: [AnyHashable : Any]) {
                 reportToAppMetrica(
                     extra,
                     placementID: placementID,
                     adType: .other,
                     originalAdType: .mediaVideo
                 )
             }
             // Implement other delegate methods as needed
         }
         ```

      - Objective-C

         ```objectivec translate=no
         #import <AppMetricaCore/AppMetricaCore.h>
         #import <AnyThinkSDK/AnyThinkSDK.h>
         import <AnyThinkBanner/AnyThinkBanner.h>
         import <AnyThinkNative/AnyThinkNative.h>
         import <AnyThinkInterstitial/AnyThinkInterstitial.h>
         import <AnyThinkRewardedVideo/AnyThinkRewardedVideo.h>
         import <AnyThinkMediaVideo/AnyThinkMediaVideo.h>
         ```

      {% endlist %}

- Configuration for other systems

   1. Initialize the `MutableAdRevenueInfo` instance.
   2. Send the `MutableAdRevenueInfo` instance to the main API key using the `+reportAdRevenue:onFailure:` method of the `AppMetrica` class.

      {% list tabs group=instructions %}

      - Swift

         ```swift translate=no
         AppMetrica.report(adRevenue: adRevenueInfo) { error in
             print("AdRevenue error: \(error)")
         }
         ```

      - Objective-C

         ```objectivec translate=no
         [AMAAppMetrica reportAdRevenue:[adRevenueInfo copy] onFailure:^(NSError *error) {
             NSLog(@"AdRevenue error: %@", error);
         }];

         ```

      {% endlist %}

{% endlist %}

### Step 3. Make sure that the ad revenue data is included in the reports {#send-adrevenue-check-reports}

1. View ads in the app.

2. Make sure the [In-app and Ad Revenue](../../../mobile-reports/revenue-report.md) report shows the same number of ad revenue events as the number of ad views.

## Setting the session timeout duration {#session-timeout}

By default, the session timeout is 10 seconds. This is the minimum acceptable value for the `sessionTimeout` property.

{% list tabs group=instructions %}

- Swift

   To change the timeout length, pass the value in seconds to the `sessionTimeout` property of the library configuration `AppMetricaConfiguration`.

   ```swift translate=no
   // Creating an extended library configuration.
   if let configuration = AppMetricaConfiguration(apiKey: "API key") {
       // Setting the session timeout.
       configuration.sessionTimeout = 15
       // Initializing the AppMetrica SDK.
       AppMetrica.activate(with: configuration)
   }
   ```

- Objective-C

   To change the timeout length, pass the value in seconds to the `sessionTimeout` property of the library configuration `AMAAppMetricaConfiguration`.

   ```obj-c translate=no
   // Creating an extended library configuration.
   AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithAPIKey:@"API key"];
   // Setting the session timeout.
   configuration.sessionTimeout = 15;
   // Initializing the AppMetrica SDK.
   [AMAAppMetrica activateWithConfiguration:configuration];
   ```

{% endlist %}

## Setting the app version {#version-app}

By default, the app version is set in the app configuration file Info.plist (`CFBundleShortVersionString`).

{% list tabs group=instructions %}

- Swift

   To specify the app version from the code, pass it to the `appVersion` property of the `AppMetricaConfiguration` configuration.

   ```swift translate=no
   // Creating an extended library configuration.
   if let configuration = AppMetricaConfiguration(apiKey: "API key") {
       // Setting the app version.
       configuration.appVersion = "1.13.2"
       // Initializing the AppMetrica SDK.
       AppMetrica.activate(with: configuration)
   }
   ```

- Objective-C

   To specify the app version from the code, pass it to the `appVersion` property of the `AMAAppMetricaConfiguration` configuration.

   ```obj-c translate=no
   // Creating an extended library configuration.
   AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithAPIKey:@"API key"];
   // Setting the app version.
   configuration.appVersion = @"1.13.2";
   // Initializing the AppMetrica SDK.
   [AMAAppMetrica activateWithConfiguration:configuration];
   ```

{% endlist %}

## Tracking app opens using deeplinks {#deeplink}

{% include notitle [tracking-deplink](../../../_includes/tracking-deeplink.md) %}

For more information, see [How do I create a remarketing campaign in AppMetrica?](../../../troubleshooting/troubleshooting.md#remarketing-campaign)

## Tracking new users {#new-user}

By default, the user is counted as a new user when the app is opened for the first time. If you connect the AppMetrica SDK to an app that already has active users, you can set up tracking new and old users to get correct statistics.

{% list tabs group=instructions %}

- Objective-C

   To do this, initialize the AppMetrica SDK using the `AMAAppMetricaConfiguration` extended startup configuration.

   ```obj-c translate=no
   BOOL isFirstLaunch = NO;
   // Creating an extended library configuration.
   AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithAPIKey:@"API key"];
   // Implement the logic for detecting whether the app is starting for the first time.
   // For example, you can check for files (settings, databases, and so on),
   // which the app creates on its first launch.
   if (conditions) {
       isFirstLaunch = YES;
   }
   configuration.handleFirstActivationAsUpdate = !isFirstLaunch;
   // Initializing the AppMetrica SDK.
   [AMAAppMetrica activateWithConfiguration:configuration];
   ```

- Swift

   To do this, initialize the AppMetrica SDK using the `AppMetricaConfiguration` extended startup configuration.

   ```swift translate=no
   var isFirstLaunch = false
   // Creating an extended library configuration.
   guard let configuration = AppMetricaConfiguration(apiKey: "API key") else {
       print("AppMetricaConfiguration initialization failed.")
       return // or return someDefaultValue or throw someError
   }
   // Implement the logic for detecting whether the app is starting for the first time.
   // For example, you can check for files (settings, databases, and so on),
   // which the app creates on its first launch.
   if conditions {
       isFirstLaunch = true
   }
   configuration.handleFirstActivationAsUpdate = !isFirstLaunch
   // Initializing the AppMetrica SDK.
   AppMetrica.activate(with: configuration)
   ```

{% endlist %}

## Disabling and enabling sending statistics {#stat}

If you need confirmation from the user before sending statistical data, you should initialize the library with the disabled sending option.

{% list tabs group=instructions %}

- Objective-C

   To do this, set the `NO` value for the `dataSendingEnabled` property of the `AMAAppMetricaConfiguration`.

   ```obj-c translate=no
   // Creating an extended library configuration.
   AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithAPIKey:@"API key"];
   // Disabling sending statistics.
   configuration.dataSendingEnabled = NO;
   // Initializing the AppMetrica SDK.
   [AMAAppMetrica activateWithConfiguration:configuration];
   ```

   After the user has consented to sending statistics (for example, in the app settings or in the agreement on the first start of the app), you should enable sending using the `+setDataSendingEnabled:` method of the `AMAAppMetrica` class.

   ```obj-c translate=no
   // Checking the status of the boolean variable. It shows the user confirmation.
   if (flag) {
       // Enabling sending statistics.
       [AMAAppMetrica setDataSendingEnabled:YES];
   }
   ```

- Swift

   To do this, set the `false` value for the `dataSendingEnabled` property of the `AppMetricaConfiguration`.

   ```swift translate=no
   // Creating an extended library configuration.
   if let configuration = AppMetricaConfiguration(apiKey: "API key") {
       // Disabling sending statistics.
       configuration.dataSendingEnabled = false
       // Initializing the AppMetrica SDK.
       AppMetrica.activate(with: configuration)
   }
   ```

   After the user has consented to sending statistics (for example, in the app settings or in the agreement on the first start of the app), you should enable sending using the `setDataSendingEnabled(_:)` method of the `AppMetrica` class.

   ```swift translate=no
   // Checking the status of the boolean variable. It shows the user confirmation.
   if flag {
       // Enabling sending statistics.
       AppMetrica.setDataSendingEnabled(true);
   }
   ```

{% endlist %}

### Alert example {#stat-alert-example}

You can use any text to inform users of statistics collection. For example:

> This app uses the AppMetrica analytical service provided by YANDEX LLC, ulitsa Lva Tolstogo 16, Moscow, Russia 119021 (hereinafter referred to as Yandex) based on the [Terms of Use](https://yandex.com/legal/metrica_termsofuse/).
>
> AppMetrica analyzes app usage data, including the device it is running on, the installation source, calculates conversion, collects statistics of your activity for product analytics, ad campaign analysis, and optimization, as well as for troubleshooting. Information collected in this way cannot identify you.
>
> Depersonalized information about your use of this app collected by AppMetrica tools will be transferred to Yandex and stored on Yandex’s server in the EU and the Russian Federation. Yandex will process this information to assess how you use the app, compile reports for us on our app operation, and provide other services.

## Getting AppMetrica SDK IDs {#get-ids}

To get AppMetrica SDK IDs (`DeviceId`, `DeviceIdHash`, `UUID`), use the `requestStartupIdentifiersWithKeys()` / `requestStartupIdentifiers()` method. To get the `appmetrica_device_id`, make sure to request the `DeviceIdHash`.

{% list tabs group=instructions %}

- Objective-C

   ```obj-c translate=no
   AMAIdentifiersCompletionBlock block = ^(NSDictionary<AMAStartupKey,id> * _Nullable identifiers, NSError * _Nullable error) {
       if (identifiers[kAMADeviceIDHashKey] != nil) {
           NSLog(@"deviceIDHash = %@", identifiers[kAMADeviceIDHashKey]);
       }
       if (identifiers[kAMADeviceIDKey] != nil) {
           NSLog(@"deviceID = %@", identifiers[kAMADeviceIDKey]);
       }
       if (identifiers[kAMAUUIDKey] != nil) {
           NSLog(@"uuid = %@", identifiers[kAMAUUIDKey]);
       }
   };
   [AMAAppMetrica requestStartupIdentifiersWithKeys:@[kAMADeviceIDHashKey, kAMADeviceIDKey, kAMAUUIDKey] completionQueue:nil completionBlock:block];
   ```

- Swift

   ```swift translate=no
   // Specifying the keys for which we need to get identifiers
   let keys: [StartupKey] = [StartupKey.deviceIDKey, StartupKey.deviceIDHashKey, StartupKey.uuidKey]

   // Specifying the queue on which the completion handler will be executed (for example, the main thread)
   let queue = DispatchQueue.main

   // Requesting IDs
   AppMetrica.requestStartupIdentifiers(for: keys, on: queue) { identifiers, error in
       if let error = error {
           print("An error has occurred: \(error.localizedDescription)")
       } else if let identifiers = identifiers {
           // Processing the received IDs
           if let deviceIDHash = identifiers[StartupKey.deviceIDHashKey] as? String {
               print("AppMetrica deviceIDHash: \(deviceIDHash)")
           }
           if let deviceID = identifiers[StartupKey.deviceIDKey] as? String {
               print("AppMetrica deviceID: \(deviceID)")
           }
           if let uuid = identifiers[StartupKey.uuidKey] as? String {
               print("AppMetrica uuid: \(uuid)")
           }
       }
   }  
   ```

{% endlist %}

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}

[*remarketing campaigns]: An ad campaign aimed at getting users to come back to an app they previously installed. For more information, see [Creating a remarketing tracker](../../../mobile-tracking/add-remarketing-tracker.md).
