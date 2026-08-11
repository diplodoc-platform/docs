# Diplodoc services

Services are the main components of Diplodoc, responsible for various aspects of documentation processing. Each service provides its own set of hooks for extending functionality.

## Available services

- [TOC Service](./services/toc-service.md) — managing the documentation structure.
- [Leading Service](./services/leading-service.md) — processing leading pages.
- [Markdown Service](./services/markdown-service.md) — transforming markdown content.
- [Meta Service](./services/meta-service.md) — working with documentation metadata.
- [Vars Service](./services/vars-service.md) — managing variables and templates.
- [VCS Service](./services/vcs-service.md) — working with the version control system.
- [Search Service](./services/search-service.md) — organizing search across documentation.
- [Logger Service](./services/logger-service.md) — managing logging.

## Working with Services

### Accessing services

All services are available through the execution context `run`, which is passed to hooks:

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MyExtension', (run) => {
            // Доступ к сервисам
            const {toc, markdown, leading} = run;
        });
    }
}
```

### Getting service hooks

To work with a service, you need to get its hooks using the corresponding function:

```typescript
import {getHooks as getBaseHooks} from '@diplodoc/cli/lib/program';
import {getHooks as getTocHooks} from '@diplodoc/cli/lib/toc';
import {getHooks as getMarkdownHooks} from '@diplodoc/cli/lib/markdown';
import {getHooks as getLeadingHooks} from '@diplodoc/cli/lib/leading';

export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MyExtension', (run) => {
            // Получение хуков сервисов
            const tocHooks = getTocHooks(run.toc);
            const markdownHooks = getMarkdownHooks(run.markdown);
            const leadingHooks = getLeadingHooks(run.leading);
        });
    }
}
```

### Using hooks

Service hooks follow a common usage pattern:

```typescript
serviceHooks.HookName.tap('ExtensionName', (data) => {
    // Синхронная обработка
    return modifiedData;
});

// или

serviceHooks.HookName.tapPromise('ExtensionName', async (data) => {
    // Асинхронная обработка
    return modifiedData;
});
```

### Service API

Each service, in addition to hooks, provides a set of methods for working with data:

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MyExtension', (run) => {
            // TOC Service API
            const tocPath = run.toc.dir(entry);      // Получение директории TOC
            const tocData = run.toc.data(entry);     // Получение данных TOC
            const entries = run.toc.entries;         // Список всех entry в TOC
            
            // Leading Service API
            const hasLeading = run.leading.has(path);    // Проверка наличия leading-страницы
            const leadingData = run.leading.get(path);   // Получение данных leading-страницы
            
            // Markdown Service API
            const content = run.markdown.read(path);     // Чтение markdown-файла
            await run.markdown.save(path, content);      // Сохранение markdown-файла
        });
    }
}
```

Using service APIs instead of working directly with the file system allows you to:
- Get data in the correct build context
- Use internal caching
- Support various data formats and sources
- Ensure data consistency

## Best practices

### 1. Logic isolation

Separate processing logic across the appropriate services:

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MyExtension', (run) => {
            // TOC-специфичная логика
            const tocHooks = getTocHooks(run.toc);
            tocHooks.Item.tap('MyExtension', (item) => {
                // Работа со структурой
                return item;
            });

            // Markdown-специфичная логика
            const markdownHooks = getMarkdownHooks(run.markdown);
            markdownHooks.Resolved.tap('MyExtension', (content) => {
                // Работа с контентом
                return content;
            });
        });
    }
}
```

### 2. Error handling

Always handle possible errors in hooks:

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MyExtension', (run) => {
            const tocHooks = getTocHooks(run.toc);
            
            tocHooks.Item.tapPromise('MyExtension', async (item) => {
                try {
                    const processedItem = await processItem(item);
                    return processedItem;
                } catch (error) {
                    run.logger.error('Failed to process TOC item:', error);
                    return item;
                }
            });
        });
    }
}
```

### 3. Hook execution order

The hook execution order is determined by two factors:

1. **Program lifecycle**: the main hook execution order is determined by the Diplodoc lifecycle. 
<!-- Подробнее об этом можно прочитать в [Extension Lifecycle](../lifecycle.md). -->

2. **Hook configuration**: the capabilities of the [tapable](https://github.com/webpack/tapable) library are used to control the execution order of hooks with the same name:

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap({
            name: 'MyExtension',
            stage: 10, // Более высокий stage выполняется позже
            before: ['OtherExtension'], // Выполнить до указанных расширений
            after: ['AnotherExtension'], // Выполнить после указанных расширений
        }, (run) => {
            // Логика расширения
        });
    }
}
```

You can also use different hook types for specific scenarios:
- `tap` - synchronous hook
- `tapAsync` - asynchronous hook with callback
- `tapPromise` - asynchronous hook with Promise
- `intercept` - for intercepting hook calls

<!-- ## Дополнительная информация

- [Core Concepts](./core-concepts.md) - базовые концепции архитектуры
- [Extension Lifecycle](../lifecycle.md) - жизненный цикл расширений
- [Examples](../examples.md) - примеры использования сервисов -->