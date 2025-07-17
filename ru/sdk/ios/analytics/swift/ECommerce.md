# Класс ECommerce

Методы класса создают объект `ECommerce`.

Для различных действий пользователя есть соответствующие типы ecommerce-событий. Чтобы создать конкретный тип события, используйте нужный метод класса.

{% note info %}

Объект `ECommerce` можно отправить с помощью метода [reportECommerce(_:onFailure:)](AppMetrica.md#method_reportECommerce__onFailure) класса [AppMetrica](AppMetrica.md) и протокола [AppMetricaReporting](AppMetricaReporting.md).

{% endnote %}

## Методы экземпляра {#instance_summary}

#|
|| [showScreenEvent(screen:)](#method_showScreenEventWithScreen) | Создает ecommerce-событие `ShowScreenEvent`. Используйте его, чтобы сообщить об открытии какой-либо страницы, например: списка товаров, поиска, главной страницы. ||
|| [showProductCardEvent(product:screen:)](#method_showProductCardEventWithProduct__screen) | Создает ecommerce-событие `ShowProductCardEvent`. Используйте его, чтобы сообщить о просмотре карточки товара среди других в списке. ||
|| [showProductDetailsEvent(product:referrer:)](#method_showProductDetailsEventWithProduct__referrer) | Создает ecommerce-событие `ShowProductDetailsEvent`. Используйте его, чтобы сообщить о просмотре страницы товара. ||
|| [addCartItemEvent(cartItem:)](#method_addCartItemEventWithItem) | Создает ecommerce-событие `AddCartItemEvent`. Используйте его, чтобы сообщить о добавлении товара в корзину. ||
|| [removeCartItemEvent(cartItem:)](#method_removeCartItemEventWithItem) | Создает ecommerce-событие `RemoveCartItemEvent`. Используйте его, чтобы сообщить об удалении товара из корзины. ||
|| [beginCheckoutEvent(order:)](#method_beginCheckoutEventWithOrder) | Создает ecommerce-событие `BeginCheckoutEvent`. Используйте его, чтобы сообщить о начале оформления покупки. ||
|| [purchaseEvent(order:)](#method_purchaseEventWithOrder) | Создает ecommerce-событие `PurchaseEvent`. Используйте его, чтобы сообщить о завершении покупки. ||
|#

## Описание методов {#method_detail}

### showScreenEvent(screen:) {#method_showScreenEventWithScreen}

```swift translate=no
static func showScreenEvent(screen: ECommerceScreen) -> ECommerce
```

Создает ecommerce-событие `ShowScreenEvent`. Используйте его, чтобы сообщить об открытии какой-либо страницы, например: списка товаров, поиска, главной страницы.

**Параметры:**

#|
|| `screen` | Экран, который был открыт. Объект класса [ECommerceScreen](ECommerceScreen.md). ||
|#

**Возвращает:**

Объект класса `ECommerce`.

### showProductCardEvent(product:screen:) {#method_showProductCardEventWithProduct__screen}

```swift translate=no
static func showProductCardEvent(product: ECommerceProduct,  screen: ECommerceScreen) -> ECommerce
```

Создает ecommerce-событие `ShowProductCardEvent`. Используйте его, чтобы сообщить о просмотре карточки товара среди других в списке.

{% note info %}

Перед отправкой события убедитесь, что карточка товара была показана на экране более N секунд.

{% endnote %}

**Параметры:**

#|
|| `product` | Товар, который был показан. Объект класса [ECommerceProduct](ECommerceProduct.md). ||
|| `screen` | Экран, на котором был показан товар. Объект класса [ECommerceScreen](ECommerceScreen.md). ||
|#

**Возвращает:**

Объект класса `ECommerce`.

### showProductDetailsEvent(product:referrer:) {#method_showProductDetailsEventWithProduct__referrer}

```swift translate=no
static func showProductDetailsEvent(product: ECommerceProduct, referrer: ECommerceReferrer?) -> ECommerce
```

Создает ecommerce-событие `ShowProductDetailsEvent`. Используйте его, чтобы сообщить о просмотре страницы товара.

**Параметры:**

#|
|| `product` | Товар, который был показан. Объект класса [ECommerceProduct](ECommerceProduct.md). ||
|| `referrer` | Информация об источнике перехода на страницу товара. Объект класса [ECommerceReferrer](ECommerceReferrer.md). ||
|#

**Возвращает:**

Объект класса `ECommerce`.

### addCartItemEvent(cartItem:) {#method_addCartItemEventWithItem}

```swift translate=no
static func addCartItemEvent(cartItem: ECommerceCartItem) -> ECommerce
```

Создает ecommerce-событие `AddCartItemEvent`. Используйте его, чтобы сообщить о добавлении товара в корзину.

**Параметры:**

#|
|| `item` | Товар, который был добавлен в корзину. Объект класса [ECommerceCartItem](ECommerceCartItem.md). ||
|#

**Возвращает:**

Объект класса `ECommerce`.

### removeCartItemEvent(cartItem:) {#method_removeCartItemEventWithItem}

```swift translate=no
static func removeCartItemEvent(cartItem: ECommerceCartItem) -> ECommerce
```

Создает ecommerce-событие `RemoveCartItemEvent`. Используйте его, чтобы сообщить об удалении товара из корзины.

**Параметры:**

#|
|| `item` | Товар, который был удален из корзины. Объект класса [ECommerceCartItem](ECommerceCartItem.md). ||
|#

**Возвращает:**

Объект класса `ECommerce`.

### beginCheckoutEvent(order:) {#method_beginCheckoutEventWithOrder}

```swift translate=no
static func beginCheckoutEvent(order: ECommerceOrder) -> ECommerce
```

Создает ecommerce-событие `BeginCheckoutEvent`. Используйте его, чтобы сообщить о начале оформления покупки.

**Параметры:**

#|
|| `order` | Информация о покупке. Объект класса [ECommerceOrder](ECommerceOrder.md). ||
|#

**Возвращает:**

Объект класса `ECommerce`.

### purchaseEvent(order:) {#method_purchaseEventWithOrder}

```swift translate=no
static func purchaseEvent(order: ECommerceOrder) -> ECommerce
```

Создает ecommerce-событие `PurchaseEvent`. Используйте его, чтобы сообщить о завершении покупки.

**Параметры:**

#|
|| `order` | Информация о покупке. Объект класса [ECommerceOrder](ECommerceOrder.md). ||
|#

**Возвращает:**

Объект класса `ECommerce`.
