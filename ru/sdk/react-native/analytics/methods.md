# Справочник методов

## Types

```javascript 
// Содержит расширенную конфигурацию запуска библиотеки.
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
  nativeCrashReporting?: boolean, // Android only.
  activationAsSessionStart?: boolean, // iOS only.
  sessionsAutoTracking?: boolean,
  userProfileID?: string,
  errorEnvironment?: Record<string, string | undefined>,
  appEnvironment?: Record<string, string | undefined>,
  maxReportsCount?: number,
  dispatchPeriodSeconds?: number,
}

// Тип содержит информацию для трекинга предустановленных приложений.
export type PreloadInfo = {
  trackingId: string,
  additionalInfo?: Record<string, string>,
}

// Тип содержит информацию о местоположении устройства.
export type Location = {
  latitude: number,
  longitude: number,
  altitude?: number,
  accuracy?: number,
  course?: number,
  speed?: number,
  timestamp?: number,
}

// Содержит возможные ошибки метода requestStartupParams().
export type StartupParamsReason = 'UNKNOWN' | 'NETWORK' | 'INVALID_RESPONSE';

// Содержит идентификаторы, получаемые методом requestStartupParams().
export type StartupParams = {
  deviceIdHash?: string,
  deviceId?: string,
  uuid?: string,
}

// Callback, который передается в метод requestStartupParams().
type StartupParamsCallback = (
  params?: StartupParams,
  reason?: StartupParamsReason
) => void

// Тип содержит информацию об экране, на котором происходит ecommerce событие.
export type ECommerceScreen = {
  name: string,
  searchQuery?: string,
  payload?: Map<string, string>,
  categoriesPath?: Array<string>,
}

// Содержит информацию о валюте и стоимости.
export type ECommerceAmount = {
  amount: number | string,
  unit: string,
}

// Содержит информацию о цене.
export type ECommercePrice = {
  amount: ECommerceAmount,
  internalComponents?: Array<ECommerceAmount>,
}

// Содержит информацию об отдельном товаре.
export type ECommerceProduct = {
  sku: string,
  name?: string,
  actualPrice?: ECommercePrice,
  originalPrice?: ECommercePrice,
  promocodes?: Array<string>,
  categoriesPath?: Array<string>,
  payload?: Map<string, string>,
}

// Содержит информацию об источнике, который привел к товару.
export type ECommerceReferrer = {
  type?: string,
  identifier?: string,
  screen?: ECommerceScreen,
}

// Содержит информацию о позиции в корзине, о количестве товара и его стоимости.
export type ECommerceCartItem = {
  product: ECommerceProduct,
  price: ECommercePrice,
  quantity: number | string,
  referrer?: ECommerceReferrer,
}

// Содержит информацию о заказе.
export type ECommerceOrder = {
  orderId: string,
  products: Array<ECommerceCartItem>,
  payload?: Map<string, string>,
}

// Тип для отправки in-app покупок из приложения. Содержит информацию о доходе.
export type Revenue = {
  price: number,
  currency: string,
  productID?: string,
  quantity?: number,
  payload?: string,
  receipt?: Receipt,
}

// Используется для валидации in-app покупок.
export type Receipt = {
  transactionID?: string,
  receiptData?: string,
  signature?: string,
}

// Содержит информацию о доходе с рекламы.
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

// Содержит возможные значения для GenderAttribute
export type UserProfileGender = 'male' | 'female' | 'other';

// Содержит расширенную конфигурацию репортера.
export type ReporterConfig = {
  apiKey: string,
  logs?: boolean,
  maxReportsInDatabaseCount?: number,
  sessionTimeout?: number,
  dataSendingEnabled?: boolean,
  appEnvironment?: Record<string, string | undefined>,
  dispatchPeriodSeconds?: number,
  userProfileID?: string,
  maxReportsCount?: number,
}

// Содержит возможные ошибки методов requestDeferredDeeplink() и requestDeferredDeeplinkParameters().
export type DeferredDeeplinkError = 'NO_REFERRER' | 'NOT_A_FIRST_LAUNCH' | 'PARSE_ERROR' | 'UNKNOWN';
```

## Enums

```javascript 
// Содержит возможные типы рекламы для отправки AdRevenue.
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

Основной класс для использования библиотеки.

```javascript 
// Инициализирует библиотеку с расширенной конфигурацией.
activate(config: AppMetricaConfig)

// Возвращает текущую версию библиотеки.
async getLibraryVersion(): string

// Сообщает о паузе текущей сессии.
pauseSession()

// Отправляет информацию о том, что приложение открыто диплинком.
reportAppOpen(deeplink?: string = null)

// Отправляет кастомное событие.
reportEvent(eventName: string, attributes?: Record<string, any>)

// Метод для передачи ошибок.
reportError(identifier: string, message: string)

// Метод для передачи ошибок без идентификатора.
reportErrorWithoutIdentifier(message: string | undefined, error: Error)

// Метод для передачи крэшей.
reportUnhandledException(error: Error)

// Запрашивает различные идентификаторы AppMetrica SDK.
requestStartupParams(listener: StartupParamsCallback, identifiers: Array<string>)

// Сообщает о продолжении сессии или о старте новой, если таймаут сессии прошел.
resumeSession()

// Отправляет события, накопленные в буфере.
sendEventsBuffer()

// Передает местоположение устройства.
setLocation(location?: Location)

// Включает/выключает сбор данных о местоположении устройств.
setLocationTracking(enabled: boolean)

// Включает/выключает отправку данных в AppMetrica.
setDataSendingEnabled(enabled: boolean)

// Присваивает идентификатор профиля.
setUserProfileID(userProfileID?: string)

// Метод только для Android. Возвращает уровень API библиотеки.
async getLibraryApiLevel(): number

// Отправляет Ecommerce событие.
reportECommerce(event: ECommerceEvent)

// Отправляет In-App покупки.
reportRevenue(revenue: Revenue)

// Отправляет AdRevenue.
reportAdRevenue(adRevenue: AdRevenue)

// Отправляет профиль пользователя.
reportUserProfile(userProfile: UserProfile)

// Удаляет все данные ключ-значение, связанные со всеми будущими событиями.
clearAppEnvironment()

// Устанавливает пару ключ-значение, которая ассоциирована со всеми будущими событиями.
putAppEnvironmentValue(key: string, value?: string)

// Возвращает объект, реализующий IReporter для заданного API key приложения.
getReporter(apiKey: string)

// Активирует репортер с расширенной конфигурацией.
activateReporter(config: ReporterConfig)

// Возвращает идентификатора устройства или null.
async getDeviceId()

// Возвращает идентификатор установки или null.
async getUuid()

// Запрашивает отложенный deeplink. Отложенный deeplink доступен после получения Google Play installation referrer.
// Реферер обычно доступен вскоре после первого запуска приложения.
// После получения реферера отложенный deeplink передается в DeferredDeeplinkListener.onSuccess(deeplink: string).
// Если произойдет ошибка, она будет передана в DeferredDeeplinkListener.onFailure(error: DeferredDeeplinkError, referrer?: string).
requestDeferredDeeplink(listener: DeferredDeeplinkListener)

// Запрашивает параметры отложенного deeplink. Параметры доступны после получения Google Play installation referrer.
// Реферер обычно доступен вскоре после первого запуска приложения.
// После получения реферера параметры отложенного deeplink передаются в DeferredDeeplinkParametersListener.onSuccess(parameters: Record<string, string>).
// Если произойдет ошибка, она будет передана в DeferredDeeplinkParametersListener.onFailure: (error: DeferredDeeplinkError, referrer?: string).
requestDeferredDeeplinkParameters(listener: DeferredDeeplinkParametersListener)
```

### E-commerce

Для различных действий пользователя есть соответствующие типы ecommerce-событий. Чтобы создать конкретный тип события, используйте нужный метод класса.

Подробнее про отправку E-commerce-событий в разделе [E-commerce](../../../data-collection/about-ecommerce.md).

```javascript
// Возвращает ECommerceEvent для отправки события "просмотр карточки товара".
showProductCardEvent(product: ECommerceProduct, screen: ECommerceScreen): ECommerceEvent

// Возвращает ECommerceEvent для отправки события "просмотр страницы товара".
showProductDetailsEvent(product: ECommerceProduct, referrer?: ECommerceReferrer): ECommerceEvent

// Возвращает ECommerceEvent для отправки события "добавление товара в корзину".
addCartItemEvent(item: ECommerceCartItem): ECommerceEvent

// Возвращает ECommerceEvent для отправки события "удаление товара из корзины".
removeCartItemEvent(item: ECommerceCartItem): ECommerceEvent

// Возвращает ECommerceEvent для отправки события "начало оформления покупки".
beginCheckoutEvent(order: ECommerceOrder): ECommerceEvent

// Возвращает ECommerceEvent для отправки события "завершение покупки".
purchaseEvent(order: ECommerceOrder): ECommerceEvent
```

Подробнее о методах и интеграции AppMetrica в приложение смотрите в разделах документации для [Android](../../android/analytics/quick-start.md) и [iOS](../../ios/analytics/quick-start.md).

### UserProfile

Класс для хранения профиля пользователя. [Подробнее](react-native-operations.md#send-attribute-profile).

```javascript 
// Применяет к UserProfile атрибут пользователя
apply(attribute: UserProfileUpdate): UserProfile
```

### Attributes {#attributes}

Класс для созданиz атрибутов профиля. [Подробнее](react-native-operations.md#send-attribute-profile).

```javascript 
// Создает предопределенный атрибут для даты рождения/возраста.
birthDate(): BirthDateAttribute

// Создает предопределенный атрибут для пола.
gender(): GenderAttribute

// Создает предопределенный атрибут для имени.
userName(): NameAttribute

// Создает предопределенный атрибут для статуса уведомлений.
notificationsEnabled(): NotificationsEnabledAttribute

// Создает собственный атрибут типа bool.
customBoolean(key: string): BooleanAttribute

// Создает собственный атрибут типа счетчик.
customCounter(key: string): CounterAttribute

// Создает собственный атрибут типа number.
customNumber(key: string): NumberAttribute

// Создает собственный атрибут типа string.
customString(key: string): StringAttribute
```

### BirthDateAttribute

Класс для обновления возраста или даты рождения пользовательского профиля.

```javascript 
// Обновляет значение атрибута.
withAge(age: number): UserProfileUpdate

// Обновляет значение атрибута, если оно не было установлено ранее.
withAgeIfUndefined(age: number): UserProfileUpdate

// Обновляет значение атрибута.
withYear(year: number): UserProfileUpdate

// Обновляет значение атрибута, если оно не было установлено ранее.
withYearIfUndefined(year: number): UserProfileUpdate

// Обновляет значение атрибута.
withMonth(year: number, month: number): UserProfileUpdate

// Обновляет значение атрибута, если оно не было установлено ранее.
withMonthIfUndefined(year: number, month: number): UserProfileUpdate

// Обновляет значение атрибута.
withDay(year: number, month: number, day: number): UserProfileUpdate

// Обновляет значение атрибута, если оно не было установлено ранее.
withDayIfUndefined(year: number, month: number, day: number): UserProfileUpdate

// Обновляет значение атрибута.
withDate(date: Date): UserProfileUpdate

// Обновляет значение атрибута, если оно не было установлено ранее.
withDateIfUndefined(date: Date): UserProfileUpdate

// Сбрасывает значение атрибута.
withValueReset(): UserProfileUpdate
```

### BooleanAttribute

Класс для обновления значения логического атрибута.

```javascript 
// Обновляет значение атрибута.
withValue(value: boolean): UserProfileUpdate

// Обновляет значение атрибута, если оно не было установлено ранее.
withValueIfUndefined(value: boolean): UserProfileUpdate

// Сбрасывает значение атрибута.
withValueReset(): UserProfileUpdate
```

### CounterAttribute

Класс для обновления значения атрибута типа счетчик.

```javascript 
// Обновляет значение атрибута.
withDelta(delta: number): UserProfileUpdate
```

### GenderAttribute

Класс для обновления пола пользовательского профиля.

```javascript 
// Обновляет значение атрибута.
withValue(gender: UserProfileGender): UserProfileUpdate

// Обновляет значение атрибута, если оно не было установлено ранее.
withValueIfUndefined(gender: UserProfileGender): UserProfileUpdate

// Сбрасывает значение атрибута.
withValueReset(): UserProfileUpdate
```

### NameAttribute

Класс для обновления имени пользовательского профиля.

```javascript
// Обновляет значение атрибута.
withValue(value: string): UserProfileUpdate

// Обновляет значение атрибута, если оно не было установлено ранее.
withValueIfUndefined(value: string): UserProfileUpdate

// Сбрасывает значение атрибута.
withValueReset(): UserProfileUpdate
```

### NotificationsEnabledAttribute

Класс для обновления статуса уведомлений пользовательского профиля.

```javascript 
// Обновляет значение атрибута.
withValue(value: boolean): UserProfileUpdate

// Обновляет значение атрибута, если оно не было установлено ранее.
withValueIfUndefined(value: boolean): UserProfileUpdate

// Сбрасывает значение атрибута.
withValueReset(): UserProfileUpdate
```

### NumberAttribute

Класс для обновления значения числового атрибута.

```javascript
// Обновляет значение атрибута.
withValue(value: number): UserProfileUpdate

// Обновляет значение атрибута, если оно не было установлено ранее.
withValueIfUndefined(value: number): UserProfileUpdate

// Сбрасывает значение атрибута.
withValueReset(): UserProfileUpdate
```

### StringAttribute

Класс для обновления значения строкового атрибута.

```javascript 
// Обновляет значение атрибута.
withValue(value: string): UserProfileUpdate

// Обновляет значение атрибута, если оно не было установлено ранее.
withValueIfUndefined(value: string): UserProfileUpdate

// Сбрасывает значение атрибута.
withValueReset(): UserProfileUpdate
```

## Interfaces

### UserProfileUpdate

Содержит информацию об изменении атрибута пользователя.

Создаётся с помощью методов класса [Attributes](#attributes) и передаётся в `UserProfile.apply` метод.

### IReporter

Реализация этого интерфейса используется для отправки данных на дополнительные APIKey.
Получить реализацию можно методом `AppMetrica.getReporter(apiKey: string)`. Для активации репортера с расширенной конфигурацией нужно вызвать метод `AppMetrica.activateReporter(config: ReporterConfig)` до первого вызова `AppMetrica.getReporter(apiKey: string)` с тем же APIKey.

```javascript
  // Передает ошибки через репортер.
  reportError(identifier: string, message?: string, _reason?: Error | Object)

  // Передает ошибки без идентификатора.
  reportErrorWithoutIdentifier(message: string | undefined, error: Error)

  // Отправляет крэши.
  reportUnhandledException(error: Error)

  // Отправляет кастомное событие.
  reportEvent(eventName: string, attributes?: Record<string, any>)

  // Сообщает о паузе текущей сессии.
  pauseSession()

  // Сообщает о продолжении сессии или о старте новой, если таймаут сессии прошел.
  resumeSession()

  // Отправляет события, накопленные в буфере.
  sendEventsBuffer()

  // Удаляет все данные ключ-значение, связанные со всеми будущими событиями.
  clearAppEnvironment()

  // Устанавливает пару ключ-значение, которая ассоциирована со всеми будущими событиями.
  putAppEnvironmentValue(key: string, value?: string)

  // Присваивает идентификатор профиля.
  setUserProfileID(userProfileID?: string)

  // Включает/выключает отправку данных в AppMetrica.
  setDataSendingEnabled(enabled: boolean)

  // Отправляет профиль пользователя.
  reportUserProfile(userProfile: UserProfile)

  // Отправляет AdRevenue.
  reportAdRevenue(adRevenue: AdRevenue)

  // Отправляет Ecommerce события.
  reportECommerce(event: ECommerceEvent)

  // Отправляет In-App покупки.
  reportRevenue(revenue: Revenue)
```

### DeferredDeeplinkListener

Слушатель для получения отложенного диплинка. Его реализация передается в метод `requestDeferredDeeplink(listener: DeferredDeeplinkListener)`

```javascript
// Получает отложенный deeplink
onSuccess(deeplink: string)

// Обрабатывает ошибки при получении отложенного диплинка
onFailure(error: DeferredDeeplinkError, referrer?: string)
```


### DeferredDeeplinkParametersListener

Слушатель для получения параметров отложенного диплинка. Его реализация передается в метод `requestDeferredDeeplinkParameters(listener: DeferredDeeplinkParametersListener)`

```javascript
// Получает параметры отложенного дипплинка
onSuccess(parameters: Record<string, string>)

// Обрабатывает ошибки при получении параметров отложенного диплинка
onFailure(error: DeferredDeeplinkError, referrer?: string)
```

## См. также

- [Как включить отправку данных о местоположении пользователей?](../../../troubleshooting/troubleshooting.md#region)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
