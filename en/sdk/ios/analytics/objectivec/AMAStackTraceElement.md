# AMAStackTraceElement class

## Properties {#property_summary}

#|
|| [className](#property_className) | Name of the error class/interface/character (depending on the plugin being used). ||
|| [fileName](#property_fileName) | Name of the file where the error occurred. ||
|| [line](#property_line) | Row number where the error occurred. ||
|| [column](#property_column) | Column number where the error occurred. ||
|| [methodName](#property_methodName) | Name of the method or function (depending on the plugin being used) where the error occurred. ||
|#

### className {#property_className}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSString *className;
```

Name of the error class/interface/character (depending on the plugin being used). No more than 100 characters. AppMetrica truncates any characters over the limit.

### fileName {#property_fileName}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSString *fileName;
```

Name of the file where the error occurred. No more than 100 characters. AppMetrica truncates any characters over the limit.

### line {#property_line}

```objectivec translate=no
@property (nonatomic, strong, nullable) NSNumber *line;
```

Row number where the error occurred.

### column {#property_column}

```objectivec translate=no
@property (nonatomic, strong, nullable) NSNumber *column;
```

Column number where the error occurred.

### methodName {#property_methodName}

Name of the method or function (depending on the plugin being used) where the error occurred. No more than 100 characters. AppMetrica truncates any characters over the limit.

```objectivec translate=no
@property (nonatomic, copy, nullable) NSString *methodName;
```
