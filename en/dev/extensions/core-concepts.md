# Extension Development Principles

## Extension Interface

Any extension must implement the `IExtension` interface:

```typescript
interface IExtension<Program extends BaseProgram = BaseProgram> {
    apply(program: Program): void;
}
```

Each extension module must export a class named `Extension`. The system will look for exactly this class name when loading the extension.

```typescript
// ✅ Правильно - имя класса 'Extension'
export class Extension {
    apply(program: Build) {
        // Extension logic
    }
}

// ❌ Неправильно - другое имя класса
export class MyCustomExtension {
    apply(program: Build) {
        // Этот class не будет загружен системой
    }
}
```

## Extension Initialization

- Each extension must have an `apply` method.
- Through the `apply` method, the extension gains access to a program instance.
- The `apply` method is called during the initialization of each command.
  - For example, if you have commands `build`, `translate`, `publish`, then `apply` will be called three times,
  - Additionally, `apply` is called during the initialization of the root program.
- Once it has access to the program, the extension can subscribe to its hooks.
- Attempts to subscribe to hooks of another program will be ignored. This allows you to subscribe to program hooks without worrying about which specific program you are working with at the moment.

    {% note info %}

    For example, if the extension is called for the `translate` program, then `getBuildHooks(program)` will return a set of hooks that will never be called.

    {% endnote %}

- The extension cannot be sure which specific command it is working with at the moment. This imposes certain limitations on the extension's logic.
- It is not recommended to store state between `apply` calls.

## Basic Principles of Working with Hooks

### Hook Types

Diplodoc uses the following hook types:

1. ##**SyncHook**## — a synchronous hook, called sequentially,
2. ##**AsyncSeriesHook**## — an asynchronous hook, called sequentially,
3. ##**AsyncParallelHook**## — an asynchronous hook, called in parallel,
4. ##**AsyncSeriesWaterfallHook**## — an asynchronous hook where the result of the previous handler is passed to the next one.

### Subscribing to Hooks

The following methods are used to subscribe to hooks:
- `tap` — for synchronous hooks,
- `tapPromise` — for asynchronous hooks,
- `tapAsync` — for asynchronous hooks with a callback.

```typescript
// Подписка на синхронный хук
hooks.Command.tap('MyExtension', (command) => {
    // Обработка команды
});

// Подписка на асинхронный хук
hooks.BeforeAnyRun.tapPromise('MyExtension', async (run) => {
    // Асинхронная обработка
});

// Подписка на waterfall хук
hooks.Config.tapPromise('MyExtension', async (config) => {
    // Модификация конфигурации
    return config;
});
```

### Execution Order

1. Hooks are executed in the order they are registered.
2. For ##AsyncSeriesHook## and ##AsyncSeriesWaterfallHook##, handlers are executed sequentially.
3. For ##AsyncParallelHook##, handlers are executed in parallel.
4. For ##AsyncSeriesWaterfallHook##, the result of the previous handler is passed to the next one.

### Error handling

- Synchronous hooks: errors are handled via ##try/catch##
- Asynchronous hooks: errors are handled via ##Promise.catch## or ##try/catch## in async functions

```typescript
// Обработка ошибок в асинхронном хуке
hooks.BeforeAnyRun.tapPromise('MyExtension', async (run) => {
    try {
        // Логика расширения
    } catch (error) {
        run.logger.error('Extension error:', error);
        throw new HandledError('Extension failed');
    }
});
```

### Best practices

1. Always specify a unique name for the hook handler.
2. Use the correct hook type depending on the task.
3. Handle errors in asynchronous hooks.
4. Do not block execution in synchronous hooks.
5. Use ##AsyncSeriesWaterfallHook## to modify data.

## Program architecture

### BaseProgram

The `BaseProgram` class is the foundation of the Diplodoc CLI:

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

Key components:
- **name**: Unique program identifier
- **command**: CLI command instance
- **config**: Program configuration
- **logger**: Logging system
- **options**: Command-line options
- **modules**: List of extensions and subprograms
- **extensions**: Extension configurations

### Hook system

The hook system is based on [tapable](https://github.com/webpack/tapable) and provides several hook types:

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

## Configuration system

Extensions can be configured in two ways:

### 1. File-based configuration

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

### 2. Programmatic configuration

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

## Execution context

The `Run` class provides context for processing documents:

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

<!-- ## Next Steps

- Learn about the [Extension Lifecycle](./lifecycle.md)
- See [Creating Extensions](./creating-extensions.md) for practical examples
- Check the [API Reference](./api-reference.md) for detailed documentation  -->