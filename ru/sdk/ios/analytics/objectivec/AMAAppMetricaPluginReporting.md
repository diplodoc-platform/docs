# Протокол AMAAppMetricaPluginReporting
Протокол `AMAAppMetricaPluginReporting` — это расширение `AMAAppMetricaCrashReporting`.

Экземпляр объекта, который реализует `AMAAppMetricaPluginReporting`, может быть получен с помощью метода [pluginExtension](AMAAppMetricaCrashReporting.md#method_pluginExtension) в [AMAAppMetricaCrashReporting](AMAAppMetricaCrashReporting.md).

Для каждого репортера создается один экземпляр `AMAAppMetricaPluginReporting`. Можно запрашивать его каждый раз по необходимости или сохранить ссылку на него для повторного использования. 

## Методы экземпляра {#instance_summary}

#|
|| [-reportUnhandledException:onFailure:](#method_reportUnhandledException_onFailure) | Отправляет сообщение о необработанной ошибке. ||
|| [-reportError:message:onFailure:](#method_reportError_message_onFailure) | Отправляет сообщение об ошибке. ||
|| [-reportErrorWithIdentifier:message:details:onFailure:](#method_reportErrorWithIdentifier_message_details_onFailure) | Отправляет сообщение об ошибке c кратким описанием. ||
|#

## Описание методов {#method_detail}

### -reportUnhandledException:onFailure: {#method_reportUnhandledException_onFailure}

```objectivec translate=no
- (void)reportUnhandledException:(AMAPluginErrorDetails *)errorDetails
                       onFailure:(nullable void (^)(NSError *error))onFailure
reportUnhandledException(exception:onFailure:);
```

Отправляет сообщение о необработанной ошибке. Подробнее см. [AMAPluginErrorDetails](AMAPluginErrorDetails.md).

**Параметры:**

#|
|| `errorDetails` | Объект, который описывает ошибку. ||
|| `onFailure` | Callback-метод, который будет вызван при сбое передачи сообщения. Ошибка `error` передается в качестве аргумента. ||
|#

### -reportError:message:onFailure: {#method_reportError_message_onFailure}

```objectivec translate=no
- (void)reportError:(AMAPluginErrorDetails *)errorDetails
            message:(nullable NSString *)message
          onFailure:(nullable void (^)(NSError *error))onFailure
reportError(error:message:onFailure:);
```

Отправляет сообщение об ошибке. Для группировки используется обратная трассировка `backtrace`. Чтобы изменить параметр группировки, используйте [-reportErrorWithIdentifier:message:details:onFailure:](#method_reportErrorWithIdentifier_message_details_onFailure). Подробнее см. [AMAPluginErrorDetails](AMAPluginErrorDetails.md).

**Параметры:**

#|
|| `errorDetails` | Объект с детальной информацией об ошибке. ||
|| `message` | Краткое описание ошибки. ||
|| `onFailure` | Callback-метод, который будет вызван при сбое передачи сообщения. Ошибка `error` передается в качестве аргумента. ||
|#

### -reportErrorWithIdentifier:message:details:onFailure: {#method_reportErrorWithIdentifier_message_details_onFailure}

```objectivec translate=no
- (void)reportErrorWithIdentifier:(NSString *)identifier
                          message:(nullable NSString *)message
                          details:(nullable AMAPluginErrorDetails *)errorDetails
                        onFailure:(nullable void (^)(NSError *error))onFailure
reportError(identifier:message:error:onFailure:);
```

Отправляет сообщение об ошибке c кратким описанием. Для группировки ошибок используется переданный идентификатор. Чтобы вместо него использовать для группировки обратную трассировку `backtrace`, используйте метод [-reportError:message:onFailure:](#method_reportError_message_onFailure). Подробнее см. [AMAPluginErrorDetails](AMAPluginErrorDetails.md).


**Параметры:**

#|
|| `identifier` | Идентификатор, который используется для группировки. ||
|| `message` | Краткое описание ошибки. ||
|| `errorDetails` | Объект с детальной информацией об ошибке.  ||
|| `onFailure` | Callback-метод, который будет вызван при сбое передачи сообщения. Ошибка `error` передается в качестве аргумента. ||
|#
