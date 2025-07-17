# Migrating to version 2.0.0

When you migrate your app from `YandexMobileMetricaPush` to `AppMetricaPush`, the main IDs and data are preserved. That means the transition to the new version shouldn't result in issues or anomalies in the reports.

To migrate to the new version, follow these steps:

1. Update AppMetrica SDK by following the [guide](../analytics/migration-io-5-0-0.md).
2. Replace dependencies. The required changes are provided in the [dependency renaming section](#rename-modules).
3. Make sure you're not running [two different AppMetrica Push SDK versions in parallel](#two-versions).
4. Import dependencies in the code. The required changes are provide in the [dependency importing section](#import-modules).
5. In the project code, replace the classes and methods that were simply renamed. The required changes are provided in the [API renaming section](#rename-api).
6. If you have any questions, contact [support](../../../troubleshooting/feedback-new.md).

## Renamed dependencies {#rename-modules}

{% list tabs group=instructions %}

- CocoaPods

   ```ruby translate=no
   pod 'YandexMobileMetricaPush', '~> 1.3.0'
   ```

   Replace with:

   ```ruby translate=no
   pod 'AppMetricaPush', '~> 2.0.0' # Main module for working with Push SDK, it's required for connecting
   pod 'AppMetricaPushLazy', '~> 2.0.0' # Additional module for lazy push notifications
   ```

- Package.swift

   #### When using the Package.swift manifest

   1. Delete the `.package` dependency with `metrica-push-sdk-ios` from the file `Package.swift` in your project together with all references to the dependencies in the `targets:` section within your project.
   2. Insert the following code to add the new `push-sdk-ios` dependency:

      ```swift translate=no
      dependencies: [
         .package(
            url: "https://github.com/appmetrica/push-sdk-ios",
            from: "2.0.0"
         )
      ],
      ```

   3. Add the required modules to your project's targets.

      The AppMetrica Push SDK modules that you can enable depending on the needs of your project:

      * `AppMetricaPush`: The main mandatory Push SDK module. You need to enable it to use AppMetrica.
      * `AppMetricaPushLazy`: Additional module for lazy push notifications.

      ```swift translate=no
      .target(
         name: "MyTargetName",
         dependencies: [
            .product(name: "AppMetricaPush", package: "push-sdk-ios"),
            // .product(name: "AppMetricaPushLazy", package: "push-sdk-ios"), // This module is disabled
         ]
      ),
      ```

{% endlist %}

## Running two versions of AppMetrica Push SDK in parallel {#two-versions}

We renamed the group and main artifacts. As a result, you can use two AppMetrica Push SDK versions in a single app in parallel: AppMetrica Push version 1.3.0 and lower (`YandexMobileMetricaPush`) and version 2.0.0 and higher (`AppMetricaPush`). However, we recommend avoiding this approach because it requires processing push notifications twice and implementing a custom `UINotificationCenterDelegate` to invoke handlers from different versions of the AppMetrica Push SDK.

### How to make sure that YandexMobileMetricaPush isn't used

{% list tabs %}

- CocoaPods

   Open `Podfile.lock` and search `YandexMobileMetricaPush`.

   From the `PODS` section of the `Podfile.lock` file, you can understand which dependency refers to `YandexMobileMetricaPush`.

   ```
   PODS:
     ...
      FizzLibarry (10.0.0):
       - BuzzLibrary (= 11.0.0)
       - YandexMobileMetricaPush (< 2.0.0, >= 1.3.0)
     ...
   ```

- SPM in Xcode

   #### If dependencies are set via Xcode

   Open the project in Xcode. Make sure that `Package Dependencies` don't contain `YandexMobileMetricaPush`.

- Package.swift

   #### When using the Package.swift manifest

   If your project uses the Package.swift manifest to manage dependencies, execute the `swift package show-dependencies` command in the terminal in your project's directory. This will output a list of all project dependencies, including transitive ones.

   ```bash translate=no
   .
   └── fizz-library<https://github.com/appmetrica/fizz@10.0.0>
     ├──buzz-library<https://github.com/appmetrica/buzz@28.0.0>
     ├── metrica-sdk-push-ios<https://github.com/yandexmobile/metrica-sdk-push-ios@1.3.0>
   ```

   You can also check the `Package.resolved` file for the `YandexMobileMetricaPush` dependency.

   ```json translate=no
   {
     "object": {
       "pins": [
         //...
         {
           "package": "YandexMobileMetricaPush",
           "repositoryURL": "https://github.com/yandexmobile/metrica-sdk-push-ios",
           "state": {
             "branch": null,
             "revision": "37012eb6d43ad7d9fc32801855f0eb62a53deec7",
             "version": "1.3.0"
           }
         },
         //...
       ]
     },
     // ...
   }
   ```

{% endlist %}

## Importing dependencies {#import-modules}

{% list tabs group=instructions %}

- Swift

   ```swift translate=no
   import YandexMobileMetricaPush
   ```

   Replace with:

   ```swift translate=no
   import AppMetricaPush
   import AppMetricaPushLazy // Additional module for lazy push notifications
   ```

- Objective-C

   ```obj-c translate=no
   #import <YandexMobileMetricaPush/YandexMobileMetricaPush.h>
   ```

   Replace with:

   ```obj-c translate=no
   #import <AppMetricaPush/AppMetricaPush.h>
   #import <AppMetricaPushLazy/AppMetricaPushLazy.h> // Additional module for lazy push notifications
   ```

{% endlist %}

## Renaming the API {#rename-api}

{% list tabs group=instructions %}

- Swift

   Removed the `YMP` prefix.

   * Renamed the `YMPYandexMetricaPush` interface to `AppMetricaPush`.
      * Removed the `userNotificationCenterDelegate` method. Use the `userNotificationCenterDelegate` property.
      * Removed the `userNotificationCenterHandler` method. Use the `userNotificationCenterHandler` property.
   * Renamed the `YMPUserNotificationCenterDelegate` protocol to `UserNotificationCenterDelegate`.
   * Renamed the `YMPUserNotificationCenterHandling` protocol to `UserNotificationCenterHandling`.
   * Renamed the `YMPYandexMetricaPushEnvironment` enumeration to `AppMetricaPushEnvironment`.

- Objective-C

   Changed the `YMP` prefix to `AMP`.

   * Renamed the `YMPYandexMetricaPush` interface to `AMPAppMetricaPush`.
      * Renamed the `userNotificationCenterDelegate` class method to the `userNotificationCenterDelegate` class property.
      * Renamed the `userNotificationCenterHandler` class method to the `userNotificationCenterHandler` class.
   * Renamed the `YMPUserNotificationCenterDelegate` protocol to `AMPUserNotificationCenterDelegate`.
   * Renamed the `YMPUserNotificationCenterHandling` protocol to `AMPUserNotificationCenterHandling`.
   * Renamed the `YMPYandexMetricaPushEnvironment` enumeration to `AMPAppMetricaPushEnvironment`.

{% endlist %}
