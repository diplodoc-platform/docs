# Usage examples

## Library initialization with the extended configuration {#initialize}

To initialize the library with an extended startup configuration, create an instance of the `AppMetricaConfig` class with appropriate settings and activate the library using the `AppMetrica.Activate([NotNull] AppMetricaConfig config)` method. Using an extended configuration, you can enable or disable logging, set session timeout, pass parameters for [tracking pre-installed apps](../../../mobile-tracking/preinstalled-app-attr.md), and so on.

Extended configuration settings take effect immediately upon library initialization.

```csharp translate=no
AppMetrica.Activate(new AppMetricaConfig(API_KEY) {
    Logs = true,
});
```

To configure the library while the application is running, use the `AppMetrica` class methods.

## Sending statistics to an additional API key {#reporter-different-apikey}

Sending data to an additional API key allows you to collect own statistics for these API keys. You can use this to control access to information for other users. For example, to provide access to statistics for analysts you can duplicate sending marketing data for the additional API key. Thus they will only have access to the information they need.

To send data to an additional API key, you must use reporters. Just like for the main API key, you can set up an extended startup configuration for a reporter, send events, profile information, and data about in-app purchases. The reporter can work without the AppMetrica SDK initialization.

### Step 1. (Optional) Initialize a reporter with an extended configuration {#reporter-different-apikey-initialize}

To initialize a reporter with an extended configuration, create an instance of the `ReporterConfig` class with appropriate settings and activate the reporter using the `AppMetrica.ActivateReporter([NotNull] ReporterConfig config)` method. This configuration is used for a reporter with the specified API key. You can set up your own configuration for each additional API key.

{% note alert %}

The reporter with an extended configuration should be initialized before the first call to the reporter. Otherwise, the reporter will be initialized without a configuration.

{% endnote %}

```csharp translate=no
AppMetrica.ActivateReporter(new ReporterConfig(ANOTHER_API_KEY) {
    Logs = true,
});
```

### Step 2. Configure sending data using a reporter {#reporter-different-apikey-send}

To send data using a reporter, get an object that implements the `IReporter` interface with the `AppMetrica.GetReporter([NotNull] string apiKey)` method and use the interface methods for sending reports. If the reporter was not initialized with an extended configuration, calling this method will initialize the reporter for the specified API key.

Example of sending an event:

```csharp translate=no
AppMetrica.GetReporter(ANOTHER_API_KEY).ReportEvent("Updates installed");
```

For correct tracking, manually configure the reporters to send events about the start and the pause of the session for each reporter. To do this, use the `ResumeSession()` and `PauseSession()` methods of the `IReporter` interface:

```csharp translate=no
AppMetrica.GetReporter(ANOTHER_API_KEY).ResumeSession();

AppMetrica.GetReporter(ANOTHER_API_KEY).PauseSession();
```

## Tracking app crashes {#set-report-crash}

Reports on app crashes are sent by default.

To disable automatic monitoring, initialize the library with the configuration in which sending crashes is disabled. To do this, pass `false` to the `CrashReporting` property when creating an extended library configuration.

```csharp translate=no
AppMetrica.Activate(new AppMetricaConfig(API_KEY) {
    CrashReporting = false,
});
```

If automatic monitoring is disabled, you can manually [submit information about crashes](#report-unhandled).

## Manually monitoring app crashes {#report-unhandled}

Reports on app crashes are sent by default. To prevent event duplication when sending crashes manually, disable the [automatic monitoring of app crashes](#set-report-crash).

To send crash data manually, use the `AppMetrica.ReportUnhandledException([NotNull] Exception exception)` method:

```csharp translate=no
try
{
    ...
}
catch (Exception ex)
{
    AppMetrica.ReportUnhandledException(ex);
}
```

## Using the library to send device location {#track-location}

{% note info %}

Sending device location is disabled by default.

{% endnote %}

To enable sending it, initialize the library with the configuration where sending device location data is enabled. To do this, pass `true` to the `LocationTracking` property when creating an extended library configuration.

```csharp translate=no
AppMetrica.Activate(new AppMetricaConfig(API_KEY) {
    LocationTracking = true,
});
```

To enable sending at app runtime, use the `AppMetrica.SetLocationTracking(bool enabled)` method:

```csharp translate=no
AppMetrica.SetLocationTracking(true);
```

For more precise locations, add one of the following permissions to the AndroidManifest.xml file:

- [android.permission.ACCESS_COARSE_LOCATION](https://developer.android.com/reference/android/Manifest.permission.html#ACCESS_COARSE_LOCATION) — For approximate determination.
- [android.permission.ACCESS_FINE_LOCATION](https://developer.android.com/reference/android/Manifest.permission.html#ACCESS_FINE_LOCATION) — For accurate determination.

## Setting location manually {#location-manual}

Before sending your own data about the device location, make sure that report sending is [enabled](#track-location).

The library determines the device location on its own. To send your own data about the device location, pass an instance of the `Location` class to the `AppMetrica.SetLocation([CanBeNull] Location? location)` method:

```csharp translate=no
AppMetrica.SetLocation(new Location {
    Latitude = ... ,
    Longitude = ... ,
});
```

To send your own data about the device location using the startup configuration, pass an instance of the `Location` class to the `Location` property when creating an extended library configuration.

```csharp translate=no
AppMetrica.Activate(new AppMetricaConfig(API_KEY) {
    Location = new Location {
        Latitude = ... ,
        Longitude = ... ,
    },
});
```

To resume detecting the location with the library, call the `AppMetrica.SetLocation([CanBeNull] Location? location)` method with a `null` and configure the [sending of device location data](#track-location).

```csharp translate=no
AppMetrica.SetLocation(null);
```

## Sending a custom event {#report-event}

To send a custom event without nested parameters, pass a short name or description of the event to the `AppMetrica.ReportEvent([NotNull] string eventName)` method:

```csharp translate=no
AppMetrica.ReportEvent("Updates installed");
```

## Sending a custom event with nested parameters {#report-event-params}

With the AppMetrica SDK, you can send custom events with nested parameters in JSON string format.

To pass nested event parameters in JSON format, use the `AppMetrica.ReportEvent([NotNull] string eventName, [CanBeNull] string jsonValue)` method:

```csharp translate=no
string eventParameters = "{\"name\":\"Alice\", \"age\":\"18\"}";
AppMetrica.ReportEvent("New person", eventParameters);
```

The AppMetrica web interface displays up to five nesting levels for events. So if an event has six or more levels, only the top five are shown in the report. You can use the [Reporting API](../../../mobile-api/api_v1/intro.md) to export up to ten levels.

For more information about events, see [Events](../../../data-collection/about-events.md).

## Sending a custom error message {#send-report-error}

To send your own error message, use the following methods:

```csharp translate=no
AppMetrica.ReportError([NotNull] string message, [NotNull] Exception error);
AppMetrica.ReportError([NotNull] string identifier, [CanBeNull] string message = null, [CanBeNull] Exception error = null);
```

{% cut "Example with groupIdentifier" %}

If you send errors using methods with groupIdentifier, they are grouped by ID.

```csharp translate=no
try
{
    ...
}
catch (Exception ex)
{
    AppMetrica.ReportError("Your ID", "Error while parsing some integer number", ex);
}
```

Don't use variable values as grouping IDs. Otherwise, the number of groups increases, and it becomes difficult to analyze them.

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/id-group-android.png){style="border: solid 1px #cccccc;"}

{% endcut %}

{% cut "Example with message" %}

If errors are sent using the `AppMetrica.ReportError([NotNull] string message, [NotNull] Exception error)` method, they are grouped by [stack trace](https://en.wikipedia.org/wiki/Stack_trace).

```csharp translate=no
try
{
    ...
}
catch (Exception ex)
{
    AppMetrica.ReportError("Error while parsing some integer number", ex);
}
```

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/msg-group-android.png){style="border: solid 1px #cccccc;"}

{% endcut %}

## Sending events from the buffer {#send-events-buffer}

AppMetrica SDK does not send an event immediately after it occurred. The library stores event data in the buffer. The `SendEventsBuffer` method initiates sending data from the buffer and flushes it. Use the method to force sending stored events after passing important checkpoints of user scenarios.

```csharp translate=no
AppMetrica.SendEventsBuffer();
```

{% note alert "" %}

If you use this method frequently, this may result in increased internet traffic and energy consumption.

{% endnote %}

## Monitoring the app lifecycle manually {#listen}

AppMetrica tracks session boundaries automatically. If needed, you can disable automatic session tracking by passing `false` to the `SessionsAutoTrackingEnabled` property in the extended library configuration.

```csharp translate=no
AppMetrica.Activate(new AppMetricaConfig(API_KEY) {
    SessionsAutoTrackingEnabled = false,
});
```

To monitor the app lifecycle manually, use the following methods:

- Pause session:

    ```csharp translate=no
    AppMetrica.PauseSession();
    ```

- Resume session or start a new one:

    ```csharp translate=no
    AppMetrica.ResumeSession();
    ```

## Sending ProfileId {#send-profile-id}

If you know the user profile ID before initializing the AppMetrica SDK, pass it before initialization (`SetUserProfileID`) or during initialization with an extended configuration (`UserProfileID`).

Otherwise, a user profile is created with the ID `appmetrica_device_id`.

{% note warning "" %}

AppMetrica doesn't display `predefined attributes` in the web interface if [ProfieId](../../../data-collection/profile-attributes.md#pre-defined) sending isn't configured.

{% endnote %}

You can update `ProfileId` at any time by calling `setUserProfileID`:

```csharp translate=no
AppMetrica.SetUserProfileID("id");
```

## Sending profile attributes {#send-attribute-profile}

To send profile attributes, pass the necessary attributes to an instance of the `UserProfile` class and send this instance using the `AppMetrica.ReportUserProfile([NotNull] UserProfile profile)` method. To create profile attributes, use methods of the `Attribute` class.

```csharp translate=no
using Io.AppMetrica;
using Io.AppMetrica.Profile;

...

// Creating the UserProfile instance.
UserProfile userProfile = new UserProfile()

    // Updating predefined attributes.
    .Apply(Attribute.Name().WithValue("John"))
    .Apply(Attribute.Gender().WithValue(GenderAttribute.Gender.Male))
    .Apply(Attribute.BirthDate().WithAge(24))
    .Apply(Attribute.NotificationsEnabled().WithValue(false))

    // Updating custom attributes.
    .Apply(Attribute.CustomString("string_attribute").WithValue("string"))
    .Apply(Attribute.CustomBoolean("boolean_attribute").WithValue(true))
    .Apply(Attribute.CustomNumber("number_attribute").WithValue(55))
    .Apply(Attribute.CustomCounter("counter_attribute").WithDelta(1));

// Setting the ProfileID using the method of the AppMetrica class.
AppMetrica.SetUserProfileID("id");

// Sending the UserProfile instance.
AppMetrica.ReportUserProfile(userProfile);
```

## Sending E-commerce events {#send-ecommerce}

AppMetrica doesn't let you segment E-commerce events into test and non-test events. If you use the main API key for debugging purchases, the test events are included in general statistics. Therefore, to debug E-commerce event sending, use a reporter to send statistics to the additional API key.

### Step 1. Configure sending E-commerce events to the test API key {#send-ecommerce-test-key}

For different user actions, there are appropriate types of e-commerce events. To create a specific event type, use the appropriate `ECommerceEvent` class method.

The examples below show how to send specific types of events:

{% cut "Opening a page" %}

  ```csharp translate=no
  using Io.AppMetrica;
  using Io.AppMetrica.Ecommerce;

  ...

  IDictionary<string, string> payload = new Dictionary<string, string>();
  payload.Add("configuration", "landscape");
  payload.Add("full_screen", "true");
  // Creating a screen object.
  ECommerceScreen screen = new ECommerceScreen();
  screen.Name = "ProductCardActivity";
  screen.CategoriesPath = new string[] { "Promos", "Hot Deal" };
  screen.SearchQuery = "danissimo maple syrup";
  screen.Payload = payload;

  ECommerceEvent showScreenEvent = ECommerceEvent.ShowScreenEvent(screen);
  // Sending an E-commerce event.
  AppMetrica.GetReporter("Testing API key").ReportECommerce(showScreenEvent);
  ```

{% endcut %}

{% cut "Viewing a product card" %}

  ```csharp translate=no
  using Io.AppMetrica;
  using Io.AppMetrica.Ecommerce;

  ...

  IDictionary<string, string> payload = new Dictionary<string, string>();
  payload.Add("configuration", "landscape");
  payload.Add("full_screen", "true");
  // Creating a screen object.
  ECommerceScreen screen = new ECommerceScreen();
  screen.Name = "ProductCardActivity";
  screen.CategoriesPath = new string[] { "Promos", "Hot Deal" };
  screen.SearchQuery = "danissimo maple syrup";
  screen.Payload = payload;
  // Creating an actualPrice object.
  ECommercePrice actualPrice = new ECommercePrice(new ECommerceAmount(4.53, "USD"));
  actualPrice.InternalComponents = new ECommerceAmount[] { // Optional.
      new ECommerceAmount(30_570_000, "wood"),
      new ECommerceAmount(26.89, "iron"),
      new ECommerceAmount(new decimal(5.1), "gold")
  };
  // Creating an originalPrice object.
  ECommercePrice originalPrice = new ECommercePrice(new ECommerceAmount(5.78, "USD"));
  originalPrice.InternalComponents = new ECommerceAmount[] { // Optional.
      new ECommerceAmount(30_590_000, "wood"),
      new ECommerceAmount(26.92, "iron"),
      new ECommerceAmount(new decimal(5.5), "gold")
  };
  // Creating a product object.
  ECommerceProduct product = new ECommerceProduct("779213");
  product.ActualPrice = actualPrice; // Optional.
  product.Promocodes = new string[] { "BT79IYX", "UT5412EP" }; // Optional.
  product.Payload = payload; // Optional.
  product.OriginalPrice = originalPrice; // Optional.
  product.Name = "Danissimo curd product 5.9%, 130 g"; // Optional.
  product.CategoriesPath = new string[] { "Groceries", "Dairy", "Yogurts" }; // Optional.
  ECommerceEvent showProductCardEvent = ECommerceEvent.ShowProductCardEvent(product, screen);
  // Sending an E-commerce event.
  AppMetrica.GetReporter("Testing API key").ReportECommerce(showProductCardEvent);
  ```

{% endcut %}

{% cut "Viewing a product page" %}

  ```csharp translate=no
  using Io.AppMetrica;
  using Io.AppMetrica.Ecommerce;

  ...

  IDictionary<string, string> payload = new Dictionary<string, string>();
  payload.Add("configuration", "landscape");
  payload.Add("full_screen", "true");
  // Creating a screen object.
  ECommerceScreen screen = new ECommerceScreen();
  screen.Name = "ProductCardActivity";
  screen.CategoriesPath = new string[] { "Promos", "Hot Deal" };
  screen.SearchQuery = "danissimo maple syrup";
  screen.Payload = payload;
  // Creating an actualPrice object.
  ECommercePrice actualPrice = new ECommercePrice(new ECommerceAmount(4.53, "USD"));
  actualPrice.InternalComponents = new ECommerceAmount[] { // Optional.
      new ECommerceAmount(30_570_000, "wood"),
      new ECommerceAmount(26.89, "iron"),
      new ECommerceAmount(new decimal(5.1), "gold")
  };
  // Creating an originalPrice object.
  ECommercePrice originalPrice = new ECommercePrice(new ECommerceAmount(5.78, "USD"));
  originalPrice.InternalComponents = new ECommerceAmount[] { // Optional.
      new ECommerceAmount(30_590_000, "wood"),
      new ECommerceAmount(26.92, "iron"),
      new ECommerceAmount(new decimal(5.5), "gold")
  };
  // Creating a product object.
  ECommerceProduct product = new ECommerceProduct("779213");
  product.ActualPrice = actualPrice; // Optional.
  product.Promocodes = new string[] { "BT79IYX", "UT5412EP" }; // Optional.
  product.Payload = payload; // Optional.
  product.OriginalPrice = originalPrice; // Optional.
  product.Name = "Danissimo curd product 5.9%, 130 g"; // Optional.
  product.CategoriesPath = new string[] { "Groceries", "Dairy", "Yogurts" }; // Optional.
  ECommerceEvent showProductCardEvent = ECommerceEvent.ShowProductCardEvent(product, screen);
  // Sending an E-commerce event.
  AppMetrica.GetReporter("Testing API key").ReportECommerce(showProductCardEvent);
  ```

{% endcut %}

{% cut "Adding/removing an item to/from the cart" %}

  ```csharp translate=no
  using Io.AppMetrica;
  using Io.AppMetrica.Ecommerce;

  ...

  IDictionary<string, string> payload = new Dictionary<string, string>();
  payload.Add("configuration", "landscape");
  payload.Add("full_screen", "true");
  // Creating a screen object.
  ECommerceScreen screen = new ECommerceScreen();
  screen.Name = "ProductCardActivity";
  screen.CategoriesPath = new string[] { "Promos", "Hot Deal" };
  screen.SearchQuery = "danissimo maple syrup";
  screen.Payload = payload;
  // Creating an actualPrice object.
  ECommercePrice actualPrice = new ECommercePrice(new ECommerceAmount(4.53, "USD"));
  actualPrice.InternalComponents = new ECommerceAmount[] { // Optional.
      new ECommerceAmount(30_570_000, "wood"),
      new ECommerceAmount(26.89, "iron"),
      new ECommerceAmount(new decimal(5.1), "gold")
  };
  // Creating an originalPrice object.
  ECommercePrice originalPrice = new ECommercePrice(new ECommerceAmount(5.78, "USD"));
  originalPrice.InternalComponents = new ECommerceAmount[] { // Optional.
      new ECommerceAmount(30_590_000, "wood"),
      new ECommerceAmount(26.92, "iron"),
      new ECommerceAmount(new decimal(5.5), "gold")
  };
  // Creating a product object.
  ECommerceProduct product = new ECommerceProduct("779213");
  product.ActualPrice = actualPrice; // Optional.
  product.Promocodes = new string[] { "BT79IYX", "UT5412EP" }; // Optional.
  product.Payload = payload; // Optional.
  product.OriginalPrice = originalPrice; // Optional.
  product.Name = "Danissimo curd product 5.9%, 130 g"; // Optional.
  product.CategoriesPath = new string[] { "Groceries", "Dairy", "Yogurts" }; // Optional.
  // Creating a referrer object.
  ECommerceReferrer referrer = new ECommerceReferrer();
  referrer.Type = "button"; // Optional.
  referrer.Identifier = "76890"; // Optional.
  referrer.Screen = screen; // Optional.
  // Creating a cartItem object.
  ECommerceCartItem addedItems1 = new ECommerceCartItem(product, actualPrice, 1.0);
  addedItems1.Referrer = referrer; // Optional.
  ECommerceEvent addCartItemEvent = ECommerceEvent.AddCartItemEvent(addedItems1);
  // Sending an E-commerce event.
  AppMetrica.GetReporter("Testing API key").ReportECommerce(addCartItemEvent);
  ECommerceEvent removeCartItemEvent = ECommerceEvent.RemoveCartItemEvent(addedItems1);
  // Sending an E-commerce event.
  AppMetrica.GetReporter("Testing API key").ReportECommerce(removeCartItemEvent);
  ```

{% endcut %}

{% cut "Starting and completing a purchase" %}

  ```csharp translate=no
  using Io.AppMetrica;
  using Io.AppMetrica.Ecommerce;

  ...

  IDictionary<string, string> payload = new Dictionary<string, string>();
  payload.Add("configuration", "landscape");
  payload.Add("full_screen", "true");
  // Creating a screen object.
  ECommerceScreen screen = new ECommerceScreen();
  screen.Name = "ProductCardActivity";
  screen.CategoriesPath = new string[] { "Promos", "Hot Deal" };
  screen.SearchQuery = "danissimo maple syrup";
  screen.Payload = payload;
  // Creating an actualPrice object.
  ECommercePrice actualPrice = new ECommercePrice(new ECommerceAmount(4.53, "USD"));
  actualPrice.InternalComponents = new ECommerceAmount[] { // Optional.
      new ECommerceAmount(30_570_000, "wood"),
      new ECommerceAmount(26.89, "iron"),
      new ECommerceAmount(new decimal(5.1), "gold")
  };
  // Creating an originalPrice object.
  ECommercePrice originalPrice = new ECommercePrice(new ECommerceAmount(5.78, "USD"));
  originalPrice.InternalComponents = new ECommerceAmount[] { // Optional.
      new ECommerceAmount(30_590_000, "wood"),
      new ECommerceAmount(26.92, "iron"),
      new ECommerceAmount(new decimal(5.5), "gold")
  };
  // Creating a product object.
  ECommerceProduct product = new ECommerceProduct("779213");
  product.ActualPrice = actualPrice; // Optional.
  product.Promocodes = new string[] { "BT79IYX", "UT5412EP" }; // Optional.
  product.Payload = payload; // Optional.
  product.OriginalPrice = originalPrice; // Optional.
  product.Name = "Danissimo curd product 5.9%, 130 g"; // Optional.
  product.CategoriesPath = new string[] { "Groceries", "Dairy", "Yogurts" }; // Optional.
  // Creating a referrer object.
  ECommerceReferrer referrer = new ECommerceReferrer();
  referrer.Type = "button"; // Optional.
  referrer.Identifier = "76890"; // Optional.
  referrer.Screen = screen; // Optional.
  // Creating a cartItem object.
  ECommerceCartItem addedItems1 = new ECommerceCartItem(product, actualPrice, 1.0);
  addedItems1.Referrer = referrer; // Optional.
  // Creating an order object.
  ECommerceOrder order = new ECommerceOrder("88528768", new ECommerceCartItem[] { addedItems1 });
  order.Payload = payload; // Optional.
  ECommerceEvent beginCheckoutEvent = ECommerceEvent.BeginCheckoutEvent(order);
  // Sending an E-commerce event.
  AppMetrica.GetReporter("Testing API key").ReportECommerce(beginCheckoutEvent);
  ECommerceEvent purchaseEvent = ECommerceEvent.PurchaseEvent(order);
  // Sending an E-commerce event.
  AppMetrica.GetReporter("Testing API key").ReportECommerce(purchaseEvent);
  ```

{% endcut %}

### Step 2. Check the test application's report {#send-ecommerce-test-app}

Make in-app test purchases. After a while, check the E-commerce report in the AppMetrica interface. Make sure that the report shows E-commerce events.

For more information about the report, see [E-commerce](../../../mobile-reports/ecommerce-report.md).

### Step 3. Configure sending events to the main API key {#send-ecommerce-key}

After successful testing, configure sending E-commerce events to the main API key.

To send the `ECommerceEvent` object to the main API key, use the `AppMetrica.ReportECommerce([NotNull] ECommerceEvent ecommerce)` method.

  ```csharp translate=no
  ...
  // Sending an E-commerce event.
  AppMetrica.ReportECommerce(ecommerceEvent)
  ```

## Sending Revenue {#send-revenue}

{% note info %}

Local validation with a public key is used to validate purchases on Android. To enable validation, create a public key and specify it in the settings.

{% endnote %}

### Step 1. Configure sending Revenue to the test API key {#send-revenue-test-key}

AppMetrica doesn't let you segment between test and non-test revenue. If you use the main API key for debugging purchases, the test purchases are included in general statistics. Therefore, to debug Revenue sending, use a reporter to send statistics to the additional API key.

This section outlines the steps for sending Revenue to the additional API key:

{% cut "With validation" %}

To validate purchases, configure sending a `Revenue.Receipt` instance along with `Revenue`:

1. Create a `Revenue.Receipt` instance with information about the purchase and signature. Use it in the `Revenue.Receipt` property when creating an instance of `Revenue`.
2. Create a `Revenue` instance.
3. Send the `Revenue` instance to the test API key using the `IReporter`. For more information about reporters, see [Sending statistics to an additional API key](#reporter-different-apikey).

The example below is based on the use of [Unity IAP](https://docs.unity3d.com/Manual/UnityIAP.html).

```csharp translate=no
using Io.AppMetrica;

...

// Declaration of the Receipt structure for getting information about the IAP.
[System.Serializable]
public struct Receipt {
    public string Store;
    public string TransactionID;
    public string Payload;
}

// Additional information about the IAP for Android.
[System.Serializable]
public struct PayloadAndroid {
    public string Json;
    public string Signature;
}

public PurchaseProcessingResult ProcessPurchase(PurchaseEventArgs args) {
    var product = args.purchasedProduct;
    if (String.Equals(product.definition.id, kProductIDConsumable, StringComparison.Ordinal)) {
        string currency = product.metadata.isoCurrencyCode;
        decimal price = product.metadata.localizedPrice;

        // Creating an instance of the Revenue class.
        Revenue revenue = new Revenue(price, currency);
        if (product.receipt != null) {
            // Creating an instance of the Revenue.Receipt class.
            Revenue.Receipt yaReceipt = new Revenue.Receipt();
            Receipt receipt = JsonUtility.FromJson<Receipt>(product.receipt);
        #if UNITY_ANDROID
            PayloadAndroid payloadAndroid = JsonUtility.FromJson<PayloadAndroid>(receipt.Payload);
            yaReceipt.Signature = payloadAndroid.Signature;
            yaReceipt.Data = payloadAndroid.Json;
        #elif UNITY_IPHONE
            yaReceipt.TransactionID = receipt.TransactionID;
            yaReceipt.Data = receipt.Payload;
        #endif
            revenue.ReceiptValue = yaReceipt;
        }
        // Sending data to the AppMetrica server.
        AppMetrica.GetReporter("Testing API key").ReportRevenue(revenue);
    }
    return PurchaseProcessingResult.Complete;
}
```

{% endcut %}

{% cut "Without validation" %}

To send information about a purchase without validation:

1. Create a `Revenue` instance.
2. (Optional) To group purchases by `OrderID`, specify it in the `Revenue.Payload` property.

   {% note info %}

   If the `OrderID` is not specified, AppMetrica generates the ID automatically.

   {% endnote %}

3. Send the `Revenue` instance to the test API key using the `IReporter`. For more information about reporters, see [Sending statistics to an additional API key](#reporter-different-apikey).

```csharp translate=no
using Io.AppMetrica;

...

public PurchaseProcessingResult ProcessPurchase(PurchaseEventArgs args) {
    var product = args.purchasedProduct;
    if (String.Equals(product.definition.id, kProductIDConsumable, StringComparison.Ordinal)) {
        string currency = product.metadata.isoCurrencyCode;
        decimal price = product.metadata.localizedPrice;

        // Creating an instance of the Revenue class.
        Revenue revenue = new Revenue(price, currency);
        revenue.Payload = "{\"OrderID\":\"Identifier\", \"source\":\"Google Play\"}";
        revenue.Quantity = 2;
        // Sending data to the AppMetrica server.
        AppMetrica.GetReporter("Testing API key").ReportRevenue(revenue);
    }
    return PurchaseProcessingResult.Complete;
}
```

{% endcut %}

### Step 2. Check the test application's report {#send-revenue-test-app}

Check the Revenue report in the AppMetrica report. Make sure that the number of purchases has increased.

For more information about the report, see [In-app and Ad Revenue](../../../mobile-reports/revenue-report.md).

### Step 3. Configure sending Revenue to the main API key {#send-revenue-key}

After successful testing, have `Revenue` sent to the main API key.

To send the `Revenue` instance to the main API key, use the `AppMetrica.ReportRevenue([NotNull] Revenue revenue)` method.

```csharp translate=no
...
// Sending the Revenue instance.
AppMetrica.ReportRevenue(revenue);
```

## Sending AdRevenue {#send-adrevenue}

Use this option to manually set up the transfer of data from an ad monetization service that provides impression-level revenue data.

Create a `PluginErrorDetails` instance.

```csharp translate=no
IDictionary<string, string> payload = new Dictionary<string, string>();
payload.Add("payload_key_1", "payload_value_1");
payload.Add("payload_key_2", "payload_value_2");
AdRevenue adRevenue = new AdRevenue(100.100, "USD");
adRevenue.AdNetwork = "ad_network";
adRevenue.AdPlacementId = "ad_placement_id";
adRevenue.AdPlacementName = "ad_placement_name";
adRevenue.AdType = AdType.Banner;
adRevenue.AdUnitId = "ad_unit_id";
adRevenue.AdUnitName = "ad_unit_name";
adRevenue.Precision = "some_precision";
adRevenue.Payload = payload;
```

Send the `AdRevenue` instance using the `AppMetrica.ReportAdRevenue([NotNull] AdRevenue adRevenue)` method.

```csharp translate=no
AppMetrica.ReportAdRevenue(adRevenue);
```

## Automatic collection of AdRevenue data {#adrevenue-autocollection}

AppMetrica supports automatic collection of ad monetization data for certain advertising services.
When using Unity library version 6.5.0 or higher, automatic data collection is enabled for AppLovin, ironSource, and TopOn by default. For Fyber (Digital Turbine), you need to enable data collection manually.

When activating collection for Fyber (Digital Turbine), make sure that you aren't using the following methods:

```csharp translate=no
Banner.SetBannerListener();
Interstitial.SetInterstitialListener();
Rewarded.SetRewardedListener();
```

Automatic collection may not work if you're using any of the methods listed above.

To disable automatic data collection, go to **Assets** → **AppMetrica** → **Settings** and select the desired advertising service.

To disable automatic detection of connected advertising services, turn off the **Enable Auto Detection Of Features** option.

{% cut "Settings" %}

![](../../../../_images/adrevenue-unity-settings.png){style="border: solid 1px #cccccc; max-width: 350px;"}

{% endcut %}

## Setting the session timeout duration {#session-timeout}

By default, the session timeout is 10 seconds. This is the minimum acceptable value of the `SessionTimeout` parameter.

To change the timeout duration, pass the value in seconds to the `SessionTimeout` property when creating an extended library configuration.

```csharp translate=no
AppMetrica.Activate(new AppMetricaConfig(API_KEY) {
    SessionTimeout = 15,
});
```

## Setting the app version {#version-app}

By default, the app version is set in the file [build.gradle](https://developer.android.com/studio/publish/versioning).

To specify the app version programmatically, pass the app version to the `AppVersion` property when creating an extended library configuration.

```csharp translate=no
AppMetrica.Activate(new AppMetricaConfig(API_KEY) {
    AppVersion = "1.13.2",
});
```

where `1.13.2` is the app version.

## Determining the library's version {#version-sdk}

To determine the library version from the application code, use the `AppMetrica.GetLibraryVersion()` method.

```csharp translate=no
string libraryVersion = AppMetrica.GetLibraryVersion();
```

## Tracking installation sources {#source}

Tracking installation source in AppMetrica SDK is enabled by default.

## Tracking app opens using deeplinks {#deeplink}

{% note tip %}

To work with deeplinks, support them in your application: [Android](https://developer.android.com/training/app-links/deep-linking#adding-filters), [iOS](https://developer.apple.com/documentation/xcode/allowing-apps-and-websites-to-link-to-your-content).

{% endnote %}

Starting with version 4.0 of the iOS/Android SDK, deeplink tracking works automatically when the app is opened. For more information, see [Deeplink tracking](../../../data-collection/deeplinks.md).

If you need to track app launches manually, use the `ReportAppOpen([NotNull] string deeplink)` method:

```csharp translate=no
AppMetrica.ReportAppOpen(deeplink);
```

{% note info %}

You can add the opening of the app via the [deferred deeplink](../../android/analytics/android-deferred-deeplinks.md) on Android.

{% endnote %}

For more information, see [How do I create a remarketing campaign in AppMetrica?](../../../troubleshooting/troubleshooting.md#remarketing-campaign)

## Requesting a deferred deeplink {#deferreddeeplink-request}

To request a deferred deeplink, pass an implementation of the `DeferredDeeplink.DeeplinkDelegate` and `DeferredDeeplink.ErrorDelegate` delegates to the `AppMetrica.RequestDeferredDeeplink()` method. The method returns the deferred deeplink only at the initial application start after obtaining the Google Play Install Referrer.

```csharp translate=no
void DeeplinkDelegate(string deeplink)
{
    Debug.Log("deeplink: " + deeplink);
}

void ErrorDelegate(DeferredDeeplink.Error? error, string referrer)
{
    Debug.Log("error: " + error + " referrer: " + referrer);
}

...

AppMetrica.RequestDeferredDeeplink(DeeplinkDelegate, ErrorDelegate);
```

For more information about deferred deeplinks, see [Support for deferred deeplinks](../../android/analytics/android-deferred-deeplinks.md)

## Requesting deferred deeplink parameters {#deferreddeeplink-parameters-request}

To request parameters for a deferred deeplink, pass the methods implementing the `DeferredDeeplinkParameters.ParametersDelegate` and `DeferredDeeplinkParameters.ErrorDelegate` delegates to the `AppMetrica.RequestDeferredDeeplinkParameters()` method. The method returns the deferred deeplink parameters only at the first application start after Google Play Install Referrer obtaining.

```csharp translate=no
void DeeplinkParametersDelegate(IDictionary<string, string> parameters)
{
    foreach(KeyValuePair<string, string> pair in parameters)
    {
        Debug.Log("key: " + pair.Key + " Value: " + pair.Value);
    }
}

void ErrorParametersDelegate(DeferredDeeplinkParameters.Error? error, string referrer)
{
    Debug.Log("error: " + error + " referrer: " + referrer);
}

...

AppMetrica.RequestDeferredDeeplinkParameters(DeeplinkParametersDelegate, ErrorParametersDelegate);
```

For more information about deferred deeplinks, see [Support for deferred deeplinks](../../android/analytics/android-deferred-deeplinks.md)

## Tracking new users {#new-user}

By default, the user is counted as a new user when the app is opened for the first time. If you connect the AppMetrica SDK to an app that already has active users, you can set up tracking new and old users to get correct statistics. Configure that by initializing the AppMetrica SDK using the extended `AppMetricaConfig` configuration:

```csharp translate=no
using Io.AppMetrica;
using UnityEngine;

public static class AppMetricaActivator {
    [RuntimeInitializeOnLoadMethod(RuntimeInitializeLoadType.BeforeSceneLoad)]
    private static void Activate() {
        AppMetrica.Activate(new AppMetricaConfig("APIKey") {
            FirstActivationAsUpdate = !IsFirstLaunch(),
        });
    }

    private static bool IsFirstLaunch() {
        // Implement logic to detect whether the app is opening for the first time.
        // For example, you can check for files (settings, databases, and so on),
        // which the app creates on its first launch.
        return true;
    }
}
```

## Disabling and enabling sending statistics {#stat}

If you need confirmation from the user before sending statistical data, you should initialize the library with the disabled sending option. To do this, pass `false` to the `DataSendingEnabled` property when creating an extended library configuration.

```csharp translate=no
AppMetrica.Activate(new AppMetricaConfig(API_KEY) {
    DataSendingEnabled = false,
});
```

After the user has granted permission to send statistics (for example, in the app settings or by accepting the agreement when launching the app for the first time), enable the sending of statistics using the `AppMetrica.SetDataSendingEnabled(bool enabled)` method:

```csharp translate=no
// Checking the status of the boolean variable. It shows the user confirmation.
if (flag) {
    // Enabling sending data.
    AppMetrica.SetDataSendingEnabled(true);
}
```

### Alert example {#stat-alert-example}

You can use any text to inform users of statistics collection. For example:

> This app uses the AppMetrica analytical service provided by YANDEX LLC, ulitsa Lva Tolstogo 16, Moscow, Russia 119021 (hereinafter referred to as Yandex) based on the [Terms of Use](https://yandex.com/legal/metrica_termsofuse/).
>
> AppMetrica analyzes app usage data, including the device it is running on, the installation source, calculates conversion, collects statistics of your activity for product analytics, ad campaign analysis, and optimization, as well as for troubleshooting. Information collected in this way cannot identify you.
>
> Depersonalized information about your use of this app collected by AppMetrica tools will be transferred to Yandex and stored on Yandex’s server in the EU and the Russian Federation. Yandex will process this information to provide you with app usage statistics, generate app performance reports, and deliver other services.

## Getting AppMetrica SDK IDs {#get-ids}

To get AppMetrica SDK IDs (`DeviceId`, `DeviceIdHash`, `UUID`), use the `RequestStartupParams` method. To get the `appmetrica_device_id`, make sure to request the `DeviceIdHash`.

```csharp translate=no
void StartupParamsDelegateStartupParamsDelegate(StartupParamsResult result, StartupParamsErrorReason errorReason) {
    Debug.Log("Uuid: " + result.Uuid);
    Debug.Log("DeviceId: " + result.DeviceId);
    Debug.Log("DeviceIdHash: " + result.DeviceIdHash);
    Debug.Log("errorReason: " + errorReason);
}

...

IEnumerable<string> keys = new string[] { StartupParamsKey.AppMetricaUuid, StartupParamsKey.AppMetricaDeviceID, StartupParamsKey.AppMetricaDeviceIDHash };
AppMetrica.RequestStartupParams(StartupParamsDelegateStartupParamsDelegate, keys);
```

## Delivering the device type {#device-type}

If you want to set the device type, specify it when creating your configuration:

```csharp translate=no
AppMetrica.Activate(new AppMetricaConfig(API_KEY) {
    DeviceType = "TV",
});
```

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
    <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
