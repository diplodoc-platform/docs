# Основные концепции

API расширений Diplodoc построено вокруг нескольких ключевых концепций, которые работают вместе, чтобы обеспечить гибкую и мощную систему расширений.

## Интерфейс расширения

Любое расширение должно реализовывать интерфейс `IExtension`:

```typescript
interface IExtension<Program extends BaseProgram = BaseProgram> {
    apply(program: Program): void;
}
```

Каждый extension module должен экспортировать class с именем `Extension`. Система будет искать именно это имя класса при загрузке extensions.

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

## Инициализация расширения

- Каждое расширение должно иметь метод `apply`
- Через метод `apply` расширение получает доступ к экземпляру программы.
- Метод `apply` вызывается при инициализации каждой команды
  - Например, если у вас есть команды `build`, `translate`, `publish`, то `apply` будет вызван три раза,
  - Дополнительно `apply` вызывается при инициализации корневой программы.
- Получив доступ к программе, расширение может подписаться на ее хуки.
- Попытка подписаться на хуки другой программы будет проигнорирована. Это позволяет подписываться на хуки программы, не задумываясь о том, с какой именно программой вы работаете в данный момент.

    {% note %}

    Например, если расширение вызывается для программы `translate`, то `getBuildHooks(program)` вернет набор хуков, который никогда не будет вызван

    {% endnote %}

- Расширение не может быть уверено, с какой именно командой оно работает в данный момент. Это накладывает определенные ограничения на логику работы расширения.
- Не рекомендуется сохранять состояние между вызовами `apply`

<!-- {% note %}

Подробнее про работу с базовыми хуками можно почитать в руководстве [{#T}](./guides/use-hooks.md)

{% endnote %} -->

## Основные принципы работы с хуками

### Типы хуков

В Diplodoc используются следующие типы хуков:

1. **SyncHook** - синхронный хук, вызывается последовательно
2. **AsyncSeriesHook** - асинхронный хук, вызывается последовательно
3. **AsyncParallelHook** - асинхронный хук, вызывается параллельно
4. **AsyncSeriesWaterfallHook** - асинхронный хук, где результат предыдущего обработчика передается следующему

### Подписка на хуки

Для подписки на хуки используются методы:
- `tap` - для синхронных хуков
- `tapPromise` - для асинхронных хуков
- `tapAsync` - для асинхронных хуков с callback

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

### Порядок выполнения

1. Хуки выполняются в порядке их регистрации
2. Для AsyncSeriesHook и AsyncSeriesWaterfallHook обработчики выполняются последовательно
3. Для AsyncParallelHook обработчики выполняются параллельно
4. Для AsyncSeriesWaterfallHook результат предыдущего обработчика передается следующему

### Обработка ошибок

- Синхронные хуки: ошибки обрабатываются через try/catch
- Асинхронные хуки: ошибки обрабатываются через Promise.catch или try/catch в async функциях

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

### Лучшие практики

1. Всегда указывайте уникальное имя для обработчика хука
2. Используйте правильный тип хука в зависимости от задачи
3. Обрабатывайте ошибки в асинхронных хуках
4. Не блокируйте выполнение в синхронных хуках
5. Для модификации данных используйте AsyncSeriesWaterfallHook

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

<!-- ## Next Steps

- Learn about the [Extension Lifecycle](./lifecycle.md)
- See [Creating Extensions](./creating-extensions.md) for practical examples
- Check the [API Reference](./api-reference.md) for detailed documentation  -->