# Logger Service

Logger Service is a logging system in Diplodoc with support for various logging levels.

## Main features

- Three logging levels: ##info##, ##warning##, and ##error##.
- Support for logging channels and topics.
- Colored message output.
- Creating custom topics.
- Support for message filtering.
- Log redirection.
- Integration with hooks for message handling.

## Accessing the service

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MyExtension', (run) => {
            // Получение сервиса из контекста
            const {logger} = run;
            
            // Получение хуков сервиса
            const loggerHooks = getLoggerHooks(logger);
        });
    }
}
```

## Available hooks

### Info
The hook is called when logging informational messages.

```typescript
loggerHooks.Info.tap('MyHook', (message) => {
    // message: Сообщение для логирования
    console.log('Info message:', message);
    return message;
});
```

### Warn
The hook is called when logging warnings.

```typescript
loggerHooks.Warn.tap('MyHook', (message) => {
    // message: Сообщение для логирования
    console.warn('Warning message:', message);
    return message;
});
```

### Error
The hook is called when logging errors.

```typescript
loggerHooks.Error.tap('MyHook', (message) => {
    // message: Сообщение для логирования
    console.error('Error message:', message);
    return message;
});
```

## Service API

### The setup method

Configures logger parameters.

**Parameters:**
- `options: {quiet?: boolean}` — configuration options
  - `quiet` — disables informational messages

**Returns:**
- `Logger` — the current logger instance.

```typescript
logger.setup({quiet: true});
```

### The pipe method

Redirects logs to another logger.

**Parameters:**
- `consumer: LogConsumer` — the target logger.

**Returns:**
- `Logger` — the current logger instance.

```typescript
logger.pipe(anotherLogger);
```

### The topic method

Creates a new logging topic.

**Parameters:**
- `level: LogLevels` — logging level.
- `prefix: string` — message prefix.
- `color?: Color` — prefix color.

**Returns:**
- `(...messages: unknown[]) => void` — logging function.

```typescript
const myTopic = logger.topic(LogLevel.INFO, 'MY_TOPIC', gray);
myTopic('Message');
```

### The reset method

Resets message counters.

**Returns:**
- `Logger` — the current logger instance.

```typescript
logger.reset();
```

### Methods

#### info
Method for logging informational messages.

```typescript
logger.info('Information message');
```

#### warn
Method for logging warnings.

```typescript
logger.warn('Warning message');
```

#### error
Method for logging errors.

```typescript
logger.error('Error message');
```

## Usage examples

### Creating a custom logger

```typescript
export class CustomLogger extends Logger {
    readonly process = this.topic(LogLevel.INFO, 'PROCESS', gray);
    readonly validate = this.topic(LogLevel.INFO, 'VALIDATE', gray);
    readonly transform = this.topic(LogLevel.INFO, 'TRANSFORM', gray);
    
    readonly processError = this.topic(LogLevel.ERROR, 'PROCESS_ERROR');
    readonly validateError = this.topic(LogLevel.ERROR, 'VALIDATE_ERROR');
    readonly transformError = this.topic(LogLevel.ERROR, 'TRANSFORM_ERROR');
}
```

### Message filtering

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MessageFilter', (run) => {
            const logger = run.logger;
            
            // Добавляем фильтр для сообщений
            logger.filters.push((level, message) => {
                if (level === LogLevel.INFO && message.includes('sensitive')) {
                    return ''; // Пропускаем сообщение
                }
                return message;
            });
        });
    }
}
```

### Collecting log statistics

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('LogStats', (run) => {
            const logger = run.logger;
            
            // Собираем статистику по логам
            const stats = {
                info: logger.info.count,
                warn: logger.warn.count,
                error: logger.error.count
            };
            
            console.log('Log statistics:', stats);
        });
    }
}
```

### Redirecting logs to a file

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('FileLogger', (run) => {
            const logger = run.logger;
            const fileLogger = new FileLogger('logs.txt');
            
            // Перенаправляем логи в файл
            logger.pipe(fileLogger);
        });
    }
}
``` 