# Search Service

Search Service отвечает за организацию поиска по документации. Сервис предоставляет гибкую систему поиска с поддержкой различных провайдеров и возможностью кастомизации.

## Основные возможности

- Поддержка различных поисковых провайдеров
- Генерация поискового индекса
- Поддержка многоязычности
- Интеграция с клиентской частью

## Получение доступа к сервису

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

## Доступные хуки

### Page
Хук для модификации страницы поиска.

```typescript
searchHooks.Page.tap('MyHook', (template) => {
    // template: Шаблон страницы поиска
    template.addMeta({custom: 'value'});
});
```

### Provider
Хук для регистрации и настройки поисковых провайдеров.

```typescript
searchHooks.Provider.tap('MyProvider', (provider, config) => {
    // provider: Текущий провайдер
    // config: Конфигурация провайдера
    return new CustomSearchProvider(config);
});
```

## API сервиса

### Метод init

Инициализирует сервис, загружая поисковый провайдер.

```typescript
await searchService.init();
```

### Метод config

Получает конфигурацию поиска для указанного языка.

**Параметры:**
- `lang: string` - код языка

**Возвращает:**
- `SearchAppConfig | undefined` - конфигурация поиска или undefined, если поиск отключен

```typescript
const config = searchService.config('ru');
```

### Метод add

Добавляет документ в поисковый индекс.

**Параметры:**
- `path: RelativePath` - путь к документу
- `lang: string` - код языка
- `info: EntryInfo` - информация о документе

```typescript
await searchService.add('path/to/doc.md', 'ru', info);
```

### Метод release

Освобождает ресурсы поискового провайдера.

```typescript
await searchService.release();
```

### Метод page

Генерирует страницу поиска для указанного языка.

**Параметры:**
- `lang: string` - код языка

**Возвращает:**
- `Promise<string>` - HTML страницы поиска

```typescript
const html = await searchService.page('ru');
```

### Свойства

#### enabled
Флаг, указывающий, включен ли поиск.

```typescript
if (searchService.enabled) {
    // Поиск включен
}
```

#### connected
Флаг, указывающий, подключен ли пользовательский провайдер.

```typescript
if (searchService.connected) {
    // Пользовательский провайдер подключен
}
```

## Примеры использования

### Создание пользовательского провайдера

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

### Регистрация провайдера

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

### Модификация страницы поиска

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

### Интеграция с внешним поисковым сервисом

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