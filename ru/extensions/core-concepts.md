# Основные концепции

API расширений Diplodoc построено вокруг нескольких ключевых концепций, которые работают вместе, чтобы обеспечить гибкую и мощную систему расширений.

## Интерфейс расширения

Любое расширение должно реализовывать интерфейс `IExtension`:

```typescript
interface IExtension<Program extends BaseProgram = BaseProgram> {
    apply(program: Program): void;
}
```

Основные моменты:
- Каждое расширение должно иметь метод `apply`
- Через метод `apply` расширение получает доступ к экземпляру программы
- Метод `apply` вызывается при инициализации каждой команды
  - Например, если у вас есть команды `build`, `translate`, `publish`, то `apply` будет вызван три раза
  - Дополнительно `apply` вызывается при инициализации корневой программы
- Ограничения:
  - Расширение не может быть уверено, с какой именно командой оно работает в данный момент
  - Это накладывает определенные ограничения на логику работы расширения
- Работа с хуками:
  - Получив доступ к программе, расширение может подписаться на ее хуки
  - Попытка подписаться на хуки чужой программы будет проигнорирована
  - Например, если расширение вызывается для программы `translate`, то `getBuildHooks(program)` вернет набор хуков, который никогда не будет вызван
  - Это позволяет подписываться на хуки программы, не задумываясь о том, с какой именно программой вы работаете в данный момент

## Архитектура программы

### BaseProgram

Класс `BaseProgram` является основой CLI Diplodoc:

```typescript
export class BaseProgram<TConfig extends BaseConfig = BaseConfig, TArgs extends BaseArgs = BaseArgs> {
    readonly name: string;
    readonly command: Command;
    readonly config: Config<TConfig>;
    readonly logger: Logger;
    readonly options: ExtendedOption[];
    protected modules: ICallable[];
    protected extensions: (string | ExtensionInfo)[];
}
```

Ключевые компоненты:
- **name**: Уникальный идентификатор программы
- **command**: Экземпляр CLI команды
- **config**: Конфигурация программы
- **logger**: Система логирования
- **options**: Опции командной строки
- **modules**: Список расширений и подпрограмм
- **extensions**: Конфигурации расширений

### Система хуков

Система хуков основана на [tapable](https://github.com/webpack/tapable) и предоставляет несколько типов хуков:

```typescript
export function hooks<TRun extends Run, TConfig extends BaseConfig, TArgs extends BaseArgs>(name: string) {
    return {
        Command: new SyncHook<[Command, ExtendedOption[]]>(),
        RawConfig: new AsyncSeriesHook<[DeepFrozen<TConfig>, TArgs]>(),
        Config: new AsyncSeriesWaterfallHook<[TConfig, TArgs]>(),
        BeforeAnyRun: new AsyncSeriesHook<[TRun]>(),
        AfterAnyRun: new AsyncSeriesHook<[TRun]>()
    };
}
```

## Система конфигурации

Расширения могут быть настроены двумя способами:

### 1. Конфигурация через файл

```json
{
    "extensions": [
        {
            "path": "./my-extension",
            "options": {
                "setting1": "value1",
                "setting2": "value2"
            }
        }
    ]
}
```

### 2. Программная конфигурация

```typescript
class Build extends BaseProgram {
    readonly modules = [
        new MyExtension({
            setting1: "value1",
            setting2: "value2"
        })
    ];
}
```

## Контекст выполнения

Класс `Run` предоставляет контекст для обработки документов:

```typescript
export class Run extends BaseRun<BuildConfig> {
    readonly vars: VarsService;
    readonly meta: MetaService;
    readonly toc: TocService;
    readonly vcs: VcsService;
    readonly leading: LeadingService;
    readonly markdown: MarkdownService;
    readonly search: SearchService;
    readonly logger: Logger;
}
```

Services available in Run:
- **vars**: Variable management
- **meta**: Metadata handling
- **toc**: Table of contents processing
- **vcs**: Version control integration
- **leading**: Leading content processing
- **markdown**: Markdown processing
- **search**: Search functionality
- **logger**: Logging system

## Extension Types

### 1. Command Extensions
Modify CLI behavior and options:

```typescript
export class CommandExtension {
    apply(program: Build) {
        getBaseHooks(program).Command.tap('MyCommand', (command) => {
            command.addOption(new Option('--my-option'));
        });
    }
}
```

### 2. Processing Extensions
Add custom processing steps:

```typescript
export class ProcessingExtension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tapPromise('MyProcessor', async (run) => {
            // Process files
            const files = await run.glob('**/*.md');
            for (const file of files) {
                // Custom processing
            }
        });
    }
}
```

### 3. Configuration Extensions
Modify or validate configuration:

```typescript
export class ConfigExtension {
    apply(program: Build) {
        getBaseHooks(program).Config.tapPromise('MyConfig', async (config) => {
            // Modify configuration
            config.customSetting = 'value';
            return config;
        });
    }
}
```

## Error Handling

Extensions should use the `HandledError` class for expected errors:

```typescript
export class ErrorHandlingExtension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tapPromise('MyExtension', async (run) => {
            try {
                // Extension logic
            } catch (error) {
                run.logger.error('Extension error:', error);
                throw new HandledError('Extension failed');
            }
        });
    }
}
```

## Next Steps

- Learn about the [Extension Lifecycle](./lifecycle.md)
- See [Creating Extensions](./creating-extensions.md) for practical examples
- Check the [API Reference](./api-reference.md) for detailed documentation 