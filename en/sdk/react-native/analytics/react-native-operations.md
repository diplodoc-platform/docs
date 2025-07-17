# Usage examples

## Library initialization with the extended configuration {#initialize}

To initialize the library with the extended startup configuration, create an `AppMetricaConfig` instance with
appropriate settings and activate the library using the `AppMetrica.activate(config: AppMetricaConfig)` method. For example, you
can use the extended configuration to enable/disable logging, set session timeouts, pass
parameters for [tracking pre-installed apps](../../../mobile-tracking/preinstalled-app-attr.md), and more.

Extended configuration settings take effect immediately upon library initialization.

```javascript translate=no
import AppMetrica, {AppMetricaConfig} from '@appmetrica/react-native-analytics';
```

```javascript translate=no
const config: AppMetricaConfig = {
  apiKey: API_KEY,
  firstActivationAsUpdate: false,
  logs: true,
  sessionTimeout: 20,
}
AppMetrica.activate(config);
```

To configure the library while the app is running, use the `AppMetrica` class methods.

## Using the library to send device location {#track-location}

{% note info %}

Sending device location is disabled by default for Android.

{% endnote %}

To enable sending location data, initialize the library with the configuration where sending device
location data is enabled. To do this, set the `locationTracking` property to `true` when creating an extended library
configuration.

```javascript translate=no
import AppMetrica, {AppMetricaConfig} from '@appmetrica/react-native-analytics';
```

```javascript translate=no
const config: AppMetricaConfig = {
  apiKey: API_KEY,
  locationTracking: true,
}
AppMetrica.activate(config);
```

To enable sending location data while the app is running, use the
`AppMetrica.setLocationTracking(enabled: boolean)` method:

```javascript translate=no
AppMetrica.setLocationTracking(true);
```

For more precise locations, add one of the following permissions to the AndroidManifest.xml file:

- [android.permission.ACCESS_COARSE_LOCATION](https://developer.android.com/reference/android/Manifest.permission.html#ACCESS_COARSE_LOCATION) —
  to send an approximate location.
- [android.permission.ACCESS_FINE_LOCATION](https://developer.android.com/reference/android/Manifest.permission.html#ACCESS_FINE_LOCATION) —
  to send an accurate location.

## Setting location manually {#location-manual}

Before sending custom information about the device location, make sure that reporting is enabled.

The library determines the device location on its own. To send custom device location
data, pass `Location` to the `AppMetrica.setLocation(location?: Location)` method.

```javascript translate=no
import AppMetrica from '@appmetrica/react-native-analytics';
```

```javascript translate=no
// Determining the location.
const currentLocation: Location = {
  ...
}
// Setting up custom device location data.
AppMetrica.setLocation(currentLocation);
```

To send custom device location data using the extended configuration, pass the `Location` instance to the `location?: Location` property when creating an extended library configuration.

```javascript translate=no
import AppMetrica, {AppMetricaConfig, Location} from '@appmetrica/react-native-analytics';
```

```javascript translate=no
// Determining the location.
const currentLocation: Location = {
  ...
}
// Creating an extended library configuration.
const config: AppMetricaConfig = {
  apiKey: API_KEY,
  // Set up a custom device location.
  location: currentLocation,
}
// Initializing the AppMetrica SDK.
AppMetrica.activate(config);
```

To send custom device location data while the app is running, use the
`AppMetrica.setLocation(location?: Location)` method.

```javascript translate=no
AppMetrica.setLocation(currentLocation);
```

## Sending a custom event {#report-event}

To send a custom event with no nested parameters, pass a short name or description of the event to the `AppMetrica.reportEvent(eventName: string, attributes?: Record<string, any>)`
method:

```javascript translate=no
AppMetrica.reportEvent("Updates installed");
```

## Sending a custom event with nested parameters {#report-event-params}

With the AppMetrica SDK, you can send custom events with nested parameters
in JSON format. For this, use the `AppMetrica.reportEvent(eventName: string, attributes?: Record<string, any>)` method:

```javascript translate=no
AppMetrica.reportEvent('My event', {foo: 'bar'});
```

The AppMetrica web interface displays up to five nesting levels for events. So if an event has six or more levels, only the top five are shown in the
report. You can use the [Reporting API](../../../mobile-api/api_v1/intro.md) to export up to ten
levels.

For more information about events, see [Events](../../../data-collection/about-events.md).

## Sending a custom error message {#send-report-error}

To send a custom error message, use the
`AppMetrica.reportError(identifier: string, message: string)` method.

```javascript translate=no
try {
...
} catch (e: Error) {
  AppMetrica.reportError('my error', e.message);
}
```

Errors are grouped by ID. Don't use variable values as grouping IDs.
Otherwise, the number of groups increases and it becomes difficult to analyze them.

## Sending ProfileId {#send-profile-id}

If you know the user profile ID before initializing the AppMetrica SDK, pass it before initialization (`setUserProfileID`):

```javascript translate=no
AppMetrica.setUserProfileID('your-id');
AppMetrica.activate({apiKey: 'API_KEY'});
```

Or during initialization with an extended configuration (`userProfileID`):

```javascript translate=no
AppMetrica.activate({
    apiKey: 'API_KEY',
    userProfileID: 'your-id',
});
```

Otherwise, a user profile is created with the ID `appmetrica_device_id`.

{% note warning %}

AppMetrica doesn't display `predefined attributes` in the web interface if [ProfieId](../../../data-collection/profile-attributes.md#pre-defined) sending isn't configured.

{% endnote %}

You can update `ProfileId` at any time by calling `setUserProfileID`:


```javascript translate=no
AppMetrica.setUserProfileID('your-id');
```

## Sending profile attributes {#send-attribute-profile}

To send profile attributes, pass the required attributes to an instance of the `UserProfile` class and send the instance using the `AppMetrica.reportUserProfile(userProfile: UserProfile)` method. To create profile attributes, use methods of the `Attributes` class.

```javascript translate=no
import AppMetrica, {Attributes, UserProfile} from '@appmetrica/react-native-analytics';
```

```javascript translate=no
// Creating the UserProfile instance.
const userProfile = new UserProfile()
  // Updating predefined attributes.
  .apply(Attributes.userName().withValue('John'))
  .apply(Attributes.gender().withValue('male'))
  .apply(Attributes.birthDate().withAge(24))
  .apply(Attributes.notificationsEnabled().withValue(false))
  // Updating custom attributes.
  .apply(Attributes.customString('string_attribute').withValue('string'))
  .apply(Attributes.customNumber('number_attribute').withValue(55.0))
  .apply(Attributes.customCounter('counter_attribute').withDelta(1.0))
  .apply(Attributes.customBoolean('boolean_attribute').withValue(true));

// Setting the ProfileID using the method of the AppMetrica class.
AppMetrica.setUserProfileID('your-id');

// Sending the UserProfile instance.
AppMetrica.reportUserProfile(userProfile);
```

## Sending E-commerce events {#send-ecommerce}

For different user actions, there are appropriate types of e-commerce events. To create a specific event type,
use the appropriate `ECommerce` class method.

The examples below show how to send specific types of events:

{% cut "Opening a page" %}

```javascript translate=no
import AppMetrica, {
  ECommerce,
  ECommerceScreen,
} from '@appmetrica/react-native-analytics';
```

```javascript translate=no
const payload: Record<string, string> = {
  configuration: 'landscape',
  full_screen: 'true',
};
// Creating a screen object.
const screen: ECommerceScreen = {
  name: 'ProductCardActivity',               // Optional.
  searchQuery: 'danissimo maple syrup',  // Optional.
  payload: payload,                          // Optional.
  categoriesPath: ['Promos', 'Hot deal'], // Optional.
};
const showScreen = ECommerce.showScreenEvent(screen);
// Sending an e-commerce event.
AppMetrica.reportECommerce(showScreen);
```

{% endcut %}

{% cut "Viewing a product card" %}

```javascript translate=no
import AppMetrica, {
  ECommerce,
  ECommerceAmount,
  ECommercePrice,
  ECommerceProduct,
  ECommerceScreen,
} from '@appmetrica/react-native-analytics';
```

```javascript translate=no
const payload: Record<string, string> = {
  configuration: 'landscape',
  full_screen: 'true',
};
// Creating a screen object.
const screen: ECommerceScreen = {
  name: 'ProductCardActivity',               // Optional.
  searchQuery: 'danissimo maple syrup',  // Optional.
  payload: payload,                          // Optional.
  categoriesPath: ['Promos', 'Hot deal'], // Optional.
};
const amount: ECommerceAmount = {
  amount: 4.53,
  unit: 'USD',
};
// Creating an actualPrice object.
const actualPrice: ECommercePrice = {
  amount: amount,
  internalComponents: [  // Optional.
    {
      amount: 30570000,
      unit: 'wood',
    },
    {
      amount: 26.89,
      unit: 'iron',
    },
    {
      amount: 5.1,
      unit: 'gold',
    },
  ],
};
// Creating an originalPrice object.
const originalPrice: ECommercePrice = {
  amount: {amount: 5.78, unit: 'USD'},
  internalComponents: [  // Optional.
    {
      amount: 30570000,
      unit: 'wood',
    },
    {
      amount: 26.89,
      unit: 'iron',
    },
    {
      amount: 5.1,
      unit: 'gold',
    },
  ],
};
// Creating a product object.
const product: ECommerceProduct = {
  sku: '779213',
  name: 'Danissimo Сurd Dessert 5.9%, 130 g',  // Optional.
  actualPrice: actualPrice, // Optional.
  originalPrice: originalPrice, // Optional.
  promocodes: ['BT79IYX', 'UT5412EP'],  // Optional.
  payload: payload,    // Optional.
  categoriesPath: ['Groceries', 'Dairy', 'Yogurts']  // Optional.
};
// Sending an E-commerce event.
AppMetrica.reportECommerce(ECommerce.showProductCardEvent(product, screen));
```

{% endcut %}

{% cut "Viewing a product page" %}

```javascript translate=no
import AppMetrica, {
  ECommerce,
  ECommerceAmount,
  ECommercePrice,
  ECommerceProduct,
  ECommerceReferrer,
  ECommerceScreen,
} from '@appmetrica/react-native-analytics';
```

```javascript translate=no
const payload: Record<string, string> = {
  configuration: 'landscape',
  full_screen: 'true',
};
// Creating a screen object.
const screen: ECommerceScreen = {
  name: 'ProductCardActivity',               // Optional.
  searchQuery: 'danissimo maple syrup',  // Optional.
  payload: payload,                          // Optional.
  categoriesPath: ['Promos', 'Hot deal'], // Optional.
};

const amount: ECommerceAmount = {
  amount: 4.53,
  unit: 'USD',
};
// Creating an actualPrice object.
const actualPrice: ECommercePrice = {
  amount: amount,
  internalComponents: [  // Optional.
    {
      amount: 30570000,
      unit: 'wood',
    },
    {
      amount: 26.89,
      unit: 'iron',
    },
    {
      amount: 5.1,
      unit: 'gold',
    },
  ],
};
// Creating an originalPrice object.
const originalPrice: ECommercePrice = {
  amount: {amount: 5.78, unit: 'USD'},
  internalComponents: [  // Optional.
    {
      amount: 30570000,
      unit: 'wood',
    },
    {
      amount: 26.89,
      unit: 'iron',
    },
    {
      amount: 5.1,
      unit: 'gold',
    },
  ],
};
// Creating a product object.
const product: ECommerceProduct = {
  sku: '779213',
  name: 'Danissimo Сurd Dessert 5.9%, 130 g',  // Optional.
  actualPrice: actualPrice, // Optional.
  originalPrice: originalPrice, // Optional.
  promocodes: ['BT79IYX', 'UT5412EP'],  // Optional.
  payload: payload,    // Optional.
  categoriesPath: ['Groceries', 'Dairy', 'Yogurts']  // Optional.
};

const referrer: ECommerceReferrer = {
  type: 'button',
  identifier: '76890',
  screen: screen,
};

const showProductDetails = ECommerce.showProductDetailsEvent(product, referrer);
// Sending an E-commerce event.
AppMetrica.reportECommerce(showProductDetails);
```

{% endcut %}

{% cut "Adding/removing an item to/from the cart" %}

```javascript translate=no
import AppMetrica, {
  ECommerce,
  ECommerceAmount,
  ECommerceCartItem,
  ECommerceOrder,
  ECommercePrice,
  ECommerceProduct,
  ECommerceReferrer,
  ECommerceScreen,
} from '@appmetrica/react-native-analytics';
```

```javascript translate=no
const payload: Record<string, string> = {
  configuration: 'landscape',
  full_screen: 'true',
};
// Creating a screen object.
const screen: ECommerceScreen = {
  name: 'ProductCardActivity',               // Optional.
  searchQuery: 'danissimo maple syrup',  // Optional.
  payload: payload,                          // Optional.
  categoriesPath: ['Promos', 'Hot deal'], // Optional.
};

const amount: ECommerceAmount = {
  amount: 4.53,
  unit: 'USD',
};
// Creating an actualPrice object.
const actualPrice: ECommercePrice = {
  amount: amount,
  internalComponents: [  // Optional.
    {
      amount: 30570000,
      unit: 'wood',
    },
    {
      amount: 26.89,
      unit: 'iron',
    },
    {
      amount: 5.1,
      unit: 'gold',
    },
  ],
};
// Creating an originalPrice object.
const originalPrice: ECommercePrice = {
  amount: {amount: 5.78, unit: 'USD'},
  internalComponents: [  // Optional.
    {
      amount: 30570000,
      unit: 'wood',
    },
    {
      amount: 26.89,
      unit: 'iron',
    },
    {
      amount: 5.1,
      unit: 'gold',
    },
  ],
};
// Creating a product object.
const product: ECommerceProduct = {
  sku: '779213',
  name: 'Danissimo Сurd Dessert 5.9%, 130 g',  // Optional.
  actualPrice: actualPrice, // Optional.
  originalPrice: originalPrice, // Optional.
  promocodes: ['BT79IYX', 'UT5412EP'],  // Optional.
  payload: payload,    // Optional.
  categoriesPath: ['Groceries', 'Dairy', 'Yogurts']  // Optional.
};
// Creating a referrer object.
const referrer: ECommerceReferrer = {
  type: 'button', // Optional.
  identifier: '76890', // Optional.
  screen: screen, // Optional.
};
// Creating a cartItem object.
const ecommerceCartItem: ECommerceCartItem = {
  product: product,
  price: actualPrice,
  quantity: 1.0,
  referrer: referrer, // Optional.
};

const addCartItem = ECommerce.addCartItemEvent(ecommerceCartItem);
// Sending an E-commerce event.
AppMetrica.reportECommerce(addCartItem);

const removeCartItem = ECommerce.removeCartItemEvent(ecommerceCartItem);
// Sending an E-commerce event.
AppMetrica.reportECommerce(removeCartItem);
```

{% endcut %}

{% cut "Starting and completing a purchase" %}

```javascript translate=no
import AppMetrica, {
  ECommerce,
  ECommerceAmount,
  ECommerceCartItem,
  ECommerceOrder,
  ECommercePrice,
  ECommerceProduct,
  ECommerceReferrer,
  ECommerceScreen,
} from '@appmetrica/react-native-analytics';
```

```javascript translate=no
const payload: Record<string, string> = {
  configuration: 'landscape',
  full_screen: 'true',
};
// Creating a screen object.
const screen: ECommerceScreen = {
  name: 'ProductCardActivity',               // Optional.
  searchQuery: 'danissimo maple syrup',  // Optional.
  payload: payload,                          // Optional.
  categoriesPath: ['Promos', 'Hot deal'], // Optional.
};

const amount: ECommerceAmount = {
  amount: 4.53,
  unit: 'USD',
};
// Creating an actualPrice object.
const actualPrice: ECommercePrice = {
  amount: amount,
  internalComponents: [  // Optional.
    {
      amount: 30570000,
      unit: 'wood',
    },
    {
      amount: 26.89,
      unit: 'iron',
    },
    {
      amount: 5.1,
      unit: 'gold',
    },
  ],
};
// Creating an originalPrice object.
const originalPrice: ECommercePrice = {
  amount: {amount: 5.78, unit: 'USD'},
  internalComponents: [  // Optional.
    {
      amount: 30570000,
      unit: 'wood',
    },
    {
      amount: 26.89,
      unit: 'iron',
    },
    {
      amount: 5.1,
      unit: 'gold',
    },
  ],
};
// Creating a product object.
const product: ECommerceProduct = {
  sku: '779213',
  name: 'Danissimo Сurd Dessert 5.9%, 130 g',  // Optional.
  actualPrice: actualPrice, // Optional.
  originalPrice: originalPrice, // Optional.
  promocodes: ['BT79IYX', 'UT5412EP'],  // Optional.
  payload: payload,    // Optional.
  categoriesPath: ['Groceries', 'Dairy', 'Yogurts']  // Optional.
};
// Creating a referrer object.
const referrer: ECommerceReferrer = {
  type: 'button', // Optional.
  identifier: '76890', // Optional.
  screen: screen, // Optional.
};
// Creating a cartItem object.
const ecommerceCartItem: ECommerceCartItem = {
  product: product,
  price: actualPrice,
  quantity: 1.0,
  referrer: referrer, // Optional.
};

const order: ECommerceOrder = {
  orderId: '88528768',
  products: [ecommerceCartItem],
  payload: undefined,
};

const beginCheckout = ECommerce.beginCheckoutEvent(order);
// Sending an E-commerce event.
AppMetrica.reportECommerce(beginCheckout);

const purchase = ECommerce.purchaseEvent(order);
// Sending an E-commerce event.
AppMetrica.reportECommerce(purchase);
```

{% endcut %}

## Sending Revenue events {#send-revenue}

{% cut "With validation" %}

AppMetrica supports in-app purchase validation for purchases made through the [Google Play Billing](https://developer.android.com/google/play/billing/billing_overview) and [StoreKit](https://developer.apple.com/documentation/storekit) libraries.

To validate purchases, configure sending the `Receipt` instance along with `Revenue`:

- On Android, use `Receipt` to send [originalJson](https://developer.android.com/reference/com/android/billingclient/api/Purchase#getOriginalJson()) to `receiptData`, and to send [signature](https://developer.android.com/reference/com/android/billingclient/api/Purchase#getSignature()) to the `signature` property.

- On iOS, configure sending the `transactionID` and `receiptData` fields where you implement the transaction completion:

```javascript translate=no
import AppMetrica, {Revenue} from '@appmetrica/react-native-analytics';
```

```javascript translate=no
const revenue: Revenue = {
  price: 500,
  currency: 'USD',
  productID: '12345',
  quantity: 1,
  payload: JSON.stringify({test: 'test'}),
  receipt: {
    receiptData: purcahse.getOriginalJson(),
    signature: purcahse.getSignature(),
  },
};
AppMetrica.reportRevenue(revenue);
```

{% endcut %}

{% cut "Without validation" %}

```javascript translate=no
import AppMetrica, {Revenue} from '@appmetrica/react-native-analytics';
```

```javascript translate=no
const revenue: Revenue = {
  price: 500,
  currency: 'USD',
  productID: '12345',
  quantity: 1,
  payload: JSON.stringify({test: 'test'}),
};
AppMetrica.reportRevenue(revenue);
```

{% endcut %}

## Sending Ad Revenue events {#send-adrevenue}

```javascript translate=no
import AppMetrica, {
  AdRevenue,
  AdType
} from '@appmetrica/react-native-analytics';
```

Create an `AdRevenue` instance:

```javascript translate=no
const adRevenue: AdRevenue = {
  price: 0.1,
  currency: 'USD',
  payload: {payload_key_1: 'payload_value_1'},
  adNetwork: 'ad_network',
  adPlacementID: 'ad_placement_id',
  adPlacementName: 'ad_placement_name',
  adType: AdType.NATIVE,
  adUnitID: 'ad_unit_id',
  adUnitName: 'ad_unit_name',
  precision: 'some precision',
};
```

Send the `AdRevenue` instance using the `AppMetrica.reportAdRevenue(adRevenue: AdRevenue)` method:

```javascript translate=no
AppMetrica.reportAdRevenue(adRevenue);
```

## Setting the session timeout duration {#session-timeout}

By default, the session timeout is 10 seconds. This is the minimum allowed value for the
`sessionTimeout` property.

To change the timeout duration, pass the value in seconds to the `sessionTimeout` method when creating an extended
library configuration.

```javascript translate=no
// Creating an extended library configuration.
const config: AppMetricaConfig = {
  apiKey: API_KEY,
  // Setting session timeout.
  sessionTimeout: 15,
};
// Initializing the AppMetrica SDK.
AppMetrica.activate(config);
```

## Setting the app version {#version-app}

To specify the app version programmatically, pass the app version to the `appVersion` property when
creating an extended library configuration.

```javascript translate=no
  // Creating an extended library configuration.
const config: AppMetricaConfig = {
  apiKey: API_KEY,
  // Setting the app version.
  appVersion: '1.0',
};
// Initializing the AppMetrica SDK.
AppMetrica.activate(config);
```

Where `1.0` is the app version.

## Determining the library's API level (Android) {#level-api-android}

To determine the API level of the library from the application code, use the `AppMetrica.getLibraryApiLevel()` method.

```javascript translate=no
const [libraryApiLevel, setLibraryApiLevel] = useState('???');
AppMetrica.getLibraryApiLevel().then(level => {
  setLibraryApiLevel(level);
});
```

## Determining the library's version {#version-sdk}

To determine the library version from the application code, use the `AppMetrica.getLibraryVersion()` method:

```javascript translate=no
const [appMetricaVersion, setAppMetricaVersion] = useState('???');
AppMetrica.getLibraryVersion().then(version => {
  setAppMetricaVersion(version);
});
```

## Tracking app opens using deeplinks {#deeplink}

Deeplink opens are tracked by default. You can disable this by using an extended configuration:

```javascript translate=no
  // Creating an extended library configuration.
const config: AppMetricaConfig = {
  apiKey: API_KEY,
  appOpenTrackingEnabled: false,
};
// Initializing the AppMetrica SDK.
AppMetrica.activate(config);
```

If needed, you can manually send information about deeplink-triggered app opens to AppMetrica using the
`reportAppOpen()` method:

```javascript translate=no
AppMetrica.reportAppOpen(deeplink);
```

See also [How to create a remarketing campaign in AppMetrica](../../../troubleshooting/troubleshooting.md#remarketing-campaign).

## Tracking new users {#new-user}

By default, the user is counted as a new user when the app is opened for the first time. If the AppMetrica SDK
connects to an app that already has active users, to obtain valid statistics, you can set up
tracking of both new and old users. To do this, initialize the AppMetrica SDK using an extended
startup configuration, `AppMetricaConfig`:

```javascript translate=no
const isFirstLaunch: Boolean = false;
// Implement logic to detect whether the app is opening for the first time.
// For example, you can check for files (settings, databases, and so on),
// which the app creates on its first launch.
if (conditions) {
  isFirstLaunch = true;
}
// Creating an extended library configuration.
const config: AppMetricaConfig = {
  apiKey: API_KEY,
  firstActivationAsUpdate: !isFirstLaunch,
};
// Initializing the AppMetrica SDK.
AppMetrica.activate(config);
```

## Disabling and enabling sending statistics {#stat}

If you need to obtain user consent before sending statistical data, initialize the library with the
statistics sending option disabled. To do this, pass `false` to the `statisticsSending` property when creating
an extended library configuration.

```javascript translate=no
// Creating an extended library configuration.
const config: AppMetricaConfig = {
  apiKey: API_KEY,
  // Disabling sending data.
  statisticsSending: false,
};
// Initializing the AppMetrica SDK.
AppMetrica.activate(config);
```

After the user consents to statistics sending (for example, through app settings or by giving their permission during the
first app launch), use the `AppMetrica.setDataSendingEnabled(true)` method to enable statistics sending:

```javascript translate=no
// Checking the status of the boolean variable. It shows the user confirmation.
if (flag) {
  // Enabling sending data.
  AppMetrica.setDataSendingEnabled(true);
}
```

### Alert example {#stat-alert-example}

You can use any text to inform users of statistics collection. For example:

> This app uses the AppMetrica analytical service provided by YANDEX LLC,
> ulitsa Lva Tolstogo 16, Moscow, Russia 119021 (hereinafter referred to as Yandex) based on the [Terms of Use](https://yandex.com/legal/metrica_termsofuse/).
>
> AppMetrica analyzes app usage data, including information about the device it is running on,
> install source, conversions, and statistics of your activity, for the purposes of product analytics,
> ad campaign optimization, and troubleshooting. The data collected in this manner cannot
> be used to identify you.
>
> The depersonalized information about your use of this app collected by AppMetrica tools
> will be transferred to Yandex and stored on Yandex servers in the EU and the Russian Federation. Yandex will process this
> information to provide you with app usage statistics, generate reports for us on app performance,
> and deliver other services.

## Getting AppMetrica SDK IDs {#get-ids}

To get AppMetrica SDK IDs (`DeviceId`, `DeviceIdHash`, `UUID`), use the
`requestStartupParams()` method. To get the `appmetrica_device_id`, make sure to request the `DeviceIdHash`.

```javascript translate=no
import AppMetrica, {
  DEVICE_ID_HASH_KEY,
  DEVICE_ID_KEY,
  UUID_KEY,
  StartupParams,
  StartupParamsCallback,
  StartupParamsReason,
} from '@appmetrica/react-native-analytics';
```

```javascript translate=no
const paramsList: Array<string> = [
  DEVICE_ID_HASH_KEY,
  DEVICE_ID_KEY,
  UUID_KEY,
];
const paramsCallback: StartupParamsCallback = (params?: StartupParams, reason?: StartupParamsReason) => {
  // ...
};

AppMetrica.requestStartupParams(paramsCallback, paramsList);
```

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
