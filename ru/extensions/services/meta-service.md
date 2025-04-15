# Meta Service

Meta Service отвечает за управление метаданными в Diplodoc. Этот сервис позволяет добавлять, модифицировать и получать метаданные для страниц документации, включая скрипты, стили, CSP и пользовательские метаданные.

## Получение доступа к сервису

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MyExtension', (run) => {
            // Получение сервиса из контекста
            const {meta} = run;
            
            // Получение хуков сервиса
            const metaHooks = getMetaHooks(meta);
        });
    }
}
```

## Доступные хуки

### Dump
Хук для финальной модификации метаданных перед сохранением.

```typescript
metaHooks.Dump.tapPromise('MyProcessor', async (meta, path) => {
    // Модифицируем метаданные перед сохранением
    return {
        ...meta,
        metadata: [
            ...(meta.metadata || []),
            {name: 'version', content: '1.0.0'}
        ]
    };
});
```

## API сервиса

Meta Service предоставляет методы для работы с метаданными:

### Основные методы

```typescript
// Получение текущих метаданных для пути
const meta = run.meta.get(path);

// Получение нормализованных метаданных для сохранения
const normalizedMeta = await run.meta.dump(path);

// Добавление метаданных
run.meta.add(path, {
    title: 'Page Title',
    description: 'Page Description'
});

// Добавление ресурсов (скрипты, стили, CSP)
run.meta.addResources(path, {
    script: ['script.js'],
    style: ['style.css'],
    csp: [{
        'script-src': ['self', 'https://api.example.com']
    }]
});

// Добавление пользовательских метаданных
run.meta.addMetadata(path, {
    author: 'John Doe',
    category: 'API'
});

// Добавление системных переменных
run.meta.addSystemVars(path, {
    version: '1.0.0',
    buildTime: new Date().toISOString()
});
```

## Примеры использования

### Добавление метаданных для страницы

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MetaProcessor', (run) => {
            const markdownHooks = getMarkdownHooks(run.markdown);
            
            markdownHooks.Resolved.tapPromise('MetaProcessor', async (content, path) => {
                // Добавляем метаданные для страницы
                run.meta.add(path, {
                    title: extractTitle(content),
                    description: extractDescription(content)
                });
                
                // Добавляем необходимые ресурсы
                run.meta.addResources(path, {
                    script: ['highlight.js'],
                    style: ['highlight.css']
                });
                
                return content;
            });
        });
    }
}
```

### Добавление CSP-правил

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('CSPProcessor', (run) => {
            const metaHooks = getMetaHooks(run.meta);
            
            metaHooks.Dump.tapPromise('CSPProcessor', async (meta, path) => {
                return {
                    ...meta,
                    csp: [
                        ...(meta.csp || []),
                        {
                            'default-src': ['self'],
                            'img-src': ['self', 'data:', 'https:'],
                            'script-src': ['self', 'https://cdn.example.com']
                        }
                    ]
                };
            });
        });
    }
}

### Интеграция с внешними системами

```typescript
export class Extension {
    constructor(private apiClient: ApiClient) {}
    
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('ExternalMetadata', (run) => {
            const markdownHooks = getMarkdownHooks(run.markdown);
            
            markdownHooks.Resolved.tapPromise('ExternalMetadata', async (content, path) => {
                // Получаем метаданные из внешней системы
                const externalMeta = await this.apiClient.getMetadata(path);
                
                // Добавляем пользовательские метаданные
                run.meta.addMetadata(path, {
                    lastModified: externalMeta.modifiedAt,
                    author: externalMeta.author,
                    reviewers: externalMeta.reviewers.join(', ')
                });
                
                return content;
            });
        });
    }
} 