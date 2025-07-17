# AMAECommerce class

Methods of this class create an `AMAECommerce` instance.

For different user actions, there are appropriate types of E-commerce events. To create a specific event type, use the appropriate `AMAECommerce` class method.

{% note info %}

You can send the `AMAECommerce` instance using the [+reportECommerce:onFailure:](AMAAppMetrica.md#method_reportECommerce__onFailure) method of the [AMAAppMetrica](AMAAppMetrica.md) class and the [AMAAppMetricaReporting](AMAAppMetricaReporting.md) protocol.

{% endnote %}

## Instance methods {#instance_summary}

#|
|| +[showScreenEventWithScreen:](#method_showScreenEventWithScreen) | Creates an E-commerce event called `ShowScreenEvent`. Use it to report the opening of a page, such as a list of products, search or home page. ||
|| +[showProductCardEventWithProduct:screen:](#method_showProductCardEventWithProduct__screen) | Creates an E-commerce event called `ShowProductCardEvent`. Use it to report viewing a product profile among others on the list. ||
|| +[showProductDetailsEventWithProduct:referrer:](#method_showProductDetailsEventWithProduct__referrer) | Creates an E-commerce event called `ShowProductDetailsEvent`. Use it to report viewing a product page. ||
|| +[addCartItemEventWithItem:](#method_addCartItemEventWithItem) | Creates an E-commerce event called `AddCartItemEvent`. Use it to report adding an item to the cart. ||
|| +[removeCartItemEventWithItem:](#method_removeCartItemEventWithItem) | Creates an E-commerce event called `RemoveCartItemEvent`. Use it to report removing an item from the cart. ||
|| +[beginCheckoutEventWithOrder:](#method_beginCheckoutEventWithOrder) | Creates an E-commerce event called `BeginCheckoutEvent`. Use it to report starting a purchase. ||
|| +[purchaseEventWithOrder:](#method_purchaseEventWithOrder) | Creates an E-commerce event called `PurchaseEvent`. Use it to report a completed purchase. ||
|#

## Method descriptions {#method_detail}

### +showScreenEventWithScreen: {#method_showScreenEventWithScreen}

```objectivec translate=no
+ (instancetype)showScreenEventWithScreen:(AMAECommerceScreen *)screen
```

Creates an E-commerce event called `ShowScreenEvent`. Use it to report the opening of a page, such as a list of products, search or home page.

**Parameters:**

#|
|| `screen` | The screen that was opened. The [AMAECommerceScreen](AMAECommerceScreen.md) class instance. ||
|#

**Returns:**

The `AMAECommerce` class instance.

### +showProductCardEventWithProduct:screen: {#method_showProductCardEventWithProduct__screen}

```objectivec translate=no
+ (instancetype)showProductCardEventWithProduct:(AMAECommerceProduct *)product
                                         screen:(AMAECommerceScreen *)screen
```

Creates an E-commerce event called `ShowProductCardEvent`. Use it to report viewing a product profile among others on the list.

{% note info %}

Before sending the event, make sure that the product profile was shown on the screen for more than N seconds.

{% endnote %}

**Parameters:**

#|
|| `product` | The product that was shown. The [AMAECommerceProduct](AMAECommerceProduct.md) class instance. ||
|| `screen` | The screen where the product was displayed. The [AMAECommerceScreen](AMAECommerceScreen.md) class instance. ||
|#

**Returns:**

The `AMAECommerce` class instance.

### +showProductDetailsEventWithProduct:referrer: {#method_showProductDetailsEventWithProduct__referrer}

```objectivec translate=no
+ (instancetype)showProductDetailsEventWithProduct:(AMAECommerceProduct *)product
                                          referrer:(nullable AMAECommerceReferrer *)referrer
```

Creates an E-commerce event called `ShowProductDetailsEvent`. Use it to report viewing a product page.

**Parameters:**

#|
|| `product` | The product that was shown. The [AMAECommerceProduct](AMAECommerceProduct.md) class instance. ||
|| `referrer` | Information about the source of traffic to the product page. The [AMAECommerceReferrer](AMAECommerceReferrer.md) class instance. ||
|#

**Returns:**

The `AMAECommerce` class instance.

### +addCartItemEventWithItem: {#method_addCartItemEventWithItem}

```objectivec translate=no
+ (instancetype)addCartItemEventWithItem:(AMAECommerceCartItem *)item
```

Creates an E-commerce event called `AddCartItemEvent`. Use it to report adding an item to the cart.

**Parameters:**

#|
|| `item` | The item that was added to the cart. The [AMAECommerceCartItem](AMAECommerceCartItem.md) class instance. ||
|#

**Returns:**

The `AMAECommerce` class instance.

### +removeCartItemEventWithItem: {#method_removeCartItemEventWithItem}

```objectivec translate=no
+ (instancetype)removeCartItemEventWithItem:(AMAECommerceCartItem *)item
```

Creates an E-commerce event called `RemoveCartItemEvent`. Use it to report removing an item from the cart.

**Parameters:**

#|
|| `item` | The item that was removed from the cart. The [AMAECommerceCartItem](AMAECommerceCartItem.md) class instance. ||
|#

**Returns:**

The `AMAECommerce` class instance.

### +beginCheckoutEventWithOrder: {#method_beginCheckoutEventWithOrder}

```objectivec translate=no
+ (instancetype)beginCheckoutEventWithOrder:(AMAECommerceOrder *)order
```

Creates an E-commerce event called `BeginCheckoutEvent`. Use it to report starting a purchase.

**Parameters:**

#|
|| `order` | Information about the purchase. The [AMAECommerceOrder](AMAECommerceOrder.md) class instance. ||
|#

**Returns:**

The `AMAECommerce` class instance.

### +purchaseEventWithOrder: {#method_purchaseEventWithOrder}

```objectivec translate=no
+ (instancetype)purchaseEventWithOrder:(AMAECommerceOrder *)order
```

Creates an E-commerce event called `PurchaseEvent`. Use it to report a completed purchase.

**Parameters:**

#|
|| `order` | Information about the purchase. The [AMAECommerceOrder](AMAECommerceOrder.md) class instance. ||
|#

**Returns:**

The `AMAECommerce` class instance.
