# Diplodoc Extensions API

Diplodoc Extensions API предоставляет мощный механизм для расширения функциональности Diplodoc CLI. Построенный на hook-based системе на основе библиотеки [tappable](https://github.com/webpack/tapable), он позволяет создавать модульные, расширяемые и легко интегрируемые компоненты.

На базе архитектуры Extensions API так же построены все внутренние модули CLI.

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
   - Систему хуков для расширения функциональности
   - Управление конфигурацией
   - Доступ к логированию
   - Интерфейс для регистрации расширений

2. **Run** - контекст выполнения команды. Содержит:
   - Доступ к сервисам (TOC, Markdown, Leading и др.)
   - Информацию о текущем состоянии
   - Утилиты для работы с файлами
   - Системы логирования и отладки

### Хуки и их использование

Хуки - это основной механизм расширения функциональности. Они позволяют:
- Встраиваться в различные этапы выполнения программы
- Модифицировать поведение сервисов
- Добавлять новую функциональность

Существует два типа хуков:
1. **Base Hooks** - общие хуки программы:
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

Сервисы - это основные компоненты Diplodoc, отвечающие за различные аспекты обработки документации.
Доступ к сервисам осуществляется через контекст `run`:

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

Подробное описание каждого сервиса:
- [TOC Service](./extensions/services/toc-service.md) - управление структурой документации
- [Leading Service](./extensions/services/leading-service.md) - обработка страниц оглавления
- [Markdown Service](./extensions/services/markdown-service.md) - трансформация markdown-контента
- [Meta Service](./extensions/services/meta-service.md) - работа с метаданными документации
- [Vars Service](./extensions/services/vars-service.md) - управление переменными и шаблонами

## Когда использовать расширения

Расширения особенно полезны, когда вам нужно:

1. Добавить новые параметры командной строки в Diplodoc CLI
2. Модифицировать или улучшить процесс сборки документации
3. Добавить поддержку новых типов файлов или методов обработки
4. Интегрироваться с внешними сервисами или API
5. Добавить пользовательские шаги валидации или трансформации документов

## Типы расширений

Diplodoc поддерживает несколько типов расширений, каждый из которых предназначен для решения определенных задач:

### 1. Command Extensions

Этот тип расширений позволяет модифицировать CLI-интерфейс Diplodoc. Используйте его, когда нужно:
- Добавить новые команды в CLI
- Расширить существующие команды новыми параметрами
- Изменить поведение существующих команд

В примере ниже показано, как добавить новый параметр к команде:

{% cut "Пример добавления нового параметра к команде" "%}

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

Processing Extensions предназначены для модификации процесса сборки документации. Они особенно полезны, когда вам нужно:
- Изменить содержимое или структуру TOC
- Трансформировать markdown-контент
- Добавить пользовательские включатели
- Выполнить валидацию контента во время сборки

{% cut "Пример processing extension" "%}

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

<!-- ## Связанные разделы

- Изучите [Core Concepts](./extensions/core-concepts.md) для понимания архитектуры
- Узнайте о [Extension Lifecycle](./lifecycle.md) и доступных hooks
- Следуйте руководству [Creating Extensions](./creating-extensions.md) для подробного изучения
- Посмотрите [Examples](./examples.md) для практических примеров использования  -->