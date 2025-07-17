# Протокол AMAAppMetricaCrashReporting

Протокол `AMAAppMetricaCrashReporting` содержит методы, которые используются для кастомизации сообщений об ошибках и сбоях.

## Методы экземпляра {#instance_summary}

#|
|| [-reportNSError:onFailure:](#method_reportNSError_onFailure) | Отправляет сообщение об ошибке типа `NSError` в AppMetrica. ||
|| [-reportNSError:options:onFailure:](#method_reportNSError_options_onFailure) | Отправляет сообщение об ошибке типа `NSError` с дополнительными возможностями кастомизации сообщения. ||
|| [-reportError:onFailure:](#method_reportNSError_onFailure) | Отправляет сообщение об ошибке, соответствующей протоколу `AMAErrorRepresentable`. ||
|| [-reportError:options:onFailure:](#method_reportNSError_options_onFailure) | Отправляет сообщение об ошибке, соответствующей протоколу `AMAErrorRepresentable`, с дополнительными возможностями кастомизации сообщения. ||
|| [-setErrorEnvironmentValue:forKey:](#method_setErrorEnvironmentValue_forKey) | Устанавливает пару «ключ-значение», которая будет связана с ошибками и сбоями. ||
|| [-pluginExtension:](#method_pluginExtension) | Создает `AMAAppMetricaPlugins`, который может отправлять события плагина в основной ключ API. ||
|#

## Описание методов {#method_detail}

### -reportNSError:onFailure: {#method_reportNSErro_onFailure} 

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

### -pluginExtension: {#method_pluginExtension}

```objectivec translate=no
- (id<AMAAppMetricaPlugins>)pluginExtension;
```

Создает экземпляр `AMAAppMetricaPlugins`, который может отправлять события плагина на основной ключ API. Можно запрашивать его каждый раз по необходимости или сохранить ссылку на него для повторного использования. Для использования этого расширения нужно сначала активировать AppMetrica с помощью `[AMAAppMetrica activateWithConfiguration:]`.

**Возвращает:**

Экземпляр расширения плагина.
