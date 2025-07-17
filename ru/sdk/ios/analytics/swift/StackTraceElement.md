# Класс StackTraceElement

## Свойства {#property_summary}

#|
|| [className](#property_className) | Название класса/интерфейса/символа (в зависимости от используемого плагина) ошибки. ||
|| [fileName](#property_fileName) | Имя файла, в котором произошла ошибка. ||
|| [line](#property_line) | Номер строки, в которой произошла ошибка. ||
|| [column](#property_column) | Номер столбца, в котором произошла ошибка. ||
|| [methodName](#property_methodName) | Название метода/функции (в зависимости от используемого плагина), в которой произошла ошибка. ||
|#

### className {#property_className}

```swift translate=no
var className: String?
```

Название класса/интерфейса/символа (в зависимости от используемого плагина) ошибки. Не более 100 символов. Лишние символы AppMetrica обрежет.

### fileName {#property_fileName}

```swift translate=no
var fileName: String?
```

Имя файла, в котором произошла ошибка. Не более 100 символов. Лишние символы AppMetrica обрежет.

### line {#property_line}

```swift translate=no
var line: NSNumber?
```

Номер строки, в которой произошла ошибка.

### column {#property_column}

```swift translate=no
var column: NSNumber?
```

Номер столбца, в котором произошла ошибка.

### methodName {#property_methodName}

Название метода/функции (в зависимости от используемого плагина), в которой произошла ошибка. Не более 100 символов. Лишние символы AppMetrica обрежет.

```swift translate=no
var methodName: String?
```
