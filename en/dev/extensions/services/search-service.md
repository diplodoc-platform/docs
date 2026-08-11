# Search Service

Search Service is designed to organize documentation search.

## Main features

- Support for various search providers.
- Search index generation.
- Multilingual support.
- Integration with the client side.

## Accessing the service

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MyExtension', (run) => {
            // Получение сервиса из контекста
            const {search} = run;
            
            // Получение хуков сервиса
            const searchHooks = getSearchHooks(search);
        });
    }
}
```

## Available hooks

### Page
Hook for modifying the search page.

```typescript
searchHooks.Page.tap('MyHook', (template) => {
    // template: Шаблон страницы поиска
    template.addMeta({custom: 'value'});
});
```

### Provider
Hook for registering and configuring search providers.

```typescript
searchHooks.Provider.tap('MyProvider', (provider, config) => {
    // provider: Текущий провайдер
    // config: Конфигурация провайдера
    return new CustomSearchProvider(config);
});
```

## Service API

### Method init

Initializes the service by loading the search provider.

```typescript
await searchService.init();
```

### Method config

Gets the search configuration for the specified language.

**Parameters:**
- `lang: string` — language code.

**Returns:**
- `SearchAppConfig | undefined` — search configuration or ##undefined## if search is disabled.

```typescript
const config = searchService.config('ru');
```

### Method add

Adds a document to the search index.

**Parameters:**
- `path: RelativePath` — path to the document.
- `lang: string` — language code.
- `info: EntryInfo` — document information.

```typescript
await searchService.add('path/to/doc.md', 'ru', info);
```

### Method release

Releases the search provider resources.

```typescript
await searchService.release();
```

### Method page

Generates the search page for the specified language.

**Parameters:**
- `lang: string` — language code.

**Returns:**
- `Promise<string>` — search page HTML.

```typescript
const html = await searchService.page('ru');
```

### Properties

#### enabled
Flag indicating whether search is enabled.

```typescript
if (searchService.enabled) {
    // Поиск включен
}
```

#### connected
Flag indicating whether a custom provider is connected.

```typescript
if (searchService.connected) {
    // Пользовательский провайдер подключен
}
```

## Usage examples

### Creating a custom provider

```typescript
export class CustomSearchProvider implements SearchProvider {
    async add(path: RelativePath, lang: string, info: EntryInfo) {
        // Добавление документа в индекс
    }

    async release() {
        // Освобождение ресурсов
    }

    config(lang: string) {
        return {
            enabled: true,
            // Дополнительные настройки
        };
    }
}
```

### Provider registration

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('CustomSearch', (run) => {
            const searchHooks = getSearchHooks(run.search);
            
            searchHooks.Provider.tap('CustomSearch', (provider, config) => {
                return new CustomSearchProvider(config);
            });
        });
    }
}
```

### Modifying the search page

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('SearchPageModifier', (run) => {
            const searchHooks = getSearchHooks(run.search);
            
            searchHooks.Page.tap('SearchPageModifier', (template) => {
                // Добавление пользовательских стилей
                template.addStyle('custom-search.css');
                
                // Добавление пользовательских скриптов
                template.addScript('custom-search.js');
            });
        });
    }
}
```

### Integration with an external search service

```typescript
export class ExternalSearchProvider implements SearchProvider {
    constructor(private apiKey: string) {}
    
    async add(path: RelativePath, lang: string, info: EntryInfo) {
        // Отправка документа во внешний сервис
        await this.externalService.index(path, lang, info);
    }
    
    async release() {
        // Закрытие соединения с внешним сервисом
        await this.externalService.close();
    }
    
    config(lang: string) {
        return {
            enabled: true,
            apiKey: this.apiKey,
            // Дополнительные настройки
        };
    }
}
``` 