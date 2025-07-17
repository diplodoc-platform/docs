# Класс AMAECommerce

Методы класса создают объект `AMAECommerce`.

Для различных действий пользователя есть соответствующие типы ECommerce-событий. Чтобы создать конкретный тип события, используйте нужный метод класса `AMAECommerce`.

{% note info %}

Объект `AMAECommerce` можно отправить с помощью метода [+reportECommerce:onFailure:](AMAAppMetrica.md#method_reportECommerce__onFailure) класса [AMAAppMetrica](AMAAppMetrica.md) и протокола [AMAAppMetricaReporting](AMAAppMetricaReporting.md).

{% endnote %}

## Методы экземпляра {#instance_summary}

#|
|| +[showScreenEventWithScreen:](#method_showScreenEventWithScreen) | Создает ECommerce-событие `ShowScreenEvent`. Используйте его, чтобы сообщить об открытии какой-либо страницы, например: списка товаров, поиска, главной страницы. ||
|| +[showProductCardEventWithProduct:screen:](#method_showProductCardEventWithProduct__screen) | Создает ECommerce-событие `ShowProductCardEvent`. Используйте его, чтобы сообщить о просмотре карточки товара среди других в списке. ||
|| +[showProductDetailsEventWithProduct:referrer:](#method_showProductDetailsEventWithProduct__referrer) | Создает ECommerce-событие `ShowProductDetailsEvent`. Используйте его, чтобы сообщить о просмотре страницы товара. ||
|| +[addCartItemEventWithItem:](#method_addCartItemEventWithItem) | Создает ECommerce-событие `AddCartItemEvent`. Используйте его, чтобы сообщить о добавлении товара в корзину. ||
|| +[removeCartItemEventWithItem:](#method_removeCartItemEventWithItem) | Создает ECommerce-событие `RemoveCartItemEvent`. Используйте его, чтобы сообщить об удалении товара из корзины. ||
|| +[beginCheckoutEventWithOrder:](#method_beginCheckoutEventWithOrder) | Создает ECommerce-событие `BeginCheckoutEvent`. Используйте его, чтобы сообщить о начале оформления покупки. ||
|| +[purchaseEventWithOrder:](#method_purchaseEventWithOrder) | Создает ECommerce-событие `PurchaseEvent`. Используйте его, чтобы сообщить о завершении покупки. ||
|#

## Описание методов {#method_detail}

### +showScreenEventWithScreen: {#method_showScreenEventWithScreen}

```objectivec translate=no
+ (instancetype)showScreenEventWithScreen:(AMAECommerceScreen *)screen
```

Создает ECommerce-событие `ShowScreenEvent`. Используйте его, чтобы сообщить об открытии какой-либо страницы, например: списка товаров, поиска, главной страницы.

**Параметры:**

#|
|| `screen` | Экран, который был открыт. Объект класса [AMAECommerceScreen](AMAECommerceScreen.md). ||
|#

**Возвращает:**

Объект класса `AMAECommerce`.

### +showProductCardEventWithProduct:screen: {#method_showProductCardEventWithProduct__screen}

```objectivec translate=no
+ (instancetype)showProductCardEventWithProduct:(AMAECommerceProduct *)product
                                         screen:(AMAECommerceScreen *)screen
```

Создает ECommerce-событие `ShowProductCardEvent`. Используйте его, чтобы сообщить о просмотре карточки товара среди других в списке.

{% note info %}

Перед отправкой события убедитесь, что карточка товара была показана на экране более N секунд.

{% endnote %}

**Параметры:**

#|
|| `product` | Товар, который был показан. Объект класса [AMAECommerceProduct](AMAECommerceProduct.md). ||
|| `screen` | Экран, на котором был показан товар. Объект класса [AMAECommerceScreen](AMAECommerceScreen.md). ||
|#

**Возвращает:**

Объект класса `AMAECommerce`.

### +showProductDetailsEventWithProduct:referrer: {#method_showProductDetailsEventWithProduct__referrer}

```objectivec translate=no
+ (instancetype)showProductDetailsEventWithProduct:(AMAECommerceProduct *)product
                                          referrer:(nullable AMAECommerceReferrer *)referrer
```

Создает ECommerce-событие `ShowProductDetailsEvent`. Используйте его, чтобы сообщить о просмотре страницы товара.

**Параметры:**

#|
|| `product` | Товар, который был показан. Объект класса [AMAECommerceProduct](AMAECommerceProduct.md). ||
|| `referrer` | Информация об источнике перехода на страницу товара. Объект класса [AMAECommerceReferrer](AMAECommerceReferrer.md). ||
|#

**Возвращает:**

Объект класса `AMAECommerce`.

### +addCartItemEventWithItem: {#method_addCartItemEventWithItem}

```objectivec translate=no
+ (instancetype)addCartItemEventWithItem:(AMAECommerceCartItem *)item
```

Создает ECommerce-событие `AddCartItemEvent`. Используйте его, чтобы сообщить о добавлении товара в корзину.

**Параметры:**

#|
|| `item` | Товар, который был добавлен в корзину. Объект класса [AMAECommerceCartItem](AMAECommerceCartItem.md). ||
|#

**Возвращает:**

Объект класса `AMAECommerce`.

### +removeCartItemEventWithItem: {#method_removeCartItemEventWithItem}

```objectivec translate=no
+ (instancetype)removeCartItemEventWithItem:(AMAECommerceCartItem *)item
```

Создает ECommerce-событие `RemoveCartItemEvent`. Используйте его, чтобы сообщить об удалении товара из корзины.

**Параметры:**

#|
|| `item` | Товар, который был удален из корзины. Объект класса [AMAECommerceCartItem](AMAECommerceCartItem.md). ||
|#

**Возвращает:**

Объект класса `AMAECommerce`.

### +beginCheckoutEventWithOrder: {#method_beginCheckoutEventWithOrder}

```objectivec translate=no
+ (instancetype)beginCheckoutEventWithOrder:(AMAECommerceOrder *)order
```

Создает ECommerce-событие `BeginCheckoutEvent`. Используйте его, чтобы сообщить о начале оформления покупки.

**Параметры:**

#|
|| `order` | Информация о покупке. Объект класса [AMAECommerceOrder](AMAECommerceOrder.md). ||
|#

**Возвращает:**

Объект класса `AMAECommerce`.

### +purchaseEventWithOrder: {#method_purchaseEventWithOrder}

```objectivec translate=no
+ (instancetype)purchaseEventWithOrder:(AMAECommerceOrder *)order
```

Создает ECommerce-событие `PurchaseEvent`. Используйте его, чтобы сообщить о завершении покупки.

**Параметры:**

#|
|| `order` | Информация о покупке. Объект класса [AMAECommerceOrder](AMAECommerceOrder.md). ||
|#

**Возвращает:**

Объект класса `AMAECommerce`.
