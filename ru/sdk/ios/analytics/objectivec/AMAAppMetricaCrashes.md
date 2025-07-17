# Класс AMAAppMetricaCrashes

Класс предоставляет функции отправки сообщений об ошибках и сбоях для интеграции с AppMetrica.

## Методы экземпляра {#instance_summary}

#|
|| [+crashes:](#method_crashes) | Получает доступ к синглтону `AMAAppMetricaCrashes`. ||
|| [-setConfiguration:](#method_setConfiguration) | Настраивает для приложения конфигурацию механизма отправки сообщений о сбоях. ||
|| [-reportNSError:onFailure:](#method_reportNSError_onFailure) | Отправляет сообщение об ошибке типа `NSError` в AppMetrica. ||
|| [-reportNSError:options:onFailure:](#method_reportNSError_options_onFailure) | Отправляет сообщение об ошибке типа `NSError` с дополнительными возможностями кастомизации сообщения. ||
|| [-reportError:onFailure:](#method_reportNSError_onFailure) | Отправляет сообщение об ошибке, соответствующей протоколу `AMAErrorRepresentable`. ||
|| [-reportError:options:onFailure:](#method_reportNSError_options_onFailure) | Отправляет сообщение об ошибке, соответствующей протоколу `AMAErrorRepresentable`, с дополнительными возможностями кастомизации сообщения. ||
|| [-setErrorEnvironmentValue:forKey:](#method_setErrorEnvironmentValue_forKey) | Устанавливает пару «ключ-значение», которая будет связана с ошибками и сбоями. ||
|| [-clearErrorEnvironment:](#method_clearErrorEnvironment) | Удаляет все пары «ключ-значение», связанные с ошибками и сбоями. ||
|| [-requestCrashReportingStateWithCompletionQueue:completionBlock:](#method_requestCrashReportingStateWithCompletionQueue_completionBlock) | Запрашивает текущее состояние о сбоях. ||
|| [-enableANRMonitoring:](#method_enableANRMonitoring) | Включает ANR-мониторинг с параметрами по умолчанию. ||
|| [-enableANRMonitoringWithWatchdogInterval:pingInterval:](#method_enableANRMonitoringWithWatchdogInterval_pingInterval) | Включает ANR-мониторинг с указанными параметрами. ||
|| [-reporterForAPIKey:](#method_reporterForAPIKey) | Возвращает `id<AMAAppMetricaCrashReporting>`, который может отправлять ошибки на определенный ключ API. ||
|| [-pluginExtension:](#method_pluginExtension) | Создает `AMAAppMetricaPlugins`, который может отправлять события плагина в основной ключ API. ||
|#

## Описание методов {#method_detail}

### +crashes: {#method_crashes}

```objectivec translate=no
+ (instancetype)crashes (crashes())
```

Получает доступ к синглтону `AMAAppMetricaCrashes`.

**Возвращает:**

Экземпляр синглтона `AMAAppMetricaCrashes`.

### -setConfiguration: {#method_setConfiguration}

```objectivec translate=no
- (void)setConfiguration:(AMAAppMetricaCrashesConfiguration *)configuration;
```

Настраивает для приложения конфигурацию механизма отправки сообщений о сбоях. Чтобы включить или отключить определенные типы сообщений о сбоях, а также настроить связанные параметры, используйте свойства класса [AMAAppMetricaCrashesConfiguration](AMAAppMetricaCrashesConfiguration.md). После настройки конфигурация будет управлять тем, как приложение обрабатывает различные типы сбоев и проблем.

**Параметр:**

#|
|| `configuration` | Объект [AMAAppMetricaCrashesConfiguration](AMAAppMetricaCrashesConfiguration.md), который определяет, как приложение должно обрабатывать сбои и сообщать о них. ||
|#

**Пример:**

```objectivec translate=no
AMAAppMetricaCrashesConfiguration *config = [AMAAppMetricaCrashesConfiguration new];
config.autoCrashTracking = YES;
config.probablyUnhandledCrashReporting = NO;
config.applicationNotRespondingDetection = YES;
config.applicationNotRespondingWatchdogInterval = 5.0;
[[AMAAppMetricaCrashes crashes] setConfiguration:config];
```

### -reportNSError:onFailure: {#method_reportNSError_onFailure} 

```objectivec translate=no
- (void)reportNSError:(NSError *)error
            onFailure:(nullable void (^)(NSError *error))onFailure report(nserror:onFailure:);
```

Отправляет сообщение об ошибке типа `NSError`, которые соответствуют определенным ограничениям на `domain`, `userInfo` и другие свойства.

Можно включить обратную трассировку в `NSError`, используя константу `AMABacktraceErrorKey` в `userInfo`.

Ограничения:

- `domain` — не более 200 символов.
- `userInfo` — Не более 50 пар «ключ-значение», длина ключа — не более 100 символов, длина значения — не более 2000 символов.
- `NSUnderlyingErrorKey` — Используя этот ключ в `userInfo`, можно включить не более 10 ошибок.
- `AMABacktraceErrorKey` — Используя этот ключ в `userInfo`, можно включить максимум 200 стековых кадров в обратную трассировку.

Если значение превысит указанное ограничение, AppMetrica обрежет его.

**Параметры:**

#|
|| `error` | Объект `NSError` — ошибка, о которой нужно сообщить. Свойства `domain` и `code` используются для группировки ошибок. ||
|| `OnFailure` | Callback-метод, который будет вызван при сбое передачи сообщения. Ошибка `error` передается в качестве аргумента. ||
|#

### -reportNSError:options:onFailure: {#method_reportNSError_options_onFailure}

```objectivec translate=no
- (void)reportNSError:(NSError *)error
              options:(AMAErrorReportingOptions)options
            onFailure:(nullable void (^)(NSError *error))onFailure report(nserror:options:onFailure:);
```

Отправляет кастомизированное сообщение об ошибке типа `NSError`, соблюдая ограничения для свойств `domain`, `userInfo` и других.

Можно включить обратную трассировку в `NSError`, используя константу `AMABacktraceErrorKey` в `userInfo`.

Ограничения:

- `domain` — не более 200 символов.
- `userInfo` — Не более 50 пар «ключ-значение», длина ключа — не более 100 символов, длина значения — не более 2000 символов.
- `NSUnderlyingErrorKey` — Используя этот ключ в `userInfo`, можно включить не более 10 ошибок.
- `AMABacktraceErrorKey` — Используя этот ключ в `userInfo`, можно включить максимум 200 стековых кадров в обратную трассировку.

Если значение превысит любое из этих ограничений, AppMetrica обрежет его.

**Параметры:**

#|
|| `error` | Объект `NSError` — ошибка, о которой нужно сообщить. Свойства `domain` и `code` используются для группировки ошибок. ||
|| `options` | Дополнительные опции [AMAErrorReportingOptions](AMAErrorReportingOptions.md), которые определяют, как должно быть передано сообщение об ошибке. ||
|| `OnFailure` | Callback-метод, который будет вызван при сбое передачи сообщения. Ошибка `error` передается в качестве аргумента. ||
|#

### -reportError:onFailure: {#method_reportNSError_onFailure}

```objectivec translate=no
- (void)reportError:(id<AMAErrorRepresentable>)error
          onFailure:(nullable void (^)(NSError *error))onFailure report(error:onFailure:);
```

Отправляет сообщение об ошибке, соответствующей протоколу [AMAErrorRepresentable](AMAErrorRepresentable.md). 

**Параметры:**

#|
|| `error` | Ошибка, соответствующая протоколу `AMAErrorRepresentable`. ||
|| `OnFailure` | Callback-метод, который будет вызван при сбое передачи сообщения. Ошибка `error` передается в качестве аргумента. ||
|#

### -reportError:options:onFailure: {#method_reportNSError_options_onFailure}

```objectivec translate=no
- (void)reportError:(id<AMAErrorRepresentable>)error
            options:(AMAErrorReportingOptions)options
          onFailure:(nullable void (^)(NSError *error))onFailure report(error:options:onFailure:);
```

Отправляет сообщение об ошибке, соответствующей протоколу [AMAErrorRepresentable](AMAErrorRepresentable.md), с дополнительными возможностями кастомизации сообщения.

**Параметры:**

#|
|| `error` | Ошибка, соответствующая протоколу `AMAErrorRepresentable`. ||
|| `options` | Дополнительные опции [AMAErrorReportingOptions](AMAErrorReportingOptions.md), которые определяют, как должно быть передано сообщение об ошибке. ||
|| `OnFailure` | Callback-метод, который будет вызван при сбое передачи сообщения. Ошибка `error` передается в качестве аргумента. ||
|#

### -setErrorEnvironmentValue:forKey: {#method_setErrorEnvironmentValue_forKey}

```objectivec translate=no
- (void)setErrorEnvironmentValue:(nullable NSString *)value
                          forKey:(NSString *)key set(errorEnvironmentValue:forKey:);
```

Устанавливает пару «ключ-значение», которая будет связана с ошибками и сбоями. AppMetrica использует ее как дополнительную информацию для необработанных исключений.

**Параметры:**

#|
|| `value` | Значение, которое нужно связать с ключом. Если передать `nil`, ранее установленная пара «ключ-значение» с этим ключом будет удалена. ||
|| `key` | Ключ, с которым должно быть связано значение. ||
|#

### -clearErrorEnvironment: {#method_clearErrorEnvironment}

```objectivec translate=no
- (void)clearErrorEnvironment;
```

Удаляет все ранее установленные пары «ключ-значение», связанные с ошибками и сбоями. 

Использование этого метода гарантирует, что никакая дополнительная информация не будет добавлена к будущим необработанным исключениям, если только не будут установлены новые пары «ключ-значение».

Чтобы установить пару «ключ-значение», используйте [-setErrorEnvironmentValue:forKey:](#method_setErrorEnvironmentValue_forKey).


### -requestCrashReportingStateWithCompletionQueue:completionBlock: {#method_requestCrashReportingStateWithCompletionQueue_completionBlock}

```objectivec translate=no
- (void)requestCrashReportingStateWithCompletionQueue:(dispatch_queue_t)completionQueue
                                      completionBlock:(AMACrashReportingStateCompletionBlock)completionBlock;
```

Метод асинхронно получает текущее состояние сообщений об ошибках и возвращает его через блок завершения.

Подробнее о словаре с ключами и связанными с ними значениями см. `AMACrashReportingStateCompletionBlock`.

**Параметры:**

#|
|| `completionQueue` | Очередь отправки сообщений, в которой выполняется блок завершения. ||
|| `completionBlock` | Блок, который должен быть выполнен после завершения запроса. ||
|#

### -enableANRMonitoring: {#method_enableANRMonitoring}

```objectivec translate=no
- (void)enableANRMonitoring;
```

Включает мониторинг состояния «Приложение не отвечает» (ANR) с параметрами по умолчанию. 

Используйте этот метод, чтобы включить ANR-мониторинг только после активации. Чтобы включить ANR-мониторинг во время активации, используйте свойство `applicationNotRespondingDetection` в [AMAAppMetricaCrashesConfiguration](AMAAppMetricaCrashesConfiguration.md).

Параметры по умолчанию:

- `watchdog` — интервал 4 секунды;
- `ping`  — интервал 0,1 секунды.

### -enableANRMonitoringWithWatchdogInterval:pingInterval: {#method_enableANRMonitoringWithWatchdogInterval_pingInterval}

```objectivec translate=no
- (void)enableANRMonitoringWithWatchdogInterval:(NSTimeInterval)watchdog 
                                   pingInterval:(NSTimeInterval)ping;
```

Включает мониторинг состояния «Приложение не отвечает» (ANR) только после активации. Чтобы включить ANR-мониторинг во время активации, используйте свойство `applicationNotRespondingDetection` в [AMAAppMetricaCrashesConfiguration](AMAAppMetricaCrashesConfiguration.md).

**Параметры:**

#|
|| `watchdog` | Интервал времени, который будет ожидать `watchdog`, прежде чем сообщить о состоянии «Приложение не отвечает» (ANR). ||
|| `ping` | Частота, с которой `watchdog` будет проверять состояние «Приложение не отвечает» (ANR). Уменьшение интервала `ping` может привести к снижению производительности приложения. ||
|#

### -reporterForAPIKey: {#method_reporterForAPIKey}

```objectivec translate=no
- (nullable id<AMAAppMetricaCrashReporting>)reporterForAPIKey:(NSString *)apiKey reporter(for:);
```

Возвращает `id<AMAAppMetricaCrashReporting>`, который может отправлять ошибки на определенный ключ API.

**Параметр:**

#|
|| `apiKey` | API-ключ, на который нужно отправлять ошибки. ||
|#

**Возвращает:**

Идентификатор `id<AMAAppMetricaCrashReporting>`, который соответствует `AMAAppMetricaCrashReporting` и обеспечивает
отправку ошибок на определенный ключ API.

### -pluginExtension: {#method_pluginExtension}

```objectivec translate=no
- (id<AMAAppMetricaPlugins>)pluginExtension;
```

Создает экземпляр `AMAAppMetricaPlugins`, который может отправлять события плагина на основной ключ API. Можно запрашивать его каждый раз по необходимости или сохранить ссылку на него для повторного использования. Для использования этого расширения нужно сначала активировать AppMetrica с помощью `[AMAAppMetrica activateWithConfiguration:]`.

**Возвращает:**

Экземпляр расширения плагина.
