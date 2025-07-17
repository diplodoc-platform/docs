# Usage examples

## Library initialization with the extended configuration {#initialize}

To initialize the library with an extended startup configuration, pass an `AppMetricaConfig` instance with appropriate settings and activate the library using the `AppMetrica.activate(AppMetricaConfig config)` method. Using an extended configuration, you can enable or disable logging, set session timeout, pass parameters for tracking pre-installed apps, and so on.

Extended configuration settings take effect immediately upon library initialization.

```java translate=no
AppMetrica.activate(
      AppMetricaConfig(API_KEY, logs: true
          // ...
          ));
```

## Sending statistics to an additional API key {#reporter-different-apikey}

Sending data to an additional API key allows you to collect own statistics for these API keys. You can use this to control access to information for other users. For example, to provide access to statistics for analysts you can duplicate sending marketing data for the additional API key. Thus they will only have access to the information they need.

To send data to an additional API key, you must use reporters. Just like for the main API key, you can set up an extended startup configuration for a reporter, send events, profile information, and data about in-app purchases. The reporter can work without the AppMetrica SDK initialization.

### Step 1. (Optional) Initialize a reporter with an extended configuration {#reporter-different-apikey-initialize}

To initialize a reporter with an extended configuration, create an instance of the `AppMetricaReporterConfig` class and specify the necessary configurations. Then, activate the reporter using the `AppMetrica.activateReporter(AppMetricaReporterConfig reporterConfig)` method. This configuration is used for a reporter with the specified API key. You can set up your own configuration for each additional API key.

{% note alert %}

The reporter with an extended configuration should be initialized before the first call to the reporter. Otherwise, the reporter will be initialized without a configuration.

{% endnote %}

```dart translate=no
// Creating extended configuration of the reporter.
// To create it, pass a ANOTHER_API_KEY that is different from the app's API_KEY.
AppMetricaReporterConfig reporterConfig = AppMetricaReporterConfig("ANOTHER_API_KEY",
    // Setting up the configuration. For example, to enable logging.
    logs: true);
// Initializing a reporter.
AppMetrica.activateReporter(reporterConfig);
```

### Step 2. Configure sending data using a reporter {#reporter-different-apikey-send}

To send data using a reporter, first get the object that implements the `AppMetricaReporter` abstract class by calling the `AppMetrica.getReporter(String apiKey)` method. Then, use the interface methods for sending reports. If the reporter was not initialized with an extended configuration, calling this method will initialize the reporter for the specified API key.

Example of sending an event:

```dart translate=no
AppMetrica.getReporter("ANOTHER_API_KEY").reportEvent("Updates installed");
```

For correct tracking, manually configure the reporters to send events about the start and the pause of the session for each reporter. For this, use the `resumeSession()` and `pauseSession()` methods:

```dart translate=no
AppMetricaReporter reporter = AppMetrica.getReporter("ANOTHER_API_KEY");
reporter.resumeSession();
reporter.reportEvent("Updates installed");
reporter.pauseSession();
```

## Using the library to send device location {#track-location}

Sending device location is disabled by default for Android. To enable sending it, initialize the library with the configuration where sending device location data is enabled. To do this, set the `locationTracking` property to `true` when creating an extended library configuration:

```java translate=no
AppMetrica.activate(AppMetricaConfig(API_KEY,
	locationTracking: true));
```

To enable sending at app runtime, use the `AppMetrica.setLocationTracking(bool enabled)` method:

```java translate=no
AppMetrica.setLocationTracking(true);
```

For more precise locations, add one of the following permissions to the AndroidManifest.xml file:

- `android.permission.ACCESS_COARSE_LOCATION` — For approximate determination.
- `android.permission.ACCESS_FINE_LOCATION` — For accurate determination.

## Setting location manually {#location-manual}

Before sending custom information about the device location, make sure that report sending is enabled.

The library determines the device location on its own. To send your own data about the device location, pass `AppMetricaLocation` to the `AppMetrica.setLocation(AppMetricaLocation? location)` method:

```java translate=no
// Determining the location.
AppMetricaLocation location = AppMetricaLocation(latitude, longitude);
//  Setting up custom device location data.
AppMetrica.setLocation(location);
```

To send custom device location using an extended configuration, pass the `AppMetricaLocation` instance to the `location` property when creating an extended library configuration:

```java translate=no
AppMetricaLocation location = AppMetricaLocation(latitude, longitude);
AppMetrica.activate(AppMetricaConfig(API_KEY,
	location: location));
```

## Sending a custom event {#report-event}

To send a custom event without nested parameters, pass a short name or description of the event to the `AppMetrica.reportEvent(String eventName)` method:

```dart translate=no
AppMetrica.reportEvent("eventName");
```

## Sending a custom event with nested parameters {#report-event-params}

To send parameters in JSON format:

```dart translate=no
String jsonAttributes = '{"item":"book","price":9.99}';

AppMetrica.reportEventWithJson("Purchase", jsonAttributes);
```

To send parameters as a Map object:

```dart translate=no
Map<String, dynamic> attributesMap = {"item": "book", "price": 9.99};
AppMetrica.reportEventWithMap("Purchase", attributesMap);
```

## Sending a custom error message {#send-report-error}

To send a custom error message, use the following method:

```dart translate=no
AppMetrica.reportError(
  message: "Error occurred",
  errorDescription: AppMetricaErrorDescription(StackTrace.current),
);
```

To send an error message with a group ID:

```dart translate=no
AppMetrica.reportErrorWithGroup(
  "IDENTIFIER",
  message: "MESSAGE",
  errorDescription: AppMetricaErrorDescription(StackTrace.current),
);
```

## Sending events from the buffer {#send-events-buffer}

AppMetrica SDK does not send an event immediately after it occurred. The library stores event data in the buffer. The `sendEventsBuffer` method sends data from the buffer and flushes it. Use the method to force sending stored events after passing important checkpoints of user scenarios.

```dart translate=no
AppMetrica.sendEventsBuffer();
```

{% note alert "" %}

If you use this method frequently, this may result in increased internet traffic and energy consumption.

{% endnote %}

## Monitoring the app lifecycle manually {#listen}

AppMetrica tracks session boundaries automatically. If needed, you can disable automatic session tracking by passing `false` to the `SessionsAutoTrackingEnabled` property in the extended library configuration.

```dart translate=no
AppMetrica.activate(
    AppMetricaConfig(API_KEY, sessionsAutoTrackingEnabled: false));
```

To monitor the app lifecycle manually, use the following methods:

- Pause session:

   ```dart translate=no
   AppMetrica.pauseSession();
   ```

- Resume session or start a new one:

   ```dart translate=no
   AppMetrica.resumeSession();
   ```

## Tracking app crashes {#set-report-crash}

Reports on app crashes are sent by default.

To disable automatic monitoring, initialize the library with the configuration in which sending crashes is disabled. To do this, pass the `false` value to the `crashReporting` and `flutterCrashReporting` properties when creating an extended library configuration.

```dart translate=no
AppMetrica.activate(AppMetricaConfig("daa46e63-d4a6-46d1-bbf9-0dcf4b482b83",
    // Disabling the data sending about the native android/ios crashes.
    crashReporting: false,
    // Disabling the data sending about the Flutter crashes.
    flutterCrashReporting: false));
```

## Manually monitoring app crashes {#report-unhandled}

Reports on app crashes are sent by default. To prevent event duplication when sending crashes manually, disable the automatic monitoring of app crashes.

To send crash data manually, use the `AppMetrica.reportUnhandledException(AppMetricaErrorDescription errorDescription)` method.

```dart translate=no
AppMetrica.reportUnhandledException(
  AppMetricaErrorDescription.fromCurrentStackTrace(
      message: 'Error message', type: 'Error type'),
);
```

## Sending ProfileId {#send-profile-id}

If you know the user profile ID before initializing the AppMetrica SDK, pass it before initialization (`setUserProfileID`) or during initialization with the extended configuration (`withUserProfileID`).

Otherwise, a technical profile is created with the ID `appmetrica_device_id`.

You can update `ProfileId` at any time by calling `setUserProfileID`:

```dart translate=no
AppMetrica.setUserProfileID("id");
```

## Sending profile attributes {#send-attribute-profile}

To send profile attributes, pass an instance of the `UserProfile` class to the `AppMetrica.reportUserProfile(UserProfile)` method.

```dart translate=no
AppMetricaUserProfile userProfile = AppMetricaUserProfile([
  // Updating predefined attributes.
  AppMetricaNameAttribute.withValue("John"),
  AppMetricaGenderAttribute.withValue(AppMetricaGender.male),
  AppMetricaBirthDateAttribute.withAge(24),
  AppMetricaNotificationEnabledAttribute.withValue(false),

  // Updating custom attributes.
  AppMetricaStringAttribute.withValue("string_attribute", "string"),
  AppMetricaNumberAttribute.withValue("number_attribute", 55),
  AppMetricaCounterAttribute.withDelta("counter_attribute", 1)
]);

// Setting the ProfileID using the method of the YandexMetrica class.
AppMetrica.setUserProfileID("id");

// Sending the UserProfile instance.
AppMetrica.reportUserProfile(userProfile);
```

## Sending E-commerce events {#send-ecommerce}

AppMetrica doesn't let you segment E-commerce events into test and non-test events. If you use the main API key for debugging purchases, the test events are included in general statistics. Therefore, to debug E-commerce event sending, use a reporter to send statistics to the additional API key.

### Step 1. Create a test app in AppMetrica {#send-ecommerce-test}

Specify the app parameters: link in the app store (if the app isn't published yet, leave the field empty), name, category, and time zone for generating reports.

To add another app, click [Add app](https://appmetrika.yandex.{{ domain }}/application/new) in the drop-down list in AppMetrica.

### Step 2. Configure sending E-commerce events to the test API key {#send-ecommerce-test-key}

For different user actions, there are appropriate types of e-commerce events. To create a specific event type, use the appropriate AppMetricaECommerce class method.

The examples below show how to send specific types of events.

{% cut "Opening a page" %}

```dart translate=no
Map<String, String> payload = {
  "configuration": "landscape",
  "full_screen": "true",
};
// Creating a screen object.
AppMetricaECommerceScreen screen = AppMetricaECommerceScreen(
    name: "ProductCardActivity", // Optional.
    searchQuery: "danissimo maple syrup", // Optional.
    payload: payload, // Optional.
    categoriesPath: ["Promos", "Hot deal"] // Optional.
    );
AppMetricaECommerceEvent showScreenEvent = AppMetricaECommerce.showScreenEvent(screen);
// Sending an e-commerce event.
AppMetrica.getReporter("Testing API key").reportECommerce(showScreenEvent);
```

{% endcut %}

{% cut "Viewing a product card" %}

```dart translate=no
Map<String, String> payload = {
  "configuration": "landscape",
  "full_screen": "true"
};
// Creating a screen object.
AppMetricaECommerceScreen screen = AppMetricaECommerceScreen(
    name: "ProductCardActivity", // Optional.
    searchQuery: "danissimo maple syrup", // Optional.
    payload: payload, // Optional.
    categoriesPath: ["Promos", "Hot deal"] // Optional.
    );
AppMetricaECommerceAmount amount =
    AppMetricaECommerceAmount(amount: Decimal.parse('4.53'), currency: "USD");
// Creating an actualPrice object.
AppMetricaECommercePrice actualPrice =
    AppMetricaECommercePrice(fiat: amount, internalComponents: [
  // Optional.
  AppMetricaECommerceAmount(amount: Decimal.parse('30_570_000'), currency: "wood"),
  AppMetricaECommerceAmount(amount: Decimal.parse('26.89'), currency: "iron"),
  AppMetricaECommerceAmount(amount: Decimal.parse('5.1'), currency: "gold"),
]);
// Creating an originalPrice object.
AppMetricaECommercePrice originalPrice = AppMetricaECommercePrice(
    fiat: AppMetricaECommerceAmount(amount: Decimal.parse('5.78'), currency: "USD"),
    internalComponents: [
      // Optional.
      AppMetricaECommerceAmount(amount: Decimal.parse('30570000'), currency: "wood"),
      AppMetricaECommerceAmount(amount: Decimal.parse('26.89'), currency: "iron"),
      AppMetricaECommerceAmount(amount: Decimal.parse('5.1'), currency: "gold"),
    ]);
// Creating a product object.
AppMetricaECommerceProduct product = AppMetricaECommerceProduct(
    sku: "779213",
    name: "Danissimo curd product 5.9%, 130 g", // Optional.
    actualPrice: actualPrice, // Optional.
    originalPrice: originalPrice, // Optional.
    promocodes: ["BT79IYX", "UT5412EP"], // Optional.
    payload: payload, // Optional.
    categoriesPath: [
      "Groceries",
      "Dairy",
      "Yogurts"
    ] // Optional.
    );
AppMetricaECommerceEvent showProductCardEvent =
    AppMetricaECommerce.showProductCardEvent(product, screen);
// Sending an e-commerce event.
AppMetrica.getReporter("Testing API key")
    .reportECommerce(showProductCardEvent);
```

{% endcut %}

{% cut "Viewing a product page" %}

```dart translate=no
Map<String, String> payload = {
  "configuration": "landscape",
  "full_screen": "true"
};
// Creating a screen object.
AppMetricaECommerceScreen screen = AppMetricaECommerceScreen(
    name: "ProductCardActivity", // Optional.
    searchQuery: "danissimo maple syrup", // Optional.
    payload: payload, // Optional.
    categoriesPath: ["Promos", "Hot deal"] // Optional.
    );
AppMetricaECommerceAmount amount =
    AppMetricaECommerceAmount(amount: Decimal.parse('4.53'), currency: "USD");
// Creating an actualPrice object.
AppMetricaECommercePrice actualPrice =
    AppMetricaECommercePrice(fiat: amount, internalComponents: [
  // Optional.
  AppMetricaECommerceAmount(amount: Decimal.parse('30_570_000'), currency: "wood"),
  AppMetricaECommerceAmount(amount: Decimal.parse('26.89'), currency: "iron"),
  AppMetricaECommerceAmount(amount: Decimal.parse('5.1'), currency: "gold"),
]);
// Creating an originalPrice object.
AppMetricaECommercePrice originalPrice = AppMetricaECommercePrice(
    fiat: AppMetricaECommerceAmount(amount: Decimal.parse('5.78'), currency: "USD"),
    internalComponents: [
      // Optional.
      AppMetricaECommerceAmount(amount: Decimal.parse('30570000'), currency: "wood"),
      AppMetricaECommerceAmount(amount: Decimal.parse('26.89'), currency: "iron"),
      AppMetricaECommerceAmount(amount: Decimal.parse('5.1'), currency: "gold"),
    ]);
// Creating a product object.
AppMetricaECommerceProduct product = AppMetricaECommerceProduct(
    sku: "779213",
    name: "Danissimo curd product 5.9%, 130 g", // Optional.
    actualPrice: actualPrice, // Optional.
    originalPrice: originalPrice, // Optional.
    promocodes: ["BT79IYX", "UT5412EP"], // Optional.
    payload: payload, // Optional.
    categoriesPath: [
      "Groceries",
      "Dairy",
      "Yogurts"
    ] // Optional.
    );
AppMetricaECommerceEvent showProductDetailsEvent =
    AppMetricaECommerce.showProductDetailsEvent(product, screen);
// Sending an e-commerce event.
AppMetrica.getReporter("Testing API key")
    .reportECommerce(showProductDetailsEvent);
```

{% endcut %}

{% cut "Adding/removing an item to/from the cart" %}

```dart translate=no
Map<String, String> payload = {
  "configuration": "landscape",
  "full_screen": "true"
};
// Creating a screen object.
AppMetricaECommerceScreen screen = AppMetricaECommerceScreen(
    name: "ProductCardActivity", // Optional.
    searchQuery: "danissimo maple syrup", // Optional.
    payload: payload, // Optional.
    categoriesPath: ["Promos", "Hot deal"] // Optional.
    );
AppMetricaECommerceAmount amount =
    AppMetricaECommerceAmount(amount: Decimal.parse('4.53'), currency: "USD");
// Creating an actualPrice object.
AppMetricaECommercePrice actualPrice =
    AppMetricaECommercePrice(fiat: amount, internalComponents: [
  // Optional.
  AppMetricaECommerceAmount(amount: Decimal.parse('30570000'), currency: "wood"),
  AppMetricaECommerceAmount(amount: Decimal.parse('26.89'), currency: "iron"),
  AppMetricaECommerceAmount(amount: Decimal.parse('5.1'), currency: "gold"),
]);
// Creating an originalPrice object.
AppMetricaECommercePrice originalPrice = AppMetricaECommercePrice(
    fiat: AppMetricaECommerceAmount(amount: Decimal.parse('5.78'), currency: "USD"),
    internalComponents: [
      // Optional.
      AppMetricaECommerceAmount(amount: Decimal.parse('30570000'), currency: "wood"),
      AppMetricaECommerceAmount(amount: Decimal.parse('26.89'), currency: "iron"),
      AppMetricaECommerceAmount(amount: Decimal.parse('5.1'), currency: "gold"),
    ]);
// Creating a product object.
AppMetricaECommerceProduct product = AppMetricaECommerceProduct(
    sku: "779213",
    name: "Danissimo curd product 5.9%, 130 g", // Optional.
    actualPrice: actualPrice, // Optional.
    originalPrice: originalPrice, // Optional.
    promocodes: ["BT79IYX", "UT5412EP"], // Optional.
    payload: payload, // Optional.
    categoriesPath: [
      "Groceries",
      "Dairy",
      "Yogurts"
    ] // Optional.
    );
AppMetricaECommerceReferrer referrer = AppMetricaECommerceReferrer(
    type: "button", // Optional.
    identifier: "76890", // Optional.
    screen: screen // Optional.
    );
// Creating a cartItem object.
AppMetricaECommerceCartItem addedItems1 = AppMetricaECommerceCartItem(
    product: product,
    revenue: actualPrice,
    quantity: Decimal.parse("1.0"),
    referrer: referrer // Optional.
    );
AppMetricaECommerceEvent addCartItemEvent = AppMetricaECommerce.addCartItemEvent(addedItems1);
// Sending an e-commerce event.
AppMetrica.getReporter("Testing API key").reportECommerce(addCartItemEvent);
AppMetricaECommerceEvent removeCartItemEvent =
    AppMetricaECommerce.removeCartItemEvent(addedItems1);
// Sending an e-commerce event.
AppMetrica.getReporter("Testing API key")
    .reportECommerce(removeCartItemEvent);
```

{% endcut %}

{% cut "Starting and completing a purchase" %}

```dart translate=no
Map<String, String> payload = {
  "configuration": "landscape",
  "full_screen": "true"
};
// Creating a screen object.
AppMetricaECommerceScreen screen = AppMetricaECommerceScreen(
    name: "ProductCardActivity", // Optional.
    searchQuery: "danissimo maple syrup", // Optional.
    payload: payload, // Optional.
    categoriesPath: ["Promos", "Hot deal"] // Optional.
    );
AppMetricaECommerceAmount amount =
    AppMetricaECommerceAmount(amount: Decimal.parse('4.53'), currency: "USD");
// Creating an actualPrice object.
AppMetricaECommercePrice actualPrice =
    AppMetricaECommercePrice(fiat: amount, internalComponents: [
  // Optional.
  AppMetricaECommerceAmount(amount: Decimal.parse('30570000'), currency: "wood"),
  AppMetricaECommerceAmount(amount: Decimal.parse('26.89'), currency: "iron"),
  AppMetricaECommerceAmount(amount: Decimal.parse('5.1'), currency: "gold"),
]);
// Creating an originalPrice object.
AppMetricaECommercePrice originalPrice = AppMetricaECommercePrice(
    fiat: AppMetricaECommerceAmount(amount: Decimal.parse('5.78'), currency: "USD"),
    internalComponents: [
      // Optional.
      AppMetricaECommerceAmount(amount: Decimal.parse('30570000'), currency: "wood"),
      AppMetricaECommerceAmount(amount: Decimal.parse('26.89'), currency: "iron"),
      AppMetricaECommerceAmount(amount: Decimal.parse('5.1'), currency: "gold"),
    ]);
// Creating a product object.
AppMetricaECommerceProduct product = AppMetricaECommerceProduct(
    sku: "779213",
    name: "Danissimo curd product 5.9%, 130 g", // Optional.
    actualPrice: actualPrice, // Optional.
    originalPrice: originalPrice, // Optional.
    promocodes: ["BT79IYX", "UT5412EP"], // Optional.
    payload: payload, // Optional.
    categoriesPath: [
      "Groceries",
      "Dairy",
      "Yogurts"
    ] // Optional.
    );
AppMetricaECommerceReferrer referrer = AppMetricaECommerceReferrer(
    type: "button", // Optional.
    identifier: "76890", // Optional.
    screen: screen // Optional.
    );
// Creating a cartItem object.
AppMetricaECommerceCartItem addedItems1 = AppMetricaECommerceCartItem(
    product: product,
    revenue: actualPrice,
    quantity: Decimal.parse("1.0"),
    referrer: referrer // Optional.
    );
// Creating an order object.
AppMetricaECommerceOrder order = AppMetricaECommerceOrder(
    identifier: "88528768",
    items: [addedItems1],
    payload: payload // Optional.
    );
AppMetricaECommerceEvent beginCheckoutEvent = AppMetricaECommerce.beginCheckoutEvent(order);
// Sending an e-commerce event.
AppMetrica.getReporter("Testing API key")
    .reportECommerce(beginCheckoutEvent);
AppMetricaECommerceEvent purchaseEvent = AppMetricaECommerce.purchaseEvent(order);
// Sending an e-commerce event.
AppMetrica.getReporter("Testing API key").reportECommerce(purchaseEvent);
```

{% endcut %}

### Step 3. Check the test application's report {#send-ecommerce-check-reports}

Make in-app test purchases. After a while, check the E-commerce report in the AppMetrica interface. Make sure that the report shows e-commerce events. For more information about the report, see [E-commerce](../../../mobile-reports/ecommerce-report.md).

### Step 4. Configure sending ECommerce to the main API Key {#send-ecommerce-key}

After successful testing, configure sending E-commerce events to the main API key.

To send the `AppMetricaECommerceEvent` object to the main API key, use the `AppMetrica.reportECommerce(AppMetricaECommerceEvent event)` method:

```dart translate=no
...
// Sending an E-commerce event.
AppMetrica.reportECommerce(ecommerceEvent);
```

## Sending in-app purchases {#send-revenue}

{% cut "With validation" %}

To validate purchases on Android, configure sending the `Revenue.Receipt` instance along with Revenue. For iOS, configure sending the `transactionID` field.

1. Create an `AppMetricaReceipt` instance with information about the purchase and signature.
2. Create an `AppMetricaRevenue` instance and pass the `AppMetricaReceipt` and `transactionID` to it.
3. Send the `AppMetricaRevenue` instance using the `AppMetrica.reportRevenue(AppMetricaRevenue revenue)` method.

```java translate=no
AppMetricaReceipt receipt = AppMetricaReceipt(
	data: billingClientPurchase.originalJson,
	signature: billingClientPurchase.signature);
AppMetricaRevenue revenue = AppMetricaRevenue(
	Decimal.parse("100.100"),
	"USD",
	quantity: 2,
	productId: "com.yandex.service.299",
	payload: "{\"source\":\"Google Play\"}",
	receipt: receipt,
	transactionId: transactionIdentifier);
AppMetrica.reportRevenue(revenue);
```

{% endcut %}

{% cut "Without validation" %}

1. Create an `AppMetricaRevenue` instance.

2. (Optional) To group purchases by `OrderID`, pass it to the `payload` property.

{% note info "Note" %}

If the `OrderID` is not specified, AppMetrica generates the ID automatically.

{% endnote %}

3. Send the `AppMetricaRevenue` instance using the `AppMetrica.reportRevenue(AppMetricaRevenue revenue)` method.

```java translate=no
AppMetricaRevenue revenue = AppMetricaRevenue(Decimal.parse("100.100"), "USD",
	quantity: 2,
	productId: "com.yandex.service.299",
	payload: """{"OrderID":"Identifier", "source":"Google Play"}""");
AppMetrica.reportRevenue(revenue);
```

{% endcut %}

## Sending Ad Revenue {#send-adrevenue}

You can transmit ad revenue info to AppMetrica.

### Step 1. Make sure that the SDK is activated {#send-adrevenue-active}

Activation example:

```dart translate=no
AppMetricaConfig config = AppMetricaConfig("API_KEY");
AppMetrica.activate(config);
```

### Step 2. Set up sending ad revenue data {#send-adrevenue-send}

1. Create an `AppMetricaAdRevenue` class object.

   ```dart translate=no
    Map<String, String> adRevenuePayload = {
      "payload_key_1": "payload_value_1",
      "payload_key_2": "payload_value_2"
    };

    AppMetricaAdRevenue adRevenue = AppMetricaAdRevenue(
        adRevenue: Decimal.parse("100.100"),
        currency: "USD",
        adNetwork: "ad_network", // Optional
        adPlacementId: "ad_placement_id", // Optional
        adPlacementName: "ad_placement_name", // Optional
        adType: AdType.NATIVE, // Optional
        adUnitId: "ad_unit_id", // Optional
        adUnitName: "ad_unit_name", // Optional
        precision: "some precision", // Optional
        payload: adRevenuePayload // Optional
        );
   ```

2. Send the `AppMetricaAdRevenue` instance using the `reportAdRevenue(AppMetricaAdRevenue adRevenue)` method.

   ```dart translate=no
   AppMetrica.reportAdRevenue(adRevenue);
   ```

### Step 3. Make sure that the ad revenue data is included in the reports {#send-adrevenue-check-reports}

1. View ads in the app.

2. Make sure the [In-app and Ad Revenue](../../../mobile-reports/revenue-report.md) report shows the same number of ad revenue events as the number of ad views.

## Tracking app opens using deeplinks {#deeplink}

Use the `reportAppOpen(String deeplink)` method to track app launches:

```dart translate=no
AppMetrica.reportAppOpen(deeplink);
```

## Setting the session timeout duration {#session-timeout}

By default, the session timeout is 10 seconds. The minimum acceptable value for the `sessionTimeout` parameter is 10 seconds.

To change the timeout duration, pass the value in seconds to the `sessionTimeout` property when creating the extended library configuration.

```dart translate=no
AppMetrica.activate(
    AppMetricaConfig(API_KEY, sessionTimeout: 15));
```

## Setting the app version {#version-app}

To specify the app version manually in your code, pass it to the `appVersion` property when creating the extended library configuration.

```dart translate=no
AppMetrica.activate(
    AppMetricaConfig(API_KEY, appVersion: "1.13.2"));
```

where `1.13.2` is the app version.


## Determining the library's API level (Android) {#level-api-android}

To determine the API level of the library from the app code, use the `libraryApiLevel` property.

```dart translate=no
int apiLevel;
AppMetrica.libraryApiLevel.then((value) => {apiLevel = value});
```

## Determining the library's version {#version-sdk}

To determine the library version from the application code, use the `AppMetrica.GetLibraryVersion()` method.

```dart translate=no
String version;
AppMetrica.libraryVersion.then((value) => {version = value});
```

## Requesting a deferred deeplink {#deferreddeeplink-request}

To request a deferred deeplink, call the `AppMetrica.requestDeferredDeeplink()` method. You can only request a deferred deeplink at the first app launch after obtaining your Google Play Install Referrer.

```dart translate=no
AppMetrica.requestDeferredDeeplink()
    .then((value) => {
          // Processing deferred deeplink.
        })
    .onError((error, stackTrace) => {
          // Handling the error.
        });
```

For more information about deferred deeplinks, see [{#T}](../../android/analytics/android-deferred-deeplinks.md).

## Requesting deferred deeplink parameters {#deferreddeeplink-parameters-request}

To request parameters for a deferred deeplink, call the `AppMetrica.requestDeferredDeeplinkParameters()` method. You can only request deferred deeplink parameters at the first app launch after obtaining your Google Play Install Referrer.

```dart translate=no
AppMetrica.requestDeferredDeeplinkParameters()
    .then((value) => {
          // Processing deeplink parameters.
        })
    .onError((error, stackTrace) => {
          // Handling the error.
        });
```

For more information about deferred deeplinks, see [{#T}](../../android/analytics/android-deferred-deeplinks.md).

## Tracking new users {#new-user}

By default, the user is counted as a new user when the app is opened for the first time. If you connect the AppMetrica SDK to an app that already has active users, you can set up tracking new and old users to get correct statistics. Configure that by initializing the AppMetrica SDK using the extended `AppMetricaConfig` configuration:

```dart translate=no
bool isFirstLaunch = false;
// Implement logic to detect whether the app is opening for the first time.
// For example, you can check for files (settings, databases, and so on),
// which the app creates on its first launch.
if (conditions) {
  isFirstLaunch = true;
}
// Activating SDK with extended library configuration.
AppMetrica.activate(
    AppMetricaConfig(API_KEY, firstActivationAsUpdate: !isFirstLaunch));
```

## Disabling and enabling sending statistics {#stat}

If you need confirmation from the user before sending statistical data, you should initialize the library with the disabled sending option. To do this, pass the `false` value to the `dataSendingEnabled` property when creating the extended library configuration.

```dart translate=no
AppMetrica.activate(
    AppMetricaConfig(API_KEY, dataSendingEnabled: false));
```

After the user consents to sending their statistics (for example, in the app settings or by accepting the agreement when launching the app for the first time), enable statistics sending using the `AppMetrica.setDataSendingEnabled(bool enabled)` method:

```dart translate=no
// Checking the status of the boolean variable. It shows the user confirmation.
if (flag) {
  // Enabling sending data.
  AppMetrica.setDataSendingEnabled(true);
}
```

### Alert example {#stat-example}

You can use any text to inform users of statistics collection. For example:

This app uses the AppMetrica analytical service provided by YANDEX LLC, ulitsa Lva Tolstogo 16, Moscow, Russia 119021 (hereinafter referred to as Yandex) based on the [Terms of Use](https://yandex.ru/legal/metrica_termsofuse/?lang={{locale}}).

AppMetrica analyzes app usage data, including the device it is running on, the installation source, calculates conversion, collects statistics of your activity for product analytics, ad campaign analysis, and optimization, as well as for troubleshooting. Information collected in this way cannot identify you.

Depersonalized information about your use of this app collected by AppMetrica tools will be transferred to Yandex and stored on Yandex’s server in the EU and the Russian Federation. Yandex will process this information to provide you with app usage statistics, generate app performance reports, and deliver other services.


## Getting AppMetrica SDK IDs {#get-ids}

To get AppMetrica SDK IDs (`DeviceId`, `DeviceIdHash`, `UUID`), use the `requestStartupParams()` method. To get the `appmetrica_device_id`, make sure to request the `DeviceIdHash`.

```dart translate=no
Future<AppMetricaStartupParams> params = AppMetrica.requestStartupParams([
  AppMetricaStartupParams.deviceIdHashKey,
  AppMetricaStartupParams.deviceIdKey,
  AppMetricaStartupParams.uuidKey
]);
params.then((value) => {
      print(value.result?.deviceIdHash),
      print(value.result?.deviceId),
      print(value.result?.uuid)
    });
```

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
