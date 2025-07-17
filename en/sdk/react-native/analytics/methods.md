# Methods

## Types

```javascript translate=no
// This type contains the extended configuration for library initialization.
export type AppMetricaConfig = {
  apiKey: string,
  appVersion?: string,
  crashReporting?: boolean,
  firstActivationAsUpdate?: boolean,
  location: Location,
  locationTracking?: boolean,
  logs?: boolean,
  sessionTimeout?: number,
  statisticsSending?: boolean,
  preloadInfo?: PreloadInfo,
  appOpenTrackingEnabled?: boolean,
  maxReportsInDatabaseCount?: number,
  // Android only.
  nativeCrashReporting?: boolean,
  // This type is for iOS only.
  activationAsSessionStart?: boolean,
  sessionsAutoTracking?: boolean,
  userProfileID?: string,
}

// This type contains information for tracking pre-installed apps.
export type PreloadInfo = {
  trackingId: string,
  additionalInfo?: Record<string, string>,
}

// This type contains information about the device's location.
export type Location = {
  latitude: number,
  longitude: number,
  altitude?: number,
  accuracy?: number,
  course?: number,
  speed?: number,
  timestamp?: number,
}

// Contains possible errors from the requestStartupParams() method.
export type StartupParamsReason = 'UNKNOWN' | 'NETWORK' | 'INVALID_RESPONSE';

// This type contains IDs that were obtained using the requestStartupParams() method.
export type StartupParams = {
  deviceIdHash?: string,
  deviceId?: string,
  uuid?: string,
}

// This type is a callback passed to the requestStartupParams() method.
type StartupParamsCallback = (
  params?: StartupParams,
  reason?: StartupParamsReason
) => void

// This type contains information about the screen where the E-commerce event occurs.
export type ECommerceScreen = {
  name: string,
  searchQuery?: string,
  payload?: Map<string, string>,
  categoriesPath?: Array<string>,
}

// This type contains the currency and cost data.
export type ECommerceAmount = {
  amount: number | string,
  unit: string,
}

// This type contains the price information.
export type ECommercePrice = {
  amount: ECommerceAmount,
  internalComponents?: Array<ECommerceAmount>,
}

// This type contains information about a specific product.
export type ECommerceProduct = {
  sku: string,
  name?: string,
  actualPrice?: ECommercePrice,
  originalPrice?: ECommercePrice,
  promocodes?: Array<string>,
  categoriesPath?: Array<string>,
  payload?: Map<string, string>,
}

// This type contains data about the referrer that brought the user to the product.
export type ECommerceReferrer = {
  type?: string,
  identifier?: string,
  screen?: ECommerceScreen,
}

// This type contains data about a cart item, its price and quantity.
export type ECommerceCartItem = {
  product: ECommerceProduct,
  price: ECommercePrice,
  quantity: number | string,
  referrer?: ECommerceReferrer,
}

// This type contains information about an order.
export type ECommerceOrder = {
  orderId: string,
  products: Array<ECommerceCartItem>,
  payload?: Map<string, string>,
}

// This type is used for sending in-app purchase data from the app. This type contains revenue data.
export type Revenue = {
  price: number,
  currency: string,
  productID?: string,
  quantity?: number,
  payload?: string,
  receipt?: Receipt,
}

// This type is used for validating in-app purchases.
export type Receipt = {
  transactionID?: string,
  receiptData?: string,
  signature?: string,
}

// This type contains ad revenue  information.
export type AdRevenue = {
  price: number | string,
  currency: string,
  payload?: Map<string, string>,
  adNetwork?: string,
  adPlacementID?: string,
  adPlacementName?: string,
  adType?: AdType,
  adUnitID?: string,
  adUnitName?: string,
  precision?: string,
}

// Contains possible GenderAttribute values
export type UserProfileGender = 'male' | 'female' | 'other';
```

## Enums

```javascript translate=no
// This type contains supported ad types for sending AdRevenue data.
export enum AdType {
  NATIVE,
  BANNER,
  MREC,
  INTERSTITIAL,
  REWARDED,
  OTHER,
}
```

## Classes
### AppMetrica

The main class used for interacting with the library.

```javascript translate=no
// It initializes the library with the extended configuration.
activate(config: AppMetricaConfig)

// This method returns the current version of the library.
async getLibraryVersion(): string

// This method reports that the current session has been paused.
pauseSession()

// This method reports that the app has been opened via a deeplink.
reportAppOpen(deeplink?: string = null)

// This method reports a custom event.
reportEvent(eventName: string, attributes?: Record<string, any>)

// This method reports errors.
reportError(identifier: string, message: string)

// This method requests various IDs from the AppMetrica SDK.
requestStartupParams(listener: StartupParamsCallback, identifiers: Array<string>)

// This method reports whether a session has been resumed or a new one has started after a timeout.
resumeSession()

// This method sends events stored in the buffer.
sendEventsBuffer()

// This method sends the device's location data.
setLocation(location?: Location)

// This method enables/disables the collection of device location data.
setLocationTracking(enabled: boolean)

// This method enables/disables sending data to AppMetrica.
setDataSendingEnabled(enabled: boolean)

// This method assigns a profile ID.
setUserProfileID(userProfileID?: string)

// This is an Android-only method. It returns the library's API level.
async getLibraryApiLevel(): number

// This method is used for reporting E-commerce events.
reportECommerce(event: ECommerceEvent)

// This method is used for reporting in-app purchases.
reportRevenue(revenue: Revenue)

// This method is used for sending AdRevenue data.
reportAdRevenue(adRevenue: AdRevenue)

// This method sends a user profile.
reportUserProfile(userProfile: UserProfile)
```

### E-commerce

For different user actions, there are appropriate types of E-commerce events. To create a specific event type, use the appropriate class method.

For more information about sending E-commerce events, see [E-commerce](../../../data-collection/about-ecommerce.md).

```javascript translate=no
// Returns ECommerceEvent for sending a “product card view” event.
showProductCardEvent(product: ECommerceProduct, screen: ECommerceScreen): ECommerceEvent

// This method returns ECommerceEvent for sending a “product page view” event.
showProductDetailsEvent(product: ECommerceProduct, referrer?: ECommerceReferrer): ECommerceEvent

// This method returns ECommerceEvent for sending an “add item to cart” event.
addCartItemEvent(item: ECommerceCartItem): ECommerceEvent

// This method returns ECommerceEvent for sending a “remove item from cart” event.
removeCartItemEvent(item: ECommerceCartItem): ECommerceEvent

// This method returns ECommerceEvent for sending a ”begin checkout” event.
beginCheckoutEvent(order: ECommerceOrder): ECommerceEvent

// This method returns ECommerceEvent for sending a “purchase complete” event.
purchaseEvent(order: ECommerceOrder): ECommerceEvent
```

To learn more about the API methods and AppMetrica integration into your app, see the [Android](../../android/analytics/quick-start.md) and [iOS](../../ios/analytics/quick-start.md) sections in our documentation.

### UserProfile

A class for storing a user profile. [Learn more](react-native-operations.md#send-attribute-profile).

```javascript translate=no
// Applies a user attribute to UserProfile
apply(attribute: UserProfileUpdate): UserProfile
```

### Attributes {#attributes}

A class for creating profile attributes. [Learn more](react-native-operations.md#send-attribute-profile).

```javascript translate=no
// Creates a predefined attribute for birth date / age.
birthDate(): BirthDateAttribute

// Creates a predefined gender attribute.
gender(): GenderAttribute

// Creates a predefined name attribute.
userName(): NameAttribute

// Creates a predefined notification status attribute.
notificationsEnabled(): NotificationsEnabledAttribute

// Creates a custom attribute of the bool type.
customBoolean(key: string): BooleanAttribute

// Creates a custom attribute of the tag type.
customCounter(key: string): CounterAttribute

// Creates a custom attribute of the number type.
customNumber(key: string): NumberAttribute

// Creates a custom attribute of the string type.
customString(key: string): StringAttribute
```

### BirthDateAttribute

A class for updating the age or date of birth in a user profile.

```javascript translate=no
// Updates the attribute value.
withAge(age: number): UserProfileUpdate

// Updates the attribute value if it wasn't set earlier.
withAgeIfUndefined(age: number): UserProfileUpdate

// Updates the attribute value.
withYear(year: number): UserProfileUpdate

// Updates the attribute value if it wasn't set earlier.
withYearIfUndefined(year: number): UserProfileUpdate

// Updates the attribute value.
withMonth(year: number, month: number): UserProfileUpdate

// Updates the attribute value if it wasn't set earlier.
withMonthIfUndefined(year: number, month: number): UserProfileUpdate

// Updates the attribute value.
withDay(year: number, month: number, day: number): UserProfileUpdate

// Updates the attribute value if it wasn't set earlier.
withDayIfUndefined(year: number, month: number, day: number): UserProfileUpdate

// Updates the attribute value.
withDate(date: Date): UserProfileUpdate

// Updates the attribute value if it wasn't set earlier.
withDateIfUndefined(date: Date): UserProfileUpdate

// Resets the attribute value.
withValueReset(): UserProfileUpdate
```

### BooleanAttribute

A class for updating the value of a boolean attribute.

```javascript translate=no
// Updates the attribute value.
withValue(value: boolean): UserProfileUpdate

// Updates the attribute value if it wasn't set earlier.
withValueIfUndefined(value: boolean): UserProfileUpdate

// Resets the attribute value.
withValueReset(): UserProfileUpdate
```

### CounterAttribute

A class for updating the value of the tag type attribute.

```javascript translate=no
// Updates the attribute value.
withDelta(delta: number): UserProfileUpdate
```

### GenderAttribute

A class for updating the gender in a user profile.

```javascript translate=no
// Updates the attribute value.
withValue(gender: UserProfileGender): UserProfileUpdate

// Updates the attribute value if it wasn't set earlier.
withValueIfUndefined(gender: UserProfileGender): UserProfileUpdate

// Resets the attribute value.
withValueReset(): UserProfileUpdate
```

### NameAttribute

A class for updating the name in a user profile.

```javascript translate=no
// Updates the attribute value.
withValue(value: string): UserProfileUpdate

// Updates the attribute value if it wasn't set earlier.
withValueIfUndefined(value: string): UserProfileUpdate

// Resets the attribute value.
withValueReset(): UserProfileUpdate
```

### NotificationsEnabledAttribute

A class for updating the notification status in a user profile.

```javascript translate=no
// Updates the attribute value.
withValue(value: boolean): UserProfileUpdate

// Updates the attribute value if it wasn't set earlier.
withValueIfUndefined(value: boolean): UserProfileUpdate

// Resets the attribute value.
withValueReset(): UserProfileUpdate
```

### NumberAttribute

A class for updating the value of a numeric attribute.

```javascript translate=no
// Updates the attribute value.
withValue(value: number): UserProfileUpdate

// Updates the attribute value if it wasn't set earlier.
withValueIfUndefined(value: number): UserProfileUpdate

// Resets the attribute value.
withValueReset(): UserProfileUpdate
```

### StringAttribute

A class for updating the value of a string attribute.

```javascript translate=no
// Updates the attribute value.


withValue(value: string): UserProfileUpdate// Updates the attribute value if it wasn't set earlier.


withValueIfUndefined(value: string): UserProfileUpdate// Resets the attribute value.
withValueReset(): UserProfileUpdate
```

## Interfaces

### UserProfileUpdate

Contains information about user attribute updates.

Created using the [Attributes](#attributes) class methods and passed to the `UserProfile.apply` method.

## See also

- [How do I enable user location sending?](../../../troubleshooting/troubleshooting.md#region)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
