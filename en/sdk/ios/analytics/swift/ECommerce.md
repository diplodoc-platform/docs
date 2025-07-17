# ECommerce class

Methods of this class create an `ECommerce` instance.

For different user actions, there are appropriate types of E-commerce events. To create a specific event type, use the appropriate class method.

{% note info %}

You can send the `ECommerce` instance using the [reportECommerce(_:onFailure:)](AppMetrica.md#method_reportECommerce__onFailure) method of the [AppMetrica](AppMetrica.md) class and the [AppMetricaReporting](AppMetricaReporting.md) protocol.

{% endnote %}

## Instance methods {#instance_summary}

#|
|| [showScreenEvent(screen:)](#method_showScreenEventWithScreen) | Creates an E-commerce event called `ShowScreenEvent`. Use it to report the opening of a page, such as a list of products, search or home page. ||
|| [showProductCardEvent(product:screen:)](#method_showProductCardEventWithProduct__screen) | Creates an E-commerce event called `ShowProductCardEvent`. Use it to report viewing a product profile among others on the list. ||
|| [showProductDetailsEvent(product:referrer:)](#method_showProductDetailsEventWithProduct__referrer) | Creates an E-commerce event called `ShowProductDetailsEvent`. Use it to report viewing a product page. ||
|| [addCartItemEvent(cartItem:)](#method_addCartItemEventWithItem) | Creates an E-commerce event called `AddCartItemEvent`. Use it to report adding an item to the cart. ||
|| [removeCartItemEvent(cartItem:)](#method_removeCartItemEventWithItem) | Creates an E-commerce event called `RemoveCartItemEvent`. Use it to report removing an item from the cart. ||
|| [beginCheckoutEvent(order:)](#method_beginCheckoutEventWithOrder) | Creates an E-commerce event called `BeginCheckoutEvent`. Use it to report starting a purchase. ||
|| [purchaseEvent(order:)](#method_purchaseEventWithOrder) | Creates an E-commerce event called `PurchaseEvent`. Use it to report a completed purchase. ||
|#

## Method descriptions {#method_detail}

### showScreenEvent(screen:) {#method_showScreenEventWithScreen}

```swift translate=no
static func showScreenEvent(screen: ECommerceScreen) -> ECommerce
```

Creates an E-commerce event called `ShowScreenEvent`. Use it to report the opening of a page, such as a list of products, search or home page.

**Parameters:**

#|
|| `screen` | The screen that was opened. The [ECommerceScreen](ECommerceScreen.md) class instance. ||
|#

**Returns:**

The `ECommerce` class instance.

### showProductCardEvent(product:screen:) {#method_showProductCardEventWithProduct__screen}

```swift translate=no
static func showProductCardEvent(product: ECommerceProduct,  screen: ECommerceScreen) -> ECommerce
```

Creates an E-commerce event called `ShowProductCardEvent`. Use it to report viewing a product profile among others on the list.

{% note info %}

Before sending the event, make sure that the product profile was shown on the screen for more than N seconds.

{% endnote %}

**Parameters:**

#|
|| `product` | The product that was shown. The [ECommerceProduct](ECommerceProduct.md) class instance. ||
|| `screen` | The screen where the product was displayed. The [ECommerceScreen](ECommerceScreen.md) class instance. ||
|#

**Returns:**

The `ECommerce` class instance.

### showProductDetailsEvent(product:referrer:) {#method_showProductDetailsEventWithProduct__referrer}

```swift translate=no
static func showProductDetailsEvent(product: ECommerceProduct, referrer: ECommerceReferrer?) -> ECommerce
```

Creates an E-commerce event called `ShowProductDetailsEvent`. Use it to report viewing a product page.

**Parameters:**

#|
|| `product` | The product that was shown. The [ECommerceProduct](ECommerceProduct.md) class instance. ||
|| `referrer` | Information about the source of traffic to the product page. The [ECommerceReferrer](ECommerceReferrer.md) class instance. ||
|#

**Returns:**

The `ECommerce` class instance.

### addCartItemEvent(cartItem:) {#method_addCartItemEventWithItem}

```swift translate=no
static func addCartItemEvent(cartItem: ECommerceCartItem) -> ECommerce
```

Creates an E-commerce event called `AddCartItemEvent`. Use it to report adding an item to the cart.

**Parameters:**

#|
|| `item` | The item that was added to the cart. The [ECommerceCartItem](ECommerceCartItem.md) class instance. ||
|#

**Returns:**

The `ECommerce` class instance.

### removeCartItemEvent(cartItem:) {#method_removeCartItemEventWithItem}

```swift translate=no
static func removeCartItemEvent(cartItem: ECommerceCartItem) -> ECommerce
```

Creates an E-commerce event called `RemoveCartItemEvent`. Use it to report removing an item from the cart.

**Parameters:**

#|
|| `item` | The item that was removed from the cart. The [ECommerceCartItem](ECommerceCartItem.md) class instance. ||
|#

**Returns:**

The `ECommerce` class instance.

### beginCheckoutEvent(order:) {#method_beginCheckoutEventWithOrder}

```swift translate=no
static func beginCheckoutEvent(order: ECommerceOrder) -> ECommerce
```

Creates an E-commerce event called `BeginCheckoutEvent`. Use it to report starting a purchase.

**Parameters:**

#|
|| `order` | Information about the purchase. The [ECommerceOrder](ECommerceOrder.md) class instance. ||
|#

**Returns:**

The `ECommerce` class instance.

### purchaseEvent(order:) {#method_purchaseEventWithOrder}

```swift translate=no
static func purchaseEvent(order: ECommerceOrder) -> ECommerce
```

Creates an E-commerce event called `PurchaseEvent`. Use it to report a completed purchase.

**Parameters:**

#|
|| `order` | Information about the purchase. The [ECommerceOrder](ECommerceOrder.md) class instance. ||
|#

**Returns:**

The `ECommerce` class instance.
