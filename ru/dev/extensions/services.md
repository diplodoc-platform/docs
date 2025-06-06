# Сервисы Diplodoc

Сервисы - это основные компоненты Diplodoc, отвечающие за различные аспекты обработки документации. Каждый сервис предоставляет свой набор хуков для расширения функциональности.

## Работа с сервисами

### Получение доступа к сервисам

Все сервисы доступны через контекст выполнения `run`, который передается в хуки:

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

### Получение хуков сервиса

Для работы с сервисом нужно получить его хуки с помощью соответствующей функции:

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

### Использование хуков

Хуки сервисов следуют единому паттерну использования:

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

### API сервисов

Каждый сервис, помимо хуков, предоставляет набор методов для работы с данными:

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

Использование API сервисов вместо прямой работы с файловой системой позволяет:
- Получать данные в правильном контексте сборки
- Использовать внутреннее кеширование
- Поддерживать различные форматы и источники данных
- Обеспечивать консистентность данных

## Доступные сервисы

### [TOC Service](./services/toc-service.md)
Управляет структурой документации (Table of Contents). Позволяет:
- Модифицировать элементы TOC
- Регистрировать пользовательские включатели
- Валидировать структуру документации
- Добавлять метаданные к разделам
- Работать с иерархией документации
- Управлять видимостью разделов

### [Leading Service](./services/leading-service.md)
Отвечает за обработку страниц оглавления (leading pages). Позволяет:
- Обрабатывать метаданные разделов
- Добавлять информацию о разделах
- Интегрироваться с внешними системами
- Управлять контентом ведущих страниц
- Настраивать отображение разделов

### [Markdown Service](./services/markdown-service.md)
Обрабатывает markdown-контент. Позволяет:
- Трансформировать markdown-синтаксис
- Добавлять пользовательские блоки
- Обрабатывать включения
- Валидировать контент
- Управлять форматированием
- Работать с расширенным синтаксисом

### [Meta Service](./services/meta-service.md)
Управляет метаданными документации. Позволяет:
- Работать с метаданными страниц
- Управлять SEO-информацией
- Настраивать отображение в поиске
- Добавлять пользовательские метаданные
- Интегрировать внешние метаданные

### [Vars Service](./services/vars-service.md)
Управляет переменными в документации. Позволяет:
- Определять и использовать переменные
- Создавать пользовательские переменные
- Управлять контекстом переменных
- Интегрировать внешние источники данных
- Настраивать подстановку значений

### [VCS Service](./services/vcs-service.md)
Обеспечивает интеграцию с системами контроля версий. Позволяет:
- Получать информацию о коммитах
- Работать с историей изменений
- Интегрировать данные из VCS
- Управлять версиями документации
- Отслеживать изменения в файлах

### [Search Service](./services/search-service.md)
Управляет поиском по документации. Позволяет:
- Настраивать индексацию контента
- Управлять поисковыми запросами
- Кастомизировать результаты поиска
- Интегрировать внешние поисковые системы
- Оптимизировать поисковую выдачу

### [Logger Service](./services/logger-service.md)
Обеспечивает логирование в системе. Позволяет:
- Настраивать уровни логирования
- Управлять форматами логов
- Интегрировать внешние системы логирования
- Отслеживать ошибки и предупреждения
- Кастомизировать вывод логов

## Best Practices

### 1. Изоляция логики

Разделяйте логику обработки по соответствующим сервисам:

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

### 2. Обработка ошибок

Всегда обрабатывайте возможные ошибки в хуках:

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

### 3. Порядок выполнения хуков

Порядок выполнения хуков определяется двумя факторами:

1. **Жизненный цикл программы**: основной порядок выполнения хуков определяется жизненным циклом Diplodoc. 
<!-- Подробнее об этом можно прочитать в [Extension Lifecycle](../lifecycle.md). -->

2. **Конфигурация хуков**: для управления порядком выполнения хуков с одинаковым именем используются возможности библиотеки [tapable](https://github.com/webpack/tapable):

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

Также можно использовать различные типы хуков для специфических сценариев:
- `tap` - синхронный хук
- `tapAsync` - асинхронный хук с callback
- `tapPromise` - асинхронный хук с Promise
- `intercept` - для перехвата вызовов хука

<!-- ## Дополнительная информация

- [Core Concepts](./core-concepts.md) - базовые концепции архитектуры
- [Extension Lifecycle](../lifecycle.md) - жизненный цикл расширений
- [Examples](../examples.md) - примеры использования сервисов -->