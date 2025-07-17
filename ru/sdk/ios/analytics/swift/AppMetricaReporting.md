# Протокол AppMetricaReporting

## Методы экземпляра {#instance_summary}

#|
|| [clearAppEnvironment()](#method_clearAppEnvironment) | Удаление всех данных ключ-значение, связанных со всеми будущими событиями. ||
|| [pauseSession()](#method_pauseSession) | Приостанавливает сессию. ||
|| [reportAdRevenue(_:onFailure:)](#method_reportAdRevenue__onFailure) | Отправляет информацию о рекламной выручке на сервер AppMetrica. ||
|| [reportECommerce(_:onFailure)](#method_reportECommerce__onFailure) | Отправляет сообщение о ecommerce-событии. ||
|| [reportEvent(name:onFailure)](#method_reportEvent__onFailure) | Отправляет произвольное сообщение о событии. ||
|| [reportEvent(name:parameters:onFailure)](#method_reportEvent__parameters__onFailure) | Отправляет произвольное сообщение о событии c дополнительными параметрами. ||
|| [reportRevenue(_:onFailure:)](#method_reportRevenue__onFailure) | Отправляет информацию о покупке на сервер AppMetrica. ||
|| [reportUserProfile(_:onFailure)](#method_reportUserProfile__onFailure) | Отправляет информацию об обновлении пользовательского профиля. ||
|| [resumeSession()](#method_resumeSession) | Возобновляет сессию или создает новую, если таймаут сессии истек. ||
|| [sendEventsBuffer()](#method_sendEventsBuffer) | Отправляет сохраненные события из буфера. ||
|| [setAppEnvironment(_:forKey:)](#method_setAppEnvironmentValue__forKey) | Устанавливает пару ключ-значение, которая ассоциирована со всеми будущими событиями. ||
|| [setDataSendingEnabled(_:)](#method_setDataSendingEnabled) | Включает/отключает отправку статистики на сервер AppMetrica. ||
|| [setupWebViewReporting(with:onFailure:)](#method_setupWebViewReporting__onFailure) | Добавляет для указанной вебвью JavaScript-интерфейс с названием AppMetrica в window. Это позволяет отправлять клиентские события из JavaScript-кода. ||
|#

## Свойства {#property_summary}

#|
|| [userProfileID](#property_userProfileID) | Устанавливает ID для [пользовательского профиля](../../../../data-collection/about-profiles.md). ||
|#

## Описание методов {#method_detail}

### clearAppEnvironment() {#method_clearAppEnvironment}

```swift translate=no
func clearAppEnvironment()
```

Очистка среды приложения, например, удаление всех данных ключ - значение, связанных со всеми будущими событиями.

### pauseSession() {#method_pauseSession}

```swift translate=no
func pauseSession()
```

Приостанавливает сессию.

### reportAdRevenue(_:onFailure) {#method_reportAdRevenue__onFailure}

```swift translate=no
func reportAdRevenue(_ adRevenue: AdRevenueInfo, onFailure: ((Error) -> Void)?)
```

Отправляет информацию о рекламной выручке на сервер AppMetrica.

**Параметры:**

#|
|| `adRevenue` | Объект класса [AdRevenueInfo](AdRevenueInfo.md), который содержит информацию о рекламной выручке. ||
|| `onFailure` | Блок, который выполняется при возникновении ошибки. Ошибка передается как блок-аргумент. ||
|#

### reportECommerce(_:onFailure) {#method_reportECommerce__onFailure}

```swift translate=no
func reportECommerce(_ eCommerce: ECommerce, onFailure: ((Error) -> Void)?)
```

Отправляет сообщение о ecommerce-событии.

**Параметры:**

#|
|| `eCommerce` | Объект класса [ECommerce](ECommerce.md). ||
|| `onFailure` | Блок, который выполняется при возникновении ошибки. Ошибка передается как блок-аргумент. ||
|#

### reportEvent(name:onFailure) {#method_reportEvent__onFailure}

```swift translate=no
func reportEvent(name: String, onFailure: ((Error) -> Void)?)
```

Отправляет произвольное сообщение о событии.

**Параметры:**

#|
|| `name` | Короткое название или описание события. ||
|| `onFailure` | Блок, который выполняется при возникновении ошибки. Ошибка передается как блок-аргумент. ||
|#

### reportEvent(name:parameters:onFailure) {#method_reportEvent__parameters__onFailure}

```swift translate=no
func reportEvent(name: String, parameters: [AnyHashable : Any]?, onFailure: ((Error) -> Void)?)
```

Отправляет произвольное сообщение о событии c дополнительными параметрами.

**Параметры:**

#|
|| `name` | Короткое название или описание события. ||
|| `parameters` | Параметры в виде пар «ключ-значение». ||
|| `onFailure` | Блок, который выполняется при возникновении ошибки. Ошибка передается как блок-аргумент. ||
|#

### reportRevenue(_:onFailure:) {#method_reportRevenue__onFailure}

```swift translate=no
func reportRevenue(_ revenueInfo: RevenueInfo, onFailure: ((Error) -> Void)?)
```

Отправляет информацию о покупке на сервер AppMetrica.

**Параметры:**

#|
|| `revenueInfo` | Объект класса [RevenueInfo](RevenueInfo.md), который содержит информацию о покупке. ||
|| `onFailure` | Блок, который выполняется при возникновении ошибки. Ошибка передается как блок-аргумент. ||
|#

### reportUserProfile(_:onFailure) {#method_reportUserProfile__onFailure}

```swift translate=no
func reportUserProfile(_ userProfile: UserProfile, onFailure: ((Error) -> Void)?)
```

Отправляет информацию об обновлении пользовательского профиля.

**Параметры:**

#|
|| `userProfile` | Объект класса [UserProfile](UserProfile.md), который содержит информацию о пользовательском профиле. ||
|| `onFailure` | Блок, который выполняется при возникновении ошибки. Ошибка передается как блок-аргумент. ||
|#

### resumeSession() {#method_resumeSession}

```swift translate=no
func resumeSession()
```

Возобновляет сессию или создает новую, если таймаут сессии истек.

### sendEventsBuffer() {#method_sendEventsBuffer}

```swift translate=no
func sendEventsBuffer()
```

Отправляет сохраненные события из буфера.

AppMetrica SDK не отправляет события сразу после того, как оно произошло. Библиотека хранит данные о событиях в буфере. Метод `+sendEventsBuffer` отправляет данные из буфера и очищает его. Используйте этот метод для принудительной отправки сохраненных событий после прохождения важных сценариев пользователя.

{% note alert %}

Частое использование метода может привести к повышению энергопотребления и расходу исходящего интернет-трафика.

{% endnote %}

### setAppEnvironment(_:forKey:) {#method_setAppEnvironmentValue__forKey}

```swift translate=no
func setAppEnvironment(_ value: String?, forKey: String)
```

Установка данных ключ - значение, которые будут использоваться в качестве дополнительной информации, связанной со всеми будущими событиями.

Если значение равно нулю, ранее установленное значение ключа удаляется. Ничего не делает, если ключ не был добавлен.

**Параметры:**

#|
|| `value` | Значение. ||
|| `key` | Ключ. ||
|#

### setDataSendingEnabled(_:) {#method_setDataSendingEnabled}

```swift translate=no
func setDataSendingEnabled(_ enabled: Bool)
```

Включает/отключает отправку статистики на сервер AppMetrica.

{% note info %}

Отключение отправки статистики для репортера не влияет на отправку данных с главного API key. Но отключение отправки данных для главного API key прекращает отправку статистики со всех репортеров.

{% endnote %}

**Параметры:**

#|
|| `enabled` | Признак отправки статистики. Значение по умолчанию — `true`.
Возможные значения:

- `true` — отправка статистики включена.
- `false` — отправка статистики выключена. ||
  |#

### setupWebViewReporting(with:onFailure:) {#method_setupWebViewReporting__onFailure}

```swift translate=no
class func setupWebViewReporting(with: JSControlling, onFailure: ((Error) -> Void)?)
```

Добавляет для указанной вебвью JavaScript-интерфейс с названием AppMetrica в window. Это позволяет отправлять клиентские события из JavaScript-кода.

Замечания:

- Метод должен вызываться из главной очереди.
- Метод недоступен на tvOS.
- Метод необходимо вызывать до загрузки любого контента. Рекомендуется вызывать метод до создания вебвью и до добавления своих скриптов в WKUserContentController.
  Подробнее см. в разделе [Примеры использования методов](../ios-operations.md#js-event).

**Параметры:**

#|
|| `controller` | Объект `JSControlling`. ||
|| `onFailure` | Callback-метод, который будет вызван в случае ошибки. ||
|#

## Описание свойств {#property_detail}

### userProfileID {#property_userProfileID}

```swift translate=no
var userProfileID: String { get; set; }
```

Устанавливает ID для [пользовательского профиля](../../../../data-collection/about-profiles.md). Если отправка `ProfileId` не настроена, [предопределенные атрибуты](../../../../data-collection/profile-attributes.md#pre-defined) не отображаются в веб-интерфейсе.
