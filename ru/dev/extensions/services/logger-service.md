# Logger

Logger отвечает за логирование в Diplodoc. Этот сервис предоставляет гибкую систему логирования с поддержкой различных уровней логирования, каналов и тем, а также возможностью кастомизации вывода.

## Основные возможности

- Три уровня логирования: info, warning и error
- Поддержка каналов и тем логирования
- Цветной вывод сообщений
- Возможность создания пользовательских тем
- Поддержка фильтрации сообщений
- Возможность перенаправления логов
- Интеграция с хуками для обработки сообщений

## Получение доступа к сервису

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

## Доступные хуки

### Info
Хук вызывается при логировании информационных сообщений.

```typescript
loggerHooks.Info.tap('MyHook', (message) => {
    // message: Сообщение для логирования
    console.log('Info message:', message);
    return message;
});
```

### Warn
Хук вызывается при логировании предупреждений.

```typescript
loggerHooks.Warn.tap('MyHook', (message) => {
    // message: Сообщение для логирования
    console.warn('Warning message:', message);
    return message;
});
```

### Error
Хук вызывается при логировании ошибок.

```typescript
loggerHooks.Error.tap('MyHook', (message) => {
    // message: Сообщение для логирования
    console.error('Error message:', message);
    return message;
});
```

## API сервиса

### Метод setup

Настраивает параметры логгера.

**Параметры:**
- `options: {quiet?: boolean}` - опции настройки
  - `quiet` - отключение информационных сообщений

**Возвращает:**
- `Logger` - текущий экземпляр логгера

```typescript
logger.setup({quiet: true});
```

### Метод pipe

Перенаправляет логи в другой логгер.

**Параметры:**
- `consumer: LogConsumer` - целевой логгер

**Возвращает:**
- `Logger` - текущий экземпляр логгера

```typescript
logger.pipe(anotherLogger);
```

### Метод topic

Создает новую тему логирования.

**Параметры:**
- `level: LogLevels` - уровень логирования
- `prefix: string` - префикс сообщения
- `color?: Color` - цвет префикса

**Возвращает:**
- `(...messages: unknown[]) => void` - функция логирования

```typescript
const myTopic = logger.topic(LogLevel.INFO, 'MY_TOPIC', gray);
myTopic('Message');
```

### Метод reset

Сбрасывает счетчики сообщений.

**Возвращает:**
- `Logger` - текущий экземпляр логгера

```typescript
logger.reset();
```

### Методы

#### info
Метод для логирования информационных сообщений.

```typescript
logger.info('Information message');
```

#### warn
Метод для логирования предупреждений.

```typescript
logger.warn('Warning message');
```

#### error
Метод для логирования ошибок.

```typescript
logger.error('Error message');
```

## Примеры использования

### Создание пользовательского логгера

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

### Фильтрация сообщений

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

### Сбор статистики логов

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

### Перенаправление логов в файл

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