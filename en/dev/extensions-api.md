# Diplodoc Extensions API

The Diplodoc Extensions API provides a mechanism for extending the functionality of the Diplodoc CLI. Built on a hook-based system using the [tappable](https://github.com/webpack/tapable) library, it allows creating modular, integrable, and extensible components.

The CLI's internal modules are built on the Extensions API architecture.

## Features

- **Hook-based Architecture**: A hook system for extending functionality at various stages of the documentation build process.
- **Type Safety**: Full TypeScript support with detailed type definitions.
- **Modular Design**: Creation of independent, reusable extensions.
- **Configuration Support**: Flexible configuration via configuration files and command-line parameters.
- **Resource Management**: Built-in lifecycle hooks for proper initialization and cleanup of resources.
- **Logging and Debugging**: Integrated logging system with multiple levels of detail.

## Basic Concepts

### Program and Run

At the core of the Diplodoc architecture are two key classes:

1. ##**Program**## — the base class for all CLI commands. It provides:
   - A hook system for extending functionality
   - Configuration management
   - Access to logging
   - An interface for registering extensions

2. ##**Run**## — the command execution context. It contains:
   - Access to services (TOC, Markdown, Leading, etc.)
   - Information about the current state
   - Utilities for working with files
   - Logging and debugging systems

### Hooks and Their Usage

Hooks are the primary mechanism for extending functionality. They allow you to:
- Integrate into various stages of program execution
- Modify service behavior
- Add new functionality

There are two types of hooks:
1. **Base Hooks** — common program hooks:
   ```typescript
   export class Extension {
       apply(program: Build) {
           // Получение базовых hooks
           const baseHooks = getBaseHooks(program);
           
           // Hook перед любым запуском
           baseHooks.BeforeAnyRun.tap('MyExtension', (run) => {
               // Инициализация
           });
           
           // Hook после выполнения
           baseHooks.AfterAnyRun.tap('MyExtension', (run) => {
               // Очистка
           });
       }
   }
   ```

2. **Service Hooks** — specific to each service:
   ```typescript
   export class Extension {
       apply(program: Build) {
           getBaseHooks(program).BeforeAnyRun.tap('MyExtension', (run) => {
               // Получение hooks конкретного сервиса
               const tocHooks = getTocHooks(run.toc);
               const markdownHooks = getMarkdownHooks(run.markdown);
               const leadingHooks = getLeadingHooks(run.leading);
               
               // Использование hooks
               tocHooks.Item.tap('MyExtension', (item) => {
                   // Обработка элемента TOC
               });
           });
       }
   }
   ```

### Working with Services

Services are the main components of Diplodoc, responsible for various aspects of documentation processing.
Access to services is provided through the `run` context:

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MyExtension', (run) => {
            // Доступ к сервисам
            const {toc, markdown, leading, meta, vars} = run;
            
            // Получение hooks сервисов
            const tocHooks = getTocHooks(toc);
            const markdownHooks = getMarkdownHooks(markdown);
            const leadingHooks = getLeadingHooks(leading);
            const metaHooks = getMetaHooks(meta);
            const varsHooks = getVarsHooks(vars);
        });
    }
}
```

Detailed description of each service:
- [TOC Service](./extensions/services/toc-service.md) — managing the documentation structure.
- [Leading Service](./extensions/services/leading-service.md) — processing leading pages.
- [Markdown Service](./extensions/services/markdown-service.md) — transforming markdown content.
- [Meta Service](./extensions/services/meta-service.md) — working with documentation metadata.
- [Vars Service](./extensions/services/vars-service.md) — managing variables and templates.
- [VCS Service](./extensions/services/vcs-service.md) — working with a version control system.
- [Search Service](./extensions/services/search-service.md) — organizing documentation search.
- [Logger Service](./extensions/services/logger-service.md) — managing logging.

## When to use extensions

Extensions are especially useful when you need to:

1. Add new command-line parameters to the Diplodoc CLI.
2. Modify or improve the documentation build process.
3. Add support for new file types or processing methods.
4. Integrate with external services or APIs.
5. Add custom validation or document transformation steps.

## Types of extensions

Diplodoc supports several types of extensions, each designed to solve specific tasks:

### 1. Command Extensions

This type of extension allows you to modify the Diplodoc CLI interface. Use it when you need to:
- add new commands to the CLI,
- extend existing commands with new parameters,
- change the behavior of existing commands.

The example below shows how to add a new parameter to a command:

{% cut "Example of adding a new parameter to a command" "%}

```typescript
import {Build} from '@diplodoc/cli';

export class Extension {
    apply(program) {
        if (Build.is(program)) {
           getBaseHooks(program).Command.tap('MyCommand', (command) => {
              command.addOption(new Option('--my-option'));
           }); 
        }
    }
}
```

{% endcut %}

### 2. Processing Extensions

Processing Extensions are designed to modify the documentation build process. They are especially useful when you need to:
- change the content or structure of the TOC,
- transform markdown content,
- add custom includers,
- perform content validation during the build.

{% cut "Example extension" "%}

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MyProcessor', (run) => {
            // Получение hooks нужных сервисов
            const tocHooks = getTocHooks(run.toc);
            const markdownHooks = getMarkdownHooks(run.markdown);
            
            // Настройка обработки
            tocHooks.Item.tapPromise('MyProcessor', async (item) => {
                // Обработка элемента TOC
                return item;
            });
            
            markdownHooks.Resolved.tapPromise('MyProcessor', async (content) => {
                // Обработка markdown
                return content;
            });
        });
    }
}
```

{% endcut %}


### 3. Integration Extensions

Integration Extensions enable Diplodoc to interact with external services. Use them for:
- loading data from external APIs,
- enriching documentation with external metadata,
- synchronizing with other systems,
- sending notifications or metrics.

Example extension:

```typescript
export class Extension {
    constructor(private apiKey: string) {}
    
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MyIntegration', (run) => {
            // Интеграция с внешним API
            getLeadingHooks(run.leading).Resolved.tapPromise('MyIntegration', async (content) => {
                const externalData = await this.fetchExternalData(this.apiKey);
                return {
                    ...content,
                    externalData
                };
            });
        });
    }

    private async fetchExternalData(apiKey: string) {
        // Логика получения данных из внешнего API
    }
}
```

<!-- ## Связанные разделы

- Изучите [Core Concepts](./extensions/core-concepts.md) для понимания архитектуры
- Узнайте о [Extension Lifecycle](./lifecycle.md) и доступных hooks
- Следуйте руководству [Creating Extensions](./creating-extensions.md) для подробного изучения
- Посмотрите [Examples](./examples.md) для практических примеров использования  -->