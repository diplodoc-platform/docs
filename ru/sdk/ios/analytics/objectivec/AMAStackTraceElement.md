# Класс AMAStackTraceElement

## Свойства {#property_summary}

#|
|| [className](#property_className) | Название класса/интерфейса/символа (в зависимости от используемого плагина) ошибки. ||
|| [fileName](#property_fileName) | Имя файла, в котором произошла ошибка. ||
|| [line](#property_line) | Номер строки, в которой произошла ошибка. ||
|| [column](#property_column) | Номер столбца, в котором произошла ошибка. ||
|| [methodName](#property_methodName) | Название метода/функции (в зависимости от используемого плагина), в которой произошла ошибка. ||
|#

### className {#property_className}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSString *className;
```

Название класса/интерфейса/символа (в зависимости от используемого плагина) ошибки. Не более 100 символов. Лишние символы AppMetrica обрежет.

### fileName {#property_fileName}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSString *fileName;
```

Имя файла, в котором произошла ошибка. Не более 100 символов. Лишние символы AppMetrica обрежет.

### line {#property_line}

```objectivec translate=no
@property (nonatomic, strong, nullable) NSNumber *line;
```

Номер строки, в которой произошла ошибка.

### column {#property_column}

```objectivec translate=no
@property (nonatomic, strong, nullable) NSNumber *column;
```

Номер столбца, в котором произошла ошибка.

### methodName {#property_methodName}

Название метода/функции (в зависимости от используемого плагина), в которой произошла ошибка. Не более 100 символов. Лишние символы AppMetrica обрежет.

```objectivec translate=no
@property (nonatomic, copy, nullable) NSString *methodName;
```
