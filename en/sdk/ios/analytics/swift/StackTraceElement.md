# StackTraceElement class

## Properties {#property_summary}

#|
|| [className](#property_className) | Name of the error class/interface/character (depending on the plugin being used). ||
|| [fileName](#property_fileName) | Name of the file where the error occurred. ||
|| [line](#property_line) | Row number where the error occurred. ||
|| [column](#property_column) | Column number where the error occurred. ||
|| [methodName](#property_methodName) | Name of the method or function (depending on the plugin being used) where the error occurred. ||
|#

### className {#property_className}

```swift translate=no
var className: String?
```

Name of the error class/interface/character (depending on the plugin being used). No more than 100 characters. AppMetrica truncates any characters over the limit.

### fileName {#property_fileName}

```swift translate=no
var fileName: String?
```

Name of the file where the error occurred. No more than 100 characters. AppMetrica truncates any characters over the limit.

### line {#property_line}

```swift translate=no
var line: NSNumber?
```

Row number where the error occurred.

### column {#property_column}

```swift translate=no
var column: NSNumber?
```

Column number where the error occurred.

### methodName {#property_methodName}

Name of the method or function (depending on the plugin being used) where the error occurred. No more than 100 characters. AppMetrica truncates any characters over the limit.

```swift translate=no
var methodName: String?
```
