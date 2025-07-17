# Класс PluginErrorDetails

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

```swift translate=no
var exceptionClass: String?
```

Название класса/интерфейса/символа (в зависимости от используемого плагина) ошибки. Не более 100 символов. Лишние символы AppMetrica обрежет.

### message {#property_message}

```swift translate=no
var message: String?
```

Краткое описание ошибки. Не более 1000 символов. Лишние символы AppMetrica обрежет.

### backtrace {##property_backtrace}

```swift translate=no
var backtrace: [StackTraceElement]?
```

Обратная трассировка ошибки. Не более 200 стековых кадров. Если значение превысит ограничение, AppMetrica обрежет его.

### platform {##property_platform}

```swift translate=no
var platform: String?
```

Название плагина, в котором произошла ошибка. Не более 100 символов. Лишние символы AppMetrica обрежет.

Используйте константы, определенные в `PluginErrorDetails` для популярных плагинов, или кастомную строку для плагина, у которого нет соответствующей константы. 

### virtualMachineVersion {##property_virtualMachineVersion}

```swift translate=no
var virtualMachineVersion: String?
```

Версия виртуальной машины. Не более 100 символов. Лишние символы AppMetrica обрежет.

В этом свойстве можно указать версию используемого плагина (например, Unity или Flutter).

### pluginEnvironment {##property_pluginEnvironment}

```swift translate=no
var pluginEnvironment: [String : String]?
```

Среда подключения плагина. Произвольный словарь, содержащий любую дополнительную информацию о плагине. 

Не более 50 пар «ключ-значение». Не более 100 символов для ключа, не более 2000 символов для значения. Лишние символы AppMetrica обрежет.
