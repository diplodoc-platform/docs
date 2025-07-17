# Протокол AMAAppMetricaReporting

## Методы экземпляра {#instance_summary}

#|
|| -[clearAppEnvironment](#method_clearAppEnvironment) | Удаление всех данных ключ-значение, связанных со всеми будущими событиями. ||
|| -[pauseSession](#method_pauseSession) | Приостанавливает сессию. ||
|| -[reportAdRevenue:onFailure:](#method_reportAdRevenue__onFailure) | Отправляет информацию о рекламной выручке на сервер AppMetrica. ||
|| -[reportECommerce:onFailure](#method_reportECommerce__onFailure) | Отправляет сообщение о ecommerce-событии. ||
|| -[reportEvent:onFailure](#method_reportEvent__onFailure) | Отправляет произвольное сообщение о событии. ||
|| -[reportEvent:parameters:onFailure](#method_reportEvent__parameters__onFailure) | Отправляет произвольное сообщение о событии c дополнительными параметрами. ||
|| -[reportRevenue:onFailure:](#method_reportRevenue__onFailure) | Отправляет информацию о покупке на сервер AppMetrica. ||
|| -[reportUserProfile:onFailure](#method_reportUserProfile__onFailure) | Отправляет информацию об обновлении пользовательского профиля. ||
|| -[resumeSession](#method_resumeSession) | Возобновляет сессию или создает новую, если таймаут сессии истек. ||
|| -[sendEventsBuffer](#method_sendEventsBuffer) | Отправляет сохраненные события из буфера. ||
|| -[setAppEnvironmentValue:forKey:](#method_setAppEnvironmentValue__forKey) | Устанавливает пару ключ-значение, которая ассоциирована со всеми будущими событиями. ||
|| -[setDataSendingEnabled:](#method_setDataSendingEnabled) | Включает/отключает отправку статистики на сервер AppMetrica. ||
|| -[setupWebViewReporting:onFailure:](#method_setupWebViewReporting__onFailure) | Добавляет для указанной вебвью JavaScript-интерфейс с названием AppMetrica в window. Это позволяет отправлять клиентские события из JavaScript-кода. ||
|#

## Свойства {#property_summary}

#|
|| [userProfileID](#property_userProfileID) | Устанавливает ID для [пользовательского профиля](../../../../data-collection/about-profiles.md). ||
|#

## Описание методов {#method_detail}

### -clearAppEnvironment {#method_clearAppEnvironment}

```objectivec translate=no
- (void)clearAppEnvironment;
```

Очистка среды приложения, например, удаление всех данных ключ - значение, связанных со всеми будущими событиями.

### -pauseSession {#method_pauseSession}

```objectivec translate=no
- (void)pauseSession;
```

Приостанавливает сессию.

### -reportAdRevenue:onFailure: {#method_reportAdRevenue__onFailure}

```objectivec translate=no
- (void)reportAdRevenue:(AMAAdRevenueInfo *)adRevenue
              onFailure:(nullable void (^)(NSError *error))onFailure;
```

Отправляет информацию о рекламной выручке на сервер AppMetrica.

**Параметры:**

#|
|| `adRevenue` | Объект класса [AMAAdRevenueInfo](AMAAdRevenueInfo.md), который содержит информацию о рекламной выручке. ||
|| `onFailure` | Блок, который выполняется при возникновении ошибки. Ошибка передается как блок-аргумент. ||
|#

### -reportECommerce:onFailure {#method_reportECommerce__onFailure}

```objectivec translate=no
- (void)reportECommerce:(AMAECommerce *)eCommerce
              onFailure:(nullable void (^)(NSError *error))onFailure;
```

Отправляет сообщение о ecommerce-событии.

**Параметры:**

#|
|| `eCommerce` | Объект класса [AMAECommerce](AMAECommerce.md). ||
|| `onFailure` | Блок, который выполняется при возникновении ошибки. Ошибка передается как блок-аргумент. ||
|#

### -reportEvent:onFailure {#method_reportEvent__onFailure}

```objectivec translate=no
- (void)reportEvent:(NSString *)name
          onFailure:(nullable void (^)(NSError *error))onFailure;
```

Отправляет произвольное сообщение о событии.

**Параметры:**

#|
|| `name` | Короткое название или описание события. ||
|| `onFailure` | Блок, который выполняется при возникновении ошибки. Ошибка передается как блок-аргумент. ||
|#

### -reportEvent:parameters:onFailure {#method_reportEvent__parameters__onFailure}

```objectivec translate=no
- (void)reportEvent:(NSString *)name
         parameters:(nullable NSDictionary *)params
          onFailure:(nullable void (^)(NSError *error))onFailure;
```

Отправляет произвольное сообщение о событии c дополнительными параметрами.

**Параметры:**

#|
|| `name` | Короткое название или описание события. ||
|| `params` | Параметры в виде пар «ключ-значение». ||
|| `onFailure` | Блок, который выполняется при возникновении ошибки. Ошибка передается как блок-аргумент. ||
|#

### -reportRevenue:onFailure: {#method_reportRevenue__onFailure}

```objectivec translate=no
- (void)reportRevenue:(AMARevenueInfo *)revenueInfo
            onFailure:(nullable void (^)(NSError *error))onFailure;
```

Отправляет информацию о покупке на сервер AppMetrica.

**Параметры:**

#|
|| `revenueInfo` | Объект класса [AMARevenueInfo](AMARevenueInfo.md), который содержит информацию о покупке. ||
|| `onFailure` | Блок, который выполняется при возникновении ошибки. Ошибка передается как блок-аргумент. ||
|#

### -reportUserProfile:onFailure {#method_reportUserProfile__onFailure}

```objectivec translate=no
- (void)reportUserProfile:(AMAUserProfile *)userProfile
                onFailure:(nullable void (^)(NSError *error))onFailure;
```

Отправляет информацию об обновлении пользовательского профиля.

**Параметры:**

#|
|| `userProfile` | Объект класса [AMAUserProfile](AMAUserProfile.md), который содержит информацию о пользовательском профиле. ||
|| `onFailure` | Блок, который выполняется при возникновении ошибки. Ошибка передается как блок-аргумент. ||
|#

### -resumeSession {#method_resumeSession}

```objectivec translate=no
- (void)resumeSession;
```

Возобновляет сессию или создает новую, если таймаут сессии истек.

### -sendEventsBuffer {#method_sendEventsBuffer}

```objectivec translate=no
- (void)sendEventsBuffer;
```

Отправляет сохраненные события из буфера.

AppMetrica SDK не отправляет события сразу после того, как оно произошло. Библиотека хранит данные о событиях в буфере. Метод `+sendEventsBuffer` отправляет данные из буфера и очищает его. Используйте этот метод для принудительной отправки сохраненных событий после прохождения важных сценариев пользователя.

{% note alert %}

Частое использование метода может привести к повышению энергопотребления и расходу исходящего интернет-трафика.

{% endnote %}

### -setAppEnvironmentValue:forKey: {#method_setAppEnvironmentValue__forKey}

```objectivec translate=no
- (void)setAppEnvironmentValue:(nullable NSString *)value
                        forKey:(NSString *)key;
```

Установка данных ключ - значение, которые будут использоваться в качестве дополнительной информации, связанной со всеми будущими событиями.

Если значение равно нулю, ранее установленное значение ключа удаляется. Ничего не делает, если ключ не был добавлен.

**Параметры:**

#|
|| `value` | Значение. ||
|| `key` | Ключ. ||
|#

### -setDataSendingEnabled: {#method_setDataSendingEnabled}

```objectivec translate=no
- (void)setDataSendingEnabled:(BOOL)enabled;
```

Включает/отключает отправку статистики на сервер AppMetrica.

{% note info %}

Отключение отправки статистики для репортера не влияет на отправку данных с главного API key. Но отключение отправки данных для главного API key прекращает отправку статистики со всех репортеров.

{% endnote %}

**Параметры:**

#|
|| `enabled` | Признак отправки статистики. Значение по умолчанию — `YES`.
Возможные значения:

- `YES` — отправка статистики включена.
- `NO` — отправка статистики выключена. ||
|#

### -setupWebViewReporting:onFailure: {#method_setupWebViewReporting__onFailure}

```objectivec translate=no
- (void)setupWebViewReporting:(id<AMAJSControlling>)controller
                    onFailure:(nullable void (^)(NSError *error))onFailure;
```

Добавляет для указанной вебвью JavaScript-интерфейс с названием AppMetrica в window. Это позволяет отправлять клиентские события из JavaScript-кода.

Замечания:

- Метод должен вызываться из главной очереди.
- Метод недоступен на tvOS.
- Метод необходимо вызывать до загрузки любого контента. Рекомендуется вызывать метод до создания вебвью и до добавления своих скриптов в WKUserContentController.
  Подробнее см. в разделе [Примеры использования методов](../ios-operations.md#js-event).

**Параметры:**

#|
|| `controller` | Объект `AMAJSControlling`. ||
|| `onFailure` | Callback-метод, который будет вызван в случае ошибки. ||
|#

## Описание свойств {#property_detail}

### userProfileID {#property_userProfileID}

```objectivec translate=no
@property (class, nonatomic, nullable) NSString *userProfileID;
```

Устанавливает ID для [пользовательского профиля](../../../../data-collection/about-profiles.md). Если отправка `ProfileId` не настроена, [предопределенные атрибуты](../../../../data-collection/profile-attributes.md#pre-defined) не отображаются в веб-интерфейсе.
