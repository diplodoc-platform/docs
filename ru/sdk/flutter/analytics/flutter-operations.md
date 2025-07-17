# Примеры использования методов

## Инициализация библиотеки с расширенной конфигурацией {#initialize}

Чтобы инициализировать библиотеку с расширенной стартовой конфигурацией, передайте объект типа `AppMetricaConfig` с необходимыми настройками и активируйте библиотеку с помощью метода `AppMetrica.activate(AppMetricaConfig config)`. С помощью расширенной конфигурации можно, например, включить или отключить логирование, установить тайм-аут сессии, передать параметры для отслеживания предустановленных приложений.

Настройки расширенной конфигурации применяются с момента инициализации библиотеки.

```java translate=no
AppMetrica.activate(
      AppMetricaConfig(API_KEY, logs: true
          // ...
          ));
```

## Отправка статистики на дополнительный API key {#reporter-different-apikey}

Отправка данных на дополнительный API key позволяет собирать для каждого API key свою статистику. Это можно использовать для управления доступом к информации. Например, чтобы предоставить доступ к статистике для аналитиков, можно продублировать отправку маркетинговых данных на дополнительный API key и предоставить им доступ к этой статистике. Так у них будет доступ только к той информации, которая им необходима.

Для отправки данных на дополнительный API key необходимо использовать репортеры. С помощью них можно отправлять события, сообщения об ошибках, профили и информацию о покупках в приложении. Репортеры могут работать без инициализации AppMetrica SDK.

### Шаг 1. (Опционально) Инициализируйте репортер с расширенной конфигурацией {#reporter-different-apikey-initialize}

Чтобы инициализировать репортер с расширенной конфигурацией, создайте объект класса `AppMetricaReporterConfig` с необходимыми настройками и активируйте репортер с помощью метода `AppMetrica.activateReporter(AppMetricaReporterConfig reporterConfig)`. Конфигурация применяется для репортера с указанным API key. Для каждого дополнительного API key можно настроить свою конфигурацию.

{% note alert %}

Инициализацию репортера с расширенной конфигурацией необходимо проводить до первого обращения к репортеру. Иначе репортер будет инициализирован без конфигурации.

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

### Шаг 2. Настройте отправку данных с помощью репортера {#reporter-different-apikey-send}

Для отправки данных с помощью репортера, необходимо получить объект, который реализует абстрактный класс `AppMetricaReporter` с помощью метода `AppMetrica.getReporter(String apiKey)`, и использовать методы интерфейса для отправки отчетов. Если репортер не был инициализирован с расширенной конфигурацией, то вызов данного метода произведет инициализацию репортера для указанного API key.

Пример отправки события:

```dart translate=no
AppMetrica.getReporter("ANOTHER_API_KEY").reportEvent("Updates installed");
```

Для корректного отслеживания сессий взаимодействия пользователя с приложением настройте отправку событий о начале и приостановке сессии для каждого репортера. Для этого используйте методы `resumeSession()` и `pauseSession()`:

```dart translate=no
AppMetricaReporter reporter = AppMetrica.getReporter("ANOTHER_API_KEY");
reporter.resumeSession();
reporter.reportEvent("Updates installed");
reporter.pauseSession();
```

## Отправка местоположения устройства библиотекой {#track-location}

Для Android отправка местоположения устройства по умолчанию отключена. Чтобы включить отправку, инициализируйте библиотеку с конфигурацией, в которой отправка информации о местоположении устройства включена. Для этого при создании расширенной конфигурации библиотеки укажите свойство `locationTracking` равным `true`:

```java translate=no
AppMetrica.activate(AppMetricaConfig(API_KEY,
	locationTracking: true));
```

Чтобы включить отправку в процессе работы приложения, используйте метод `AppMetrica.setLocationTracking(bool enabled)`:

```java translate=no
AppMetrica.setLocationTracking(true);
```

Для более точного определения местоположения добавьте в файл AndroidManifest.xml одно из следующих разрешений:

- `android.permission.ACCESS_COARSE_LOCATION` — для приблизительного определения;
- `android.permission.ACCESS_FINE_LOCATION` — для точного определения.

## Установка местоположения вручную {#location-manual}

Перед отправкой собственной информации о местоположении устройства убедитесь, что отправка отчетов включена.

Библиотека определяет местоположение устройства самостоятельно. Чтобы отправить собственную информацию о местоположении устройства, передайте `AppMetricaLocation` в метод `AppMetrica.setLocation(AppMetricaLocation? location)`:

```java translate=no
// Determining the location.
AppMetricaLocation location = AppMetricaLocation(latitude, longitude);
// Setting your own location information of the device.
AppMetrica.setLocation(location);
```

Чтобы отправить собственную информацию о местоположении устройства с помощью расширенной конфигурации, при создании расширенной конфигурации библиотеки передайте объект типа `AppMetricaLocation` в свойство `location`:

```java translate=no
AppMetricaLocation location = AppMetricaLocation(latitude, longitude);
AppMetrica.activate(AppMetricaConfig(API_KEY,
	location: location));
```

## Отправка собственного события {#report-event}

Чтобы отправить собственное событие без вложенных параметров, передайте короткое название или описание события в метод `AppMetrica.reportEvent(String eventName)`:

```dart translate=no
AppMetrica.reportEvent("eventName");
```

## Отправка собственного события с вложенными параметрами {#report-event-params}

Чтобы передать параметры в формате JSON:

```dart translate=no
String jsonAttributes = '{"item":"book","price":9.99}';

AppMetrica.reportEventWithJson("Purchase", jsonAttributes);
```

Чтобы передать параметры в формате Map:

```dart translate=no
Map<String, dynamic> attributesMap = {"item": "book", "price": 9.99};
AppMetrica.reportEventWithMap("Purchase", attributesMap);
```

## Отправка собственного сообщения об ошибке {#send-report-error}

Чтобы отправить собственное сообщение об ошибке, используйте метод:

```dart translate=no
AppMetrica.reportError(
  message: "Error occurred",
  errorDescription: AppMetricaErrorDescription(StackTrace.current),
);
```

Для отправки сообщения об ошибке с идентификатором группы:

```dart translate=no
AppMetrica.reportErrorWithGroup(
  "IDENTIFIER",
  message: "MESSAGE",
  errorDescription: AppMetricaErrorDescription(StackTrace.current),
);
```

## Отправка событий из буфера {#send-events-buffer}

AppMetrica SDK не отправляет событие сразу после того, как оно произошло. Библиотека хранит данные о событиях в буфере. Метод `sendEventsBuffer` отправляет данные из буфера и очищает его. Используйте этот метод для принудительной отправки сохраненных событий после прохождения важных сценариев пользователя.

```dart translate=no
AppMetrica.sendEventsBuffer();
```

{% note alert "" %}

Частое использование метода может привести к повышению энергопотребления и расходу интернет-трафика.

{% endnote %}

## Отслеживание жизненного цикла приложения вручную {#listen}

AppMetrica отслеживает границы сессии автоматически. При необходимости можно отключить автоматический трекинг сессий, передавая `false` в свойство `sessionsAutoTrackingEnabled` в расширенной конфигурации библиотеки.

```dart translate=no
AppMetrica.activate(
    AppMetricaConfig(API_KEY, sessionsAutoTrackingEnabled: false));
```

Для отслеживания жизненного цикла вручную используйте методы:

- Приостановка сессии:

    ```dart translate=no
    AppMetrica.pauseSession();
    ```

- Возобновление или начало новой сессии:

    ```dart translate=no
    AppMetrica.resumeSession();
    ```

## Отслеживание аварийных остановок приложения {#set-report-crash}

Отчеты об аварийных остановках приложения отправляются по умолчанию.

Чтобы отключить автоматическое отслеживание, инициализируйте библиотеку с конфигурацией, в которой отправка информации об аварийных остановках приложения отключена. Для этого передайте значение `false` в свойства `crashReporting` и `flutterCrashReporting` при создании расширенной конфигурации.

```dart translate=no
AppMetrica.activate(AppMetricaConfig("daa46e63-d4a6-46d1-bbf9-0dcf4b482b83",
    // Disabling the data sending about the native android/ios crashes.
    crashReporting: false,
    // Disabling the data sending about the Flutter crashes.
    flutterCrashReporting: false));
```

## Отслеживание аварийных остановок приложения вручную {#report-unhandled}

Отчеты об аварийных остановках приложения отправляются по умолчанию. Чтобы избежать дублирования событий при ручной отправке, необходимо отключить автоматическое отслеживание аварийных остановок.

Чтобы отправлять информацию об аварийных остановках приложения вручную, используйте метод `AppMetrica.reportUnhandledException(AppMetricaErrorDescription errorDescription)`:

```dart translate=no
AppMetrica.reportUnhandledException(
  AppMetricaErrorDescription.fromCurrentStackTrace(
      message: 'Error message', type: 'Error type'),
);
```

## Отправка ProfileId {#send-profile-id}

Если идентификатор пользовательского профиля известен до инициализации AppMetrica SDK, передавайте его до инициализации (`setUserProfileID`) или во время инициализации с расширенной конфигурацией (`withUserProfileID`).

В противном случае будет создан технический профиль с идентификатором `appmetrica_device_id`.

В любой момент можно обновить `ProfileId` с помощью вызова `setUserProfileID`:

```dart translate=no
AppMetrica.setUserProfileID("id");
```

## Отправка атрибутов профиля {#send-attribute-profile}

Чтобы отправить атрибуты профиля, передайте в метод `AppMetrica.reportUserProfile(UserProfile)` объект класса `UserProfile`.

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

## Отправка ECommerce-событий {#send-ecommerce}

В AppMetrica нет возможности сегментировать ECommerce-события на «тестовые» и «не тестовые». Если для отладки покупок вы используете основной API key, то тестовые события будут попадать в общую статистику. Поэтому чтобы отладить отправку ECommerce-событий, используйте отправку статистики на дополнительный API key с помощью репортера.

### Шаг 1. Создайте тестовое приложение в AppMetrica {#send-ecommerce-test}

Заполните параметры приложения: ссылка в магазине приложений (если приложение еще не опубликовано — оставьте поле пустым), название, категория, часовой пояс для построения отчетов.

Чтобы добавить еще одно приложение, нажмите кнопку [Добавить приложение](https://appmetrika.yandex.{{ domain }}/application/new) в выпадающем списке в интерфейсе AppMetrica.

### Шаг 2. Настройте отправку ECommerce-событий на тестовый API key {#send-ecommerce-test-key}

Для различных действий пользователя есть соответствующие типы ECommerce-событий. Чтобы создать конкретный тип события, используйте нужный метод класса AppMetricaECommerce.

Ниже приведены примеры отправки конкретных типов событий.

{% cut "Открытие страницы" %}

```dart translate=no
Map<String, String> payload = {
  "configuration": "landscape",
  "full_screen": "true",
};
// Creating a screen object.
AppMetricaECommerceScreen screen = AppMetricaECommerceScreen(
    name: "ProductCardActivity", // Optional.
    searchQuery: "даниссимо кленовый сироп", // Optional.
    payload: payload, // Optional.
    categoriesPath: ["Акции", "Красная цена"] // Optional.
    );
AppMetricaECommerceEvent showScreenEvent = AppMetricaECommerce.showScreenEvent(screen);
// Sending an e-commerce event.
AppMetrica.getReporter("Testing API key").reportECommerce(showScreenEvent);
```

{% endcut %}

{% cut "Просмотр карточки товара" %}

```dart translate=no
Map<String, String> payload = {
  "configuration": "landscape",
  "full_screen": "true"
};
// Creating a screen object.
AppMetricaECommerceScreen screen = AppMetricaECommerceScreen(
    name: "ProductCardActivity", // Optional.
    searchQuery: "даниссимо кленовый сироп", // Optional.
    payload: payload, // Optional.
    categoriesPath: ["Акции", "Красная цена"] // Optional.
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
    name: "Продукт творожный «Даниссимо» 5.9%, 130 г.", // Optional.
    actualPrice: actualPrice, // Optional.
    originalPrice: originalPrice, // Optional.
    promocodes: ["BT79IYX", "UT5412EP"], // Optional.
    payload: payload, // Optional.
    categoriesPath: [
      "Продукты",
      "Молочные продукты",
      "Йогурты"
    ] // Optional.
    );
AppMetricaECommerceEvent showProductCardEvent =
    AppMetricaECommerce.showProductCardEvent(product, screen);
// Sending an e-commerce event.
AppMetrica.getReporter("Testing API key")
    .reportECommerce(showProductCardEvent);
```

{% endcut %}

{% cut "Просмотр страницы товара" %}

```dart translate=no
Map<String, String> payload = {
  "configuration": "landscape",
  "full_screen": "true"
};
// Creating a screen object.
AppMetricaECommerceScreen screen = AppMetricaECommerceScreen(
    name: "ProductCardActivity", // Optional.
    searchQuery: "даниссимо кленовый сироп", // Optional.
    payload: payload, // Optional.
    categoriesPath: ["Акции", "Красная цена"] // Optional.
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
    name: "Продукт творожный «Даниссимо» 5.9%, 130 г.", // Optional.
    actualPrice: actualPrice, // Optional.
    originalPrice: originalPrice, // Optional.
    promocodes: ["BT79IYX", "UT5412EP"], // Optional.
    payload: payload, // Optional.
    categoriesPath: [
      "Продукты",
      "Молочные продукты",
      "Йогурты"
    ] // Optional.
    );
AppMetricaECommerceEvent showProductDetailsEvent =
    AppMetricaECommerce.showProductDetailsEvent(product, screen);
// Sending an e-commerce event.
AppMetrica.getReporter("Testing API key")
    .reportECommerce(showProductDetailsEvent);
```

{% endcut %}

{% cut "Добавление или удаление товара из корзины" %}

```dart translate=no
Map<String, String> payload = {
  "configuration": "landscape",
  "full_screen": "true"
};
// Creating a screen object.
AppMetricaECommerceScreen screen = AppMetricaECommerceScreen(
    name: "ProductCardActivity", // Optional.
    searchQuery: "даниссимо кленовый сироп", // Optional.
    payload: payload, // Optional.
    categoriesPath: ["Акции", "Красная цена"] // Optional.
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
    name: "Продукт творожный «Даниссимо» 5.9%, 130 г.", // Optional.
    actualPrice: actualPrice, // Optional.
    originalPrice: originalPrice, // Optional.
    promocodes: ["BT79IYX", "UT5412EP"], // Optional.
    payload: payload, // Optional.
    categoriesPath: [
      "Продукты",
      "Молочные продукты",
      "Йогурты"
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

{% cut "Начало оформления и завершение покупки" %}

```dart translate=no
Map<String, String> payload = {
  "configuration": "landscape",
  "full_screen": "true"
};
// Creating a screen object.
AppMetricaECommerceScreen screen = AppMetricaECommerceScreen(
    name: "ProductCardActivity", // Optional.
    searchQuery: "даниссимо кленовый сироп", // Optional.
    payload: payload, // Optional.
    categoriesPath: ["Акции", "Красная цена"] // Optional.
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
    name: "Продукт творожный «Даниссимо» 5.9%, 130 г.", // Optional.
    actualPrice: actualPrice, // Optional.
    originalPrice: originalPrice, // Optional.
    promocodes: ["BT79IYX", "UT5412EP"], // Optional.
    payload: payload, // Optional.
    categoriesPath: [
      "Продукты",
      "Молочные продукты",
      "Йогурты"
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

### Шаг 3. Проверьте отчет тестового приложения {#send-ecommerce-check-reports}

Совершите тестовые покупки в приложении. Через некоторое время в интерфейсе AppMetrica проверьте отчет «Ecommerce». Убедитесь, что ECommerce-события отображаются в отчете. Подробнее об отчете в разделе [Ecommerce](../../../mobile-reports/ecommerce-report.md).

### Шаг 4. Настройте отправку ECommerce на основной API Key {#send-ecommerce-key}

После успешного тестирования настройте отправку ECommerce-событий на основной API key.

Чтобы отправить объект `AppMetricaECommerceEvent` на основной API key, используйте метод `AppMetrica.reportECommerce(AppMetricaECommerceEvent event)`:

```dart translate=no
...
// Sending an e-commerce event.
AppMetrica.reportECommerce(ecommerceEvent);
```

## Отправка In-App покупок {#send-revenue}

{% cut "С валидацией" %}

Чтобы покупки Android валидировались, настройте отправку объекта `Revenue.Receipt` вместе с Revenue, а для iOS настройте отправку поля `transactionID`.

1. Создайте объект `AppMetricaReceipt` с информацией о покупке и подписью.
2. Создайте объект `AppMetricaRevenue` и передайте в него `AppMetricaReceipt` и `transactionID`.
3. Отправьте объект `AppMetricaRevenue` с помощью метода `AppMetrica.reportRevenue(AppMetricaRevenue revenue)`.

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

{% cut "Без валидации" %}

1. Создайте объект `AppMetricaRevenue`.

2. (Опционально) Чтобы группировать покупки по `OrderID`, передайте его в свойство `payload`.

{% note info "Примечание" %}

Если идентификатор `OrderID` не указан, AppMetrica генерирует идентификатор автоматически.

{% endnote %}

3. Отправьте объект `AppMetricaRevenue` с помощью метода `AppMetrica.reportRevenue(AppMetricaRevenue revenue)`.

```java translate=no
AppMetricaRevenue revenue = AppMetricaRevenue(Decimal.parse("100.100"), "USD",
	quantity: 2,
	productId: "com.yandex.service.299",
	payload: """{"OrderID":"Identifier", "source":"Google Play"}""");
AppMetrica.reportRevenue(revenue);
```

{% endcut %}

## Отправка Ad Revenue {#send-adrevenue}

В AppMetrica можно передавать данные о выручке от показов рекламы (Ad Revenue).

### Шаг 1. Убедитесь, что SDK активирован {#send-adrevenue-active}

Пример активации:

```dart translate=no
AppMetricaConfig config = AppMetricaConfig("API_KEY");
AppMetrica.activate(config);
```

### Шаг 2. Настройте отправку Ad Revenue {#send-adrevenue-send}

1. Создайте объект класса `AppMetricaAdRevenue`.

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

2. Отправьте объект `AppMetricaAdRevenue` используя метод `reportAdRevenue(AppMetricaAdRevenue adRevenue)`.

    ```dart translate=no
    AppMetrica.reportAdRevenue(adRevenue);
    ```

### Шаг 3. Убедитесь, что Ad Revenue отображается в отчетах {#send-adrevenue-check-reports}

1. Совершите просмотры рекламы в приложении.

2. Убедитесь, что в отчете [In-app и Ad Revenue](../../../mobile-reports/revenue-report.md) количество событий Ad Revenue соответствует количеству просмотров рекламы.

## Отслеживание открытий приложения с помощью deeplink {#deeplink}

Отслеживание открытий осуществляется с помощью метода `reportAppOpen(String deeplink)`:

```dart translate=no
AppMetrica.reportAppOpen(deeplink);
```

## Установка длительности тайм-аута сессии {#session-timeout}

По умолчанию длительность тайм-аута сессии равна 10 секундам. Это минимально допустимое значение параметра `sessionTimeout`.

Чтобы изменить длительность тайм-аута, передайте значение в секундах в свойство `sessionTimeout` при создании расширенной конфигурации библиотеки.

```dart translate=no
AppMetrica.activate(
    AppMetricaConfig(API_KEY, sessionTimeout: 15));
```

## Установка версии приложения {#version-app}

Чтобы вручную указать версию приложения из кода, передайте версию приложения в свойство `appVersion` при создании расширенной конфигурации библиотеки.

```dart translate=no
AppMetrica.activate(
    AppMetricaConfig(API_KEY, appVersion: "1.13.2"));
```

где `1.13.2` — версия приложения.


## Определение уровня API библиотеки (Android) {#level-api-android}

Чтобы определить уровень API библиотеки из кода приложения, используйте свойство `libraryApiLevel`.

```dart translate=no
int apiLevel;
AppMetrica.libraryApiLevel.then((value) => {apiLevel = value});
```

## Определение версии библиотеки {#version-sdk}

Чтобы определить версию библиотеки из кода приложения, используйте метод `AppMetrica.GetLibraryVersion()`.

```dart translate=no
String version;
AppMetrica.libraryVersion.then((value) => {version = value});
```

## Запрос отложенного deeplink {#deferreddeeplink-request}

Чтобы запросить отложенный deeplink, вызывайте метод `AppMetrica.requestDeferredDeeplink()`. Отложенный deeplink можно запросить только при первом запуске приложения после получения Google Play Install Referrer.

```dart translate=no
AppMetrica.requestDeferredDeeplink()
    .then((value) => {
          // Processing deferred deeplink.
        })
    .onError((error, stackTrace) => {
          // Handling the error.
        });
```

Подробнее об отложенных deeplinks в разделе [{#T}](../../android/analytics/android-deferred-deeplinks.md).

## Запрос параметров отложенного deeplink {#deferreddeeplink-parameters-request}

Чтобы запросить параметры отложенного deeplink, вызовите метод `AppMetrica.requestDeferredDeeplinkParameters()`. Параметры отложенного deeplink можно запросить только при первом запуске приложения после получения Google Play Install Referrer.

```dart translate=no
AppMetrica.requestDeferredDeeplinkParameters()
    .then((value) => {
          // Processing deeplink parameters.
        })
    .onError((error, stackTrace) => {
          // Handling the error.
        });
```

Подробнее об отложенных deeplinks в разделе [{#T}](../../android/analytics/android-deferred-deeplinks.md).

## Учет новых пользователей {#new-user}

По умолчанию в момент первого запуска приложения все пользователи определяются как новые. Если AppMetrica SDK подключается к приложению, у которого уже есть активные пользователи, то для корректного отслеживания статистики можно настроить учет новых и старых пользователей. Для этого необходимо инициализировать AppMetrica SDK, используя расширенную стартовую конфигурацию `AppMetricaConfig`:

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

## Отключение и включение отправки статистики {#stat}

Если для отправки статистических данных требуется согласие пользователя, необходимо инициализировать библиотеку с отключенной опцией отправки статистики. Для этого передайте значение `false` в свойство `dataSendingEnabled` при создании расширенной конфигурации библиотеки.

```dart translate=no
AppMetrica.activate(
    AppMetricaConfig(API_KEY, dataSendingEnabled: false));
```

После того как пользователь дал согласие на отправку статистики (например, в настройках приложения или в соглашении при первом открытии), включите отправку статистики с помощью метода `AppMetrica.setDataSendingEnabled(bool enabled)`:

```dart translate=no
// Checking the status of the boolean variable. It shows the user confirmation.
if (flag) {
  // Enabling sending data.
  AppMetrica.setDataSendingEnabled(true);
}
```

### Пример оповещения {#stat-example}

Для информирования пользователей вы можете использовать любой текст. Например:

Это приложение использует сервис аналитики AppMetrica, предоставляемый компанией ООО «ЯНДЕКС», 119021, Россия,Москва, ул. Л. Толстого, 16 (далее — Яндекс) на [Условиях использования сервиса](https://yandex.ru/legal/metrica_termsofuse/?lang={{locale}}).

AppMetrica анализирует данные об использовании приложения, в том числе об устройстве, на котором оно функционирует, источнике установки, составляет конверсию и статистику вашей активности в целях продуктовой аналитики, анализа и оптимизации рекламных кампаний, а также для устранения ошибок. Собранная таким образом информация не может идентифицировать вас.

Информация об использовании вами данного приложения, собранная при помощи инструментов AppMetrica, в обезличенном виде будет передаваться Яндексу и храниться на сервере Яндекса в ЕС и Российской Федерации. Яндекс будет обрабатывать эту информацию для предоставления статистики использования вами приложения, составления для нас отчетов о работе приложения и предоставления других услуг.


## Получение различных идентификаторов AppMetrica SDK {#get-ids}

Чтобы получить различные идентификаторы AppMetrica SDK (`DeviceId`, `DeviceIdHash`, `UUID`) используйте метод `requestStartupParams()`. Для получения `appmetrica_device_id` нужно запрашивать `DeviceIdHash`.

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
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
