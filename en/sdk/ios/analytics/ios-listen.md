# Tracking user activity

{% include notitle [Отслеживание активности пользователей](../../_includes/listen-intro.md) %}

## Setting the session timeout {#timeout}

{% include notitle [отсчет таймаута](../../_includes/timeout-notify-listen.md) %}

{% list tabs group=instructions %}

- Swift

   To change the timeout length, pass the value in seconds to the `sessionTimeout` property of the library configuration `AppMetricaConfiguration`.

   By default, the session timeout is 10 seconds. This is the minimum acceptable value for the `sessionTimeout` property.

   ```swift translate=no
   // Creating an extended library configuration.
   let configuration = AppMetricaConfiguration(apiKey: "API key")
   // Setting the session timeout.
   configuration?.sessionTimeout = 15
   // Initializing the AppMetrica SDK.
   AppMetrica.activate(with: configuration!)
   ```

- Objective-C

   To change the timeout length, pass the value in seconds to the `sessionTimeout` property of the library configuration `AMAAppMetricaConfiguration`.

   By default, the session timeout is 10 seconds. This is the minimum acceptable value for the `sessionTimeout` property.

   ```obj-c translate=no
   // Creating an extended library configuration.
   AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithAPIKey:@"API key"];
   // Setting the session timeout.
   configuration.sessionTimeout = 15;
   // Initializing the AppMetrica SDK.
   [AMAAppMetrica activateWithConfiguration:configuration];
   ```

{% endlist %}

## Tracking sessions manually {#listen}

By default, AppMetrica automatically tracks the lifecycle of apps. To track sessions manually:

1. Initialize the library with automatic session tracking `sessionsAutoTracking` disabled.

   {% list tabs group=instructions %}

   - Swift

      ```swift translate=no
      // Creating an extended library configuration.
      if let configuration = AppMetricaConfiguration(apiKey: "API key") {
         // Disabling the automatic tracking of user activity.
         configuration.sessionsAutoTracking = false
         // ...
         // Initializing the AppMetrica SDK.
         AppMetrica.activate(with: configuration)
      }
      ```

   - Objective-C

      ```obj-c translate=no
      // Creating an extended library configuration.
      AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithAPIKey:@"API key"];
      // Disabling the automatic tracking of user activity.
      configuration.sessionsAutoTracking = NO;
      // ...
      // Initializing the AppMetrica SDK.
      [AMAAppMetrica activateWithConfiguration:configuration];
      ```

   {% endlist %}

2. Set up session control using the `resumeSession` and `pauseSession` methods.

   {% list tabs group=instructions %}

   - Swift

      ```swift translate=no
      AppMetrica.resumeSession()
      // ...
      AppMetrica.pauseSession()
      ```

   - Objective-C

      ```obj-c translate=no
      [AMAAppMetrica resumeSession];
      // ...
      [AMAAppMetrica pauseSession];
      ```

   {% endlist %}

When using manual tracking, make sure that the current active session always ends with the `pauseSession` method invoke. If you don't invoke the `pauseSession` method, the session will be ended the next time the app is launched.

## Tracking sessions for reporters {#reporter-listen}

For correct tracking, the reporters should be manually configured to send events about the start and the pause of the session for each reporter:

{% list tabs group=instructions %}

- Swift

   ```swift translate=no
   guard let reporter = AppMetrica.reporter(for: "API key") else {
       print("AppMetrica reporter initialization failed.")
       return // or return someDefaultValue or throw someError
   }
   reporter.resumeSession()
   // ...
   reporter.reportEvent(name: "Updates installed", onFailure: { (error) in
       print("REPORT ERROR: \(error.localizedDescription)")
   })
   // ...
   reporter.pauseSession()
   ```

- Objective-C

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

## Sessions for App Extensions

By default, the AppMetrica SDK doesn't track sessions for App Extensions and all activity is tracked in background sessions. If required, use the methods provided in the [Tracking sessions manually](#listen) section.

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}

[*timeout-session]: Session timeout that you set in the SDK.
