# Diplodoc Extensions API

Diplodoc Extensions API предоставляет мощный механизм для расширения функциональности Diplodoc CLI. Построенный на hook-based системе и базовом program class, он позволяет создавать модульные, расширяемые и легко интегрируемые компоненты.

## Ключевые особенности

- **Hook-based Architecture**: Используйте продвинутую систему hooks для расширения функциональности на различных этапах процесса сборки документации
- **Type Safety**: Полная поддержка TypeScript с подробными определениями типов
- **Modular Design**: Создавайте независимые, переиспользуемые extensions
- **Configuration Support**: Гибкая настройка через файлы конфигурации и параметры командной строки
- **Resource Management**: Встроенные lifecycle hooks для правильной инициализации и очистки ресурсов
- **Logging and Debugging**: Интегрированная система логирования с несколькими уровнями детализации

## Базовые концепции

### Program и Run

В основе архитектуры Diplodoc лежат два ключевых класса:

1. **Program** - базовый класс для всех команд CLI. Он предоставляет:
   - Систему hooks для расширения функциональности
   - Управление конфигурацией
   - Доступ к логированию
   - Интерфейс для регистрации extensions

2. **Run** - контекст выполнения команды. Содержит:
   - Доступ к сервисам (TOC, Markdown, Leading и др.)
   - Информацию о текущем состоянии
   - Утилиты для работы с файлами
   - Системы логирования и отладки

### Hooks и их использование

Hooks - это основной механизм расширения функциональности. Они позволяют:
- Встраиваться в различные этапы выполнения программы
- Модифицировать поведение сервисов
- Добавлять новую функциональность

Существует два типа hooks:
1. **Base Hooks** - общие hooks программы:
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

2. **Service Hooks** - специфичные для каждого сервиса:
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

### Работа с сервисами

Сервисы - это основные компоненты Diplodoc, отвечающие за различные аспекты обработки документации. Доступ к сервисам осуществляется через контекст `run`:

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MyExtension', (run) => {
            // Доступ к сервисам
            const {toc, markdown, leading} = run;
            
            // Получение hooks сервисов
            const tocHooks = getTocHooks(toc);
            const markdownHooks = getMarkdownHooks(markdown);
            const leadingHooks = getLeadingHooks(leading);
        });
    }
}
```

Подробное описание каждого сервиса:
- [TOC Service](./toc-service.md) - управление структурой документации
- [Leading Service](./leading-service.md) - обработка страниц оглавления
- [Markdown Service](./markdown-service.md) - трансформация markdown-контента

## Important Note

Каждый extension module ОБЯЗАТЕЛЬНО должен экспортировать class с именем `Extension`. Это строгое требование Diplodoc extension system. Система будет искать именно это имя класса при загрузке extensions.

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

## When to Use Extensions

Extensions особенно полезны, когда вам нужно:

1. Добавить новые параметры командной строки в Diplodoc CLI
2. Модифицировать или улучшить процесс сборки документации
3. Добавить поддержку новых типов файлов или методов обработки
4. Интегрироваться с внешними сервисами или API
5. Добавить пользовательские шаги валидации или трансформации

## Extension Types

Diplodoc поддерживает несколько типов extensions, каждый из которых предназначен для решения определенных задач:

### 1. Command Extensions
Этот тип extensions позволяет модифицировать CLI-интерфейс Diplodoc. Используйте его, когда нужно:
- Добавить новые команды в CLI
- Расширить существующие команды новыми параметрами
- Изменить поведение существующих команд

В примере ниже показано, как добавить новый параметр к команде:

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).Command.tap('MyCommand', (command) => {
            command.addOption(new Option('--my-option'));
        });
    }
}
```

### 2. Processing Extensions
Processing Extensions предназначены для модификации процесса сборки документации. Они особенно полезны, когда вам нужно:
- Изменить содержимое или структуру TOC
- Трансформировать markdown-контент
- Добавить пользовательские включатели
- Выполнить валидацию контента во время сборки

Пример processing extension:

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

### 3. Integration Extensions
Integration Extensions обеспечивают взаимодействие Diplodoc с внешними сервисами. Используйте их для:
- Загрузки данных из внешних API
- Обогащения документации внешними метаданными
- Синхронизации с другими системами
- Отправки уведомлений или метрик

Пример integration extension:

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

## Getting Started

1. **Установка**
   ```bash
   npm install @diplodoc/cli
   ```

2. **Базовый шаблон расширения**
   ```typescript
   // my-extension.ts
   import type {Build} from '~/commands/build';
   import {getHooks as getBaseHooks} from '~/core/program';

   export class Extension {
       apply(program: Build) {
           getBaseHooks(program).BeforeAnyRun.tapPromise('MyExtension', async (run) => {
               run.logger.info('MyExtension is running');
           });
       }
   }
   ```

3. **Регистрация**
   ```typescript
   // В файле конфигурации
   {
       "extensions": [
           {
               "path": "./my-extension",
               "options": {
                   "key": "value"
               }
           }
       ]
   }
   ```

## Next Steps

- Изучите [Core Concepts](./core-concepts.md) для понимания архитектуры
- Узнайте о [Extension Lifecycle](./lifecycle.md) и доступных hooks
- Следуйте руководству [Creating Extensions](./creating-extensions.md) для подробного изучения
- Посмотрите [Examples](./examples.md) для практических примеров использования 