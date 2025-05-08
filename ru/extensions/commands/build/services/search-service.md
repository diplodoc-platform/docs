# Search Service

Search Service предоставляет функциональность для организации поиска по документации. Сервис поддерживает различные типы поисковых систем, включая локальный поиск и интеграцию с внешними поисковыми сервисами.

## Основные возможности

- Создание и управление поисковым индексом
- Поддержка различных поисковых систем (lunr.js, Algolia и др.)
- Гибкая настройка параметров поиска
- Интеграция с внешними поисковыми сервисами
- Кэширование результатов поиска

## Hooks

Search Service предоставляет следующие hooks:

### `Index`
```typescript
searchHooks.Index.tap('MyExtension', (index) => {
    // Модификация поискового индекса
    return index;
});
```
Позволяет модифицировать поисковый индекс перед его использованием.

### `Search`
```typescript
searchHooks.Search.tap('MyExtension', (query, options) => {
    // Обработка поискового запроса
    return results;
});
```
Позволяет модифицировать поисковый запрос или его результаты.

## Примеры использования

### 1. Добавление пользовательских полей в индекс
```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MySearchExtension', (run) => {
            const searchHooks = getSearchHooks(run.search);
            
            searchHooks.Index.tap('MySearchExtension', (index) => {
                // Добавление пользовательских полей в индекс
                return {
                    ...index,
                    customField: 'value'
                };
            });
        });
    }
}
```

### 2. Модификация поискового запроса
```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MySearchExtension', (run) => {
            const searchHooks = getSearchHooks(run.search);
            
            searchHooks.Search.tap('MySearchExtension', (query, options) => {
                // Добавление пользовательской логики поиска
                const modifiedQuery = this.processQuery(query);
                return modifiedQuery;
            });
        });
    }

    private processQuery(query: string): string {
        // Логика обработки запроса
        return query;
    }
}
```

### 3. Интеграция с внешним поисковым сервисом
```typescript
export class Extension {
    constructor(private apiKey: string) {}
    
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MySearchExtension', (run) => {
            const searchHooks = getSearchHooks(run.search);
            
            searchHooks.Search.tapPromise('MySearchExtension', async (query, options) => {
                // Использование внешнего поискового сервиса
                const results = await this.externalSearch(query, options);
                return results;
            });
        });
    }

    private async externalSearch(query: string, options: SearchOptions) {
        // Логика интеграции с внешним сервисом
        return results;
    }
}
```

## Конфигурация

Search Service поддерживает следующие параметры конфигурации:

```typescript
interface SearchConfig {
    // Тип поисковой системы
    type: 'local' | 'algolia' | 'custom';
    
    // Параметры для локального поиска
    local?: {
        // Настройки lunr.js
        lunr?: {
            fields: string[];
            boost: Record<string, number>;
        };
    };
    
    // Параметры для Algolia
    algolia?: {
        appId: string;
        apiKey: string;
        indexName: string;
    };
    
    // Параметры для пользовательской поисковой системы
    custom?: {
        // Пользовательские настройки
    };
}
```

## Best Practices

1. **Оптимизация индекса**
   - Используйте только необходимые поля для индексации
   - Настраивайте веса полей в соответствии с их важностью
   - Регулярно обновляйте индекс при изменении контента

2. **Обработка запросов**
   - Реализуйте кэширование результатов поиска
   - Обрабатывайте ошибки поиска
   - Предоставляйте fallback механизмы

3. **Интеграция с внешними сервисами**
   - Используйте асинхронные операции для внешних запросов
   - Реализуйте механизм повторных попыток
   - Обрабатывайте ограничения API

## См. также

- [TOC Service](./toc-service.md) - для работы со структурой документации
- [Markdown Service](./markdown-service.md) - для обработки контента
- [Leading Service](./leading-service.md) - для работы со страницами оглавления 