# Примеры использования методов

## Инициализация библиотеки с расширенной конфигурацией {#initialize}

Чтобы инициализировать библиотеку с расширенной стартовой конфигурацией, создайте объект типа `AppMetricaConfig` с
необходимыми настройками и активируйте библиотеку с помощью метода `AppMetrica.activate(config: AppMetricaConfig)`. С
помощью расширенной конфигурации можно, например, включить/отключить логирование, установить таймаут сессии, передать
параметры для [отслеживания предустановленных приложений](../../../mobile-tracking/preinstalled-app-attr.md) и т. д.

Настройки расширенной конфигурации применяются с момента инициализации библиотеки.

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

Чтобы настроить библиотеку в процессе работы приложения, используйте методы класса `AppMetrica`.

## Отправка статистики на дополнительный API key {#reporter-different-apikey}

Отправка данных на дополнительный API key позволяет собирать для каждого API key свою статистику. Это можно использовать для управления доступом к информации. Например, чтобы предоставить доступ к статистике для аналитиков, можно продублировать отправку маркетинговых данных на дополнительный API key и предоставить им доступ к этой статистике. Так у них будет доступ только к той информации, которая им необходима.

Для отправки данных на дополнительный API key необходимо использовать репортеры. С их помощью можно отправлять события, сообщения об ошибках, профили и информацию о покупках в приложении. Репортеры могут работать без инициализации AppMetrica SDK.

### Шаг 1. (Опционально) Инициализируйте репортер с расширенной конфигурацией {#reporter-different-apikey-initialize}

Чтобы инициализировать репортер с расширенной конфигурацией, создайте объект типа `ReporterConfig` с необходимыми настройками и активируйте репортер с помощью метода `AppMetrica.activateReporter(config: ReporterConfig)`. Конфигурация применяется для репортера с указанным API key. Для каждого дополнительного API key можно настроить свою конфигурацию.

{% note alert "" %}

Инициализацию репортера с расширенной конфигурацией необходимо проводить до первого обращения к репортеру. Иначе репортер будет инициализирован без конфигурации.

{% endnote %}

  ```javascript translate=no
  // Creating extended configuration of the reporter.
  // To create it, pass a ANOTHER_API_KEY that is different from the app's API_KEY.
  const reporterConfig: ReporterConfig = {
    apiKey: API_KEY,
    logs: true,
    sessionTimeout: 20,
  }
  AppMetrica.activateReporter(reporterConfig);
  ```

### Шаг 2. Настройте отправку данных с помощью репортера {#reporter-different-apikey-send}

Для отправки данных с помощью репортера, необходимо получить объект, который реализует интерфейс `IReporter` с помощью метода `AppMetrica.getReporter(apiKey: string)` и использовать методы интерфейса для отправки отчетов. Если репортер не был инициализирован с расширенной конфигурацией, то вызов данного метода произведет инициализацию репортера для указанного API key.

Пример отправки события:

  ```javascript translate=no
  AppMetrica.getReporter(ANOTHER_API_KEY).reportEvent("Updates installed");
  ```

Для корректного отслеживания сессий взаимодействия пользователя с приложением настройте отправку событий о начале и приостановке сессии для каждого репортера. Для этого используйте методы `resumeSession()` и `pauseSession()` интерфейса `IReporter`:

  ```javascript translate=no
  // When app goes to foreground
  AppMetrica.getReporter(ANOTHER_API_KEY).resumeSession();
  // When app goes to background
  AppMetrica.getReporter(ANOTHER_API_KEY).pauseSession();
  ```


## Отправка местоположения устройства библиотекой {#track-location}

{% note info %}

Для Android отправка местоположения устройства по умолчанию отключена.

{% endnote %}

Чтобы включить отправку, инициализируйте библиотеку с конфигурацией, в которой отправка информации о местоположении
устройства включена. Для этого укажите `true` в свойство `locationTracking` при создании расширенной конфигурации
библиотеки.

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

Чтобы включить отправку в процессе работы приложения, используйте
метод `AppMetrica.setLocationTracking(enabled: boolean)`:

```javascript translate=no
AppMetrica.setLocationTracking(true);
```

Для более точного определения местоположения добавьте в файл AndroidManifest.xml одно из следующих разрешений:

- [android.permission.ACCESS_COARSE_LOCATION](https://developer.android.com/reference/android/Manifest.permission.html#ACCESS_COARSE_LOCATION) —
  для приблизительного определения.
- [android.permission.ACCESS_FINE_LOCATION](https://developer.android.com/reference/android/Manifest.permission.html#ACCESS_FINE_LOCATION) —
  для точного определения.

## Установка местоположения вручную {#location-manual}

Перед отправкой собственной информации о местоположении устройства убедитесь, что отправка отчетов была включена.

Библиотека определяет местоположение устройства самостоятельно. Чтобы отправить собственную информацию о местоположении
устройства, передайте `Location` в метод `AppMetrica.setLocation(location?: Location)`.

```javascript translate=no
import AppMetrica from '@appmetrica/react-native-analytics';
```

```javascript translate=no
// Determining the location.
const currentLocation: Location = {
  ...
}
// Setting your own location information of the device.
AppMetrica.setLocation(currentLocation);
```

Чтобы отправить собственную информацию о местоположении устройства с помощью расширенной конфигурации, передайте объект типа `Location` в свойство `location?: Location` при создании расширенной конфигурации библиотеки.

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
  // Set your own location information of the device.
  location: currentLocation,
}
// Initializing the AppMetrica SDK.
AppMetrica.activate(config);
```

Чтоб отправить собственную информацию о местоположении устройства в процессе работы приложения используйте
метод `AppMetrica.setLocation(location?: Location)`

```javascript translate=no
AppMetrica.setLocation(currentLocation);
```

## Отправка собственного события {#report-event}

Чтобы отправить собственное событие без вложенных параметров, передайте короткое название или описание события в
метод `AppMetrica.reportEvent(eventName: string, attributes?: Record<string, any>)`:

```javascript translate=no
AppMetrica.reportEvent("Updates installed");
```

## Отправка собственного события с вложенными параметрами {#report-event-params}

AppMetrica SDK позволяет отправлять собственные события с вложенными параметрами, которые могут быть заданы в формате
JSON. Для этого спользуйте метод `AppMetrica.reportEvent(eventName: string, attributes?: Record<string, any>)`:

```javascript translate=no
AppMetrica.reportEvent('My event', {foo: 'bar'});
```

Веб-интерфейс AppMetrica отображает до пяти уровней вложенности события. Если событие содержит шесть уровней и более, в
отчете отобразятся пять верхних. С помощью [API отчетов](../../../mobile-api/api_v1/intro.md) можно выгрузить до десяти
уровней.

Подробнее о событиях в разделе [События](../../../data-collection/about-events.md).

## Отправка собственного сообщения об ошибке {#send-report-error}

Чтобы отправить собственное сообщение об ошибке, используйте
метод `AppMetrica.reportError(identifier: string, message: string)`.

```javascript translate=no
try {
...
} catch (e: Error) {
  AppMetrica.reportError('my error', e.message);
}
```

Ошибки группируются по идентификатору. Не используйте переменные значения в качестве идентификатора для группировки.
Иначе количество групп будет увеличиваться и их будет сложно анализировать.

## Отправка событий из буфера {#send-events-buffer}

AppMetrica SDK не отправляет событие сразу после того, как оно произошло. Библиотека хранит данные о событиях в буфере. Метод `sendEventsBuffer` отправляет данные из буфера и очищает его. Используйте этот метод для принудительной отправки сохраненных событий после прохождения важных сценариев пользователя.

```javascript translate=no
AppMetrica.sendEventsBuffer();
```

{% note alert "" %}

Частое использование метода может привести к повышению энергопотребления и расходу интернет-трафика.

{% endnote %}

## Отслеживание жизненного цикла приложения вручную {#listen}

AppMetrica отслеживает границы сессии автоматически. При необходимости можно отключить автоматический трекинг сессий, передавая `false` в свойство `sessionsAutoTrackingEnabled` в расширенной конфигурации библиотеки.

```javascript translate=no
AppMetrica.activate({
  apiKey: API_KEY,
  sessionsAutoTracking: false
});
```

Для отслеживания жизненного цикла вручную используйте методы:

- Приостановка сессии:

    ```javascript translate=no 
    AppMetrica.pauseSession();
    ```

- Возобновление или начало новой сессии:

    ```javascript translate=no
    AppMetrica.resumeSession();
    ```

## Отправка ProfileId {#send-profile-id}

Если идентификатор пользовательского профиля известен до инициализации AppMetrica SDK, передавайте его до инициализации (`setUserProfileID`):

```javascript translate=no
AppMetrica.setUserProfileID('your-id');
AppMetrica.activate({apiKey: 'API_KEY'});
```

или во время инициализации с расширенной конфигурацией (`userProfileID`):

```javascript translate=no
AppMetrica.activate({
    apiKey: 'API_KEY',
    userProfileID: 'your-id',
});
```

В противном случае будет создан пользовательский профиль с идентификатором `appmetrica_device_id`.

{% note warning "" %}

Если отправка `ProfileId` не настроена, [предопределенные атрибуты](../../../data-collection/profile-attributes.md#pre-defined) не отображаются в веб-интерфейсе.

{% endnote %}

В любой момент можно обновить `ProfileId` с помощью вызова `setUserProfileID`:


```javascript translate=no
AppMetrica.setUserProfileID('your-id');
```

## Отправка атрибутов профиля {#send-attribute-profile}

Чтобы отправить атрибуты профиля, передайте в объект `UserProfile` необходимые атрибуты и отправьте этот объект с помощью метода `AppMetrica.reportUserProfile(userProfile: UserProfile)`. Атрибуты профиля создаются с помощью методов класса `Attributes`.

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

## Отправка ECommerce-событий {#send-ecommerce}

Для различных действий пользователя есть соответствующие типы ECommerce-событий. Чтобы создать конкретный тип события,
используйте нужный метод класса `ECommerce`.

Ниже приведены примеры отправки конкретных типов событий:

{% cut "Открытие страницы" %}

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
  searchQuery: 'даниссимо кленовый сироп',   // Optional.
  payload: payload,                          // Optional.
  categoriesPath: ['Акции', 'Красная цена'], // Optional.
};
const showScreen = ECommerce.showScreenEvent(screen);
// Sending an e-commerce event.
AppMetrica.reportECommerce(showScreen);
```

{% endcut %}

{% cut "Просмотр карточки товара" %}

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
  searchQuery: 'даниссимо кленовый сироп',   // Optional.
  payload: payload,                          // Optional.
  categoriesPath: ['Акции', 'Красная цена'], // Optional.
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
  name: 'Продукт творожный «Даниссимо» 5.9%, 130 г.',  // Optional.
  actualPrice: actualPrice, // Optional.
  originalPrice: originalPrice, // Optional.
  promocodes: ['BT79IYX', 'UT5412EP'],  // Optional.
  payload: payload,    // Optional.
  categoriesPath: ['Продукты', 'Молочные продукты', 'Йогурты'],  // Optional.
};
// Sending an e-commerce event.
AppMetrica.reportECommerce(ECommerce.showProductCardEvent(product, screen));
```

{% endcut %}

{% cut "Просмотр страницы товара" %}

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
  searchQuery: 'даниссимо кленовый сироп',   // Optional.
  payload: payload,                          // Optional.
  categoriesPath: ['Акции', 'Красная цена'], // Optional.
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
  name: 'Продукт творожный «Даниссимо» 5.9%, 130 г.',  // Optional.
  actualPrice: actualPrice, // Optional.
  originalPrice: originalPrice, // Optional.
  promocodes: ['BT79IYX', 'UT5412EP'],  // Optional.
  payload: payload,    // Optional.
  categoriesPath: ['Продукты', 'Молочные продукты', 'Йогурты'],  // Optional.
};

const referrer: ECommerceReferrer = {
  type: 'button',
  identifier: '76890',
  screen: screen,
};

const showProductDetails = ECommerce.showProductDetailsEvent(product, referrer);
// Sending an e-commerce event.
AppMetrica.reportECommerce(showProductDetails);
```

{% endcut %}

{% cut "Добавление или удаление товара из корзины" %}

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
  searchQuery: 'даниссимо кленовый сироп',   // Optional.
  payload: payload,                          // Optional.
  categoriesPath: ['Акции', 'Красная цена'], // Optional.
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
  name: 'Продукт творожный «Даниссимо» 5.9%, 130 г.',  // Optional.
  actualPrice: actualPrice, // Optional.
  originalPrice: originalPrice, // Optional.
  promocodes: ['BT79IYX', 'UT5412EP'],  // Optional.
  payload: payload,    // Optional.
  categoriesPath: ['Продукты', 'Молочные продукты', 'Йогурты'],  // Optional.
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
// Sending an e-commerce event.
AppMetrica.reportECommerce(addCartItem);

const removeCartItem = ECommerce.removeCartItemEvent(ecommerceCartItem);
// Sending an e-commerce event.
AppMetrica.reportECommerce(removeCartItem);
```

{% endcut %}

{% cut "Начало оформления и завершение покупки" %}

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
  searchQuery: 'даниссимо кленовый сироп',   // Optional.
  payload: payload,                          // Optional.
  categoriesPath: ['Акции', 'Красная цена'], // Optional.
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
  name: 'Продукт творожный «Даниссимо» 5.9%, 130 г.',  // Optional.
  actualPrice: actualPrice, // Optional.
  originalPrice: originalPrice, // Optional.
  promocodes: ['BT79IYX', 'UT5412EP'],  // Optional.
  payload: payload,    // Optional.
  categoriesPath: ['Продукты', 'Молочные продукты', 'Йогурты'],  // Optional.
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
// Sending an e-commerce event.
AppMetrica.reportECommerce(beginCheckout);

const purchase = ECommerce.purchaseEvent(order);
// Sending an e-commerce event.
AppMetrica.reportECommerce(purchase);
```

{% endcut %}

## Отправка событий Revenue {#send-revenue}

{% cut "С валидацией" %}

AppMetrica поддерживает валидацию покупок, которые реализованы с помощью библиотек [Google Play Billing](https://developer.android.com/google/play/billing/billing_overview) и [StoreKit](https://developer.apple.com/documentation/storekit).

Чтобы покупки валидировались, настройте отправку объекта `Receipt` вместе с `Revenue`:

- Для Android в `Receipt` передавайте [originalJson](https://developer.android.com/reference/com/android/billingclient/api/Purchase#getOriginalJson()) в `receiptData` и [signature](https://developer.android.com/reference/com/android/billingclient/api/Purchase#getSignature()) в свойство `signature`.

- Для iOS в собственной реализации завершения транзакции настройте отправку полей `transactionID` и `receiptData`.

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

{% cut "Без валидации" %}

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

## Отправка событий Ad Revenue {#send-adrevenue}

```javascript translate=no
import AppMetrica, {
  AdRevenue,
  AdType
} from '@appmetrica/react-native-analytics';
```

Создайте объект `AdRevenue`:

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

Отправьте объект `AdRevenue` с помощью метода `AppMetrica.reportAdRevenue(adRevenue: AdRevenue)`:

```javascript translate=no
AppMetrica.reportAdRevenue(adRevenue);
```

## Установка длительности тайм-аута сессии {#session-timeout}

По умолчанию длительность тайм-аута сессии равна 10 секундам. Это минимально допустимое значение
параметра `sessionTimeout`.

Чтобы изменить длительность тайм-аута, передайте значение в секундах в метод `sessionTimeout` при создании расширенной
конфигурации библиотеки.

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

## Установка версии приложения {#version-app}

Чтобы указать версию приложения из кода, передайте версию приложения в свойство `appVersion` при
создании расширенной конфигурации библиотеки.

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

где `1.0` — версия приложения.

## Определение уровня API библиотеки (Android) {#level-api-android}

Чтобы определить уровень API библиотеки из кода приложения, используйте метод `AppMetrica.getLibraryApiLevel()`.

```javascript translate=no
const [libraryApiLevel, setLibraryApiLevel] = useState('???');
AppMetrica.getLibraryApiLevel().then(level => {
  setLibraryApiLevel(level);
});
```

## Определение версии библиотеки {#version-sdk}

Чтобы определить версию библиотеки из кода приложения, используйте метод `AppMetrica.getLibraryVersion()`.

```javascript translate=no
const [appMetricaVersion, setAppMetricaVersion] = useState('???');
AppMetrica.getLibraryVersion().then(version => {
  setAppMetricaVersion(version);
});
```

## Отслеживание открытий приложения с помощью deeplink {#deeplink}

Отслеживание открытий deeplink работает по умолчанию. Выключить отслеживание можно в расширенной конфигурации:

```javascript translate=no
  // Creating an extended library configuration.
const config: AppMetricaConfig = {
  apiKey: API_KEY,
  appOpenTrackingEnabled: false,
};
// Initializing the AppMetrica SDK.
AppMetrica.activate(config);
```

При необходимости вы можете вручную отправить в AppMetrica информацию об открытии приложения диплинком
методом `reportAppOpen()`:

```javascript translate=no
AppMetrica.reportAppOpen(deeplink);
```

См. также [Как создать ремаркетинг-кампанию в AppMetrica](../../../troubleshooting/troubleshooting.md#remarketing-campaign).

## Запрос отложенного deeplink {#deferreddeeplink-request}

Чтобы запросить отложенный deeplink, передайте в метод `AppMetrica.requestDeferredDeeplink(listener: DeferredDeeplinkListener)` объект, реализующий интерфейс `DeferredDeeplinkListener`. Метод возвращает отложенный deeplink только при первом запуске приложения после получения Google Play Install Referrer.

```javascript translate=no
const deferredDeeplinkListener: DeferredDeeplinkListener = {
  onSuccess: (deeplink: string) => {
    console.log('Deferred deeplink:', deeplink);
  },
  onFailure: (error: DeferredDeeplinkError, referrer?: string) => {
    console.log(`Deferred deeplink error: ${error}, referrer: ${referrer}`);
  },
};
AppMetrica.requestDeferredDeeplink(deferredDeeplinkListener);
```

Подробнее об отложенных deeplinks в разделе [Поддержка отложенных deeplinks](../../android/analytics/android-deferred-deeplinks.md).

## Запрос параметров отложенного deeplink {#deferreddeeplink-parameters-request}

Чтобы запросить параметры отложенного deeplink, передайте в метод `AppMetrica.requestDeferredDeeplinkParameters(listener: DeferredDeeplinkParametersListener)` объект, реализующий интерфейс `DeferredDeeplinkParametersListener`. Метод возвращает параметры отложенного deeplink только при первом запуске приложения после получения Google Play Install Referrer.

```javascript translate=no
const deferredDeeplinkParametersListener: DeferredDeeplinkParametersListener = {
  onSuccess: (parameters: Record<string, string>) => {
    console.log('Deferred deeplink parameters:', parameters); // или JSON.stringify(parameters)
  },
  onFailure: (error: DeferredDeeplinkError, referrer?: string) => {
    console.log(`Deferred deeplink parameters error: ${error}, referrer: ${referrer}`);
  },
};
AppMetrica.requestDeferredDeeplinkParameters(deferredDeeplinkParametersListener);
```

Подробнее об отложенных deeplinks в разделе [Поддержка отложенных deeplinks](../../android/analytics/android-deferred-deeplinks.md).


## Учет новых пользователей {#new-user}

По умолчанию в момент первого запуска приложения все пользователи определяются как новые. Если AppMetrica SDK
подключается к приложению, у которого уже есть активные пользователи, то для корректного отслеживания статистики можно
настроить учет новых и старых пользователей. Для этого необходимо инициализировать AppMetrica SDK, используя расширенную
стартовую конфигурацию `AppMetricaConfig`:

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

## Отключение и включение отправки статистики {#stat}

Если для отправки статистических данных требуется согласие пользователя, необходимо инициализировать библиотеку с
отключенной опцией отправки статистики. Для этого передайте значение `false` в свойство `statisticsSending` при создании
расширенной конфигурации библиотеки.

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

После того как пользователь дал согласие на отправку статистики (например, в настройках приложения или в соглашении при
первом открытии), включите отправку статистики с помощью метода `AppMetrica.setDataSendingEnabled(true)`:

```javascript translate=no
// Checking the status of the boolean variable. It shows the user confirmation.
if (flag) {
  // Enabling sending data.
  AppMetrica.setDataSendingEnabled(true);
}
```

### Пример оповещения {#stat-alert-example}

Для информирования пользователей вы можете использовать любой текст. Например:

> Это приложение использует сервис аналитики AppMetrica, предоставляемый компанией ООО «ЯНДЕКС», 119021, Россия,Москва,
> ул. Л. Толстого, 16 (далее — Яндекс) на [Условиях использования сервиса](https://yandex.ru/legal/metrica_termsofuse/).
>
> AppMetrica анализирует данные об использовании приложения, в том числе об устройстве, на котором оно функционирует,
> источнике установки, составляет конверсию и статистику вашей активности в целях продуктовой аналитики, анализа и
> оптимизации рекламных кампаний, а также для устранения ошибок. Собранная таким образом информация не может
> идентифицировать вас.
>
> Информация об использовании вами данного приложения, собранная при помощи инструментов AppMetrica, в обезличенном виде
> будет передаваться Яндексу и храниться на сервере Яндекса в ЕС и Российской Федерации. Яндекс будет обрабатывать эту
> информацию для предоставления статистики использования вами приложения, составления для нас отчетов о работе приложения,
> и предоставления других услуг.

## Получение различных идентификаторов AppMetrica SDK {#get-ids}

Чтобы получить различные идентификаторы AppMetrica SDK (`DeviceId`, `DeviceIdHash`, `UUID`) используйте
метод `requestStartupParams()`. Для получения `appmetrica_device_id` нужно запрашивать `DeviceIdHash`.

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
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
