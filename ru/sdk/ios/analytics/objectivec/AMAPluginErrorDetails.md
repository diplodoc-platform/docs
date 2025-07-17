# Класс AMAPluginErrorDetails

## Свойства {#property_summary}

#|
|| [exceptionClass](#property_exceptionClass) | Название класса/интерфейса/символа (в зависимости от используемого плагина) ошибки. ||
|| [message](#property_message) | Краткое описание ошибки. ||
|| [backtrace](#property_backtrace) | Обратная трассировка ошибки. ||
|| [platform](#property_platform) | Название плагина, в котором произошла ошибка. ||
|| [virtualMachineVersion](#property_virtualMachineVersion) | Версия виртуальной машины. ||
|| [pluginEnvironment](#property_pluginEnvironment) | Среда подключения плагина. ||
|#

### exceptionClass {#property_exceptionClass}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSString *exceptionClass;
```

Название класса/интерфейса/символа (в зависимости от используемого плагина) ошибки. Не более 100 символов. Лишние символы AppMetrica обрежет.

### message {#property_message}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSString *message;
```

Краткое описание ошибки. Не более 1000 символов. Лишние символы AppMetrica обрежет.

### backtrace {##property_backtrace}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSArray<AMAStackTraceElement *> *backtrace;
```

Обратная трассировка ошибки. Не более 200 стековых кадров. Если значение превысит ограничение, AppMetrica обрежет его.

### platform {##property_platform}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSString *platform;
```

Название плагина, в котором произошла ошибка. Не более 100 символов. Лишние символы AppMetrica обрежет.

Используйте константы, определенные в `AMAPluginErrorDetails` для популярных плагинов, или кастомную строку для плагина, у которого нет соответствующей константы. 

### virtualMachineVersion {##property_virtualMachineVersion}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSString *virtualMachineVersion;
```

Версия виртуальной машины. Не более 100 символов. Лишние символы AppMetrica обрежет.

В этом свойстве можно указать версию используемого плагина (например, Unity или Flutter).

### pluginEnvironment {##property_pluginEnvironment}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSDictionary<NSString *, NSString *> *pluginEnvironment;
```

Среда подключения плагина. Произвольный словарь, содержащий любую дополнительную информацию о плагине. 

Не более 50 пар «ключ-значение». Не более 100 символов для ключа, не более 2000 символов для значения. Лишние символы AppMetrica обрежет.
