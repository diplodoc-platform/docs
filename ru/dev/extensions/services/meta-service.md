# Meta Service

Meta Service отвечает за управление метаданными в Diplodoc. Этот сервис позволяет добавлять, модифицировать и получать метаданные для страниц документации.

## Основные возможности

- Управление метаданными страниц
- Добавление скриптов и стилей в документы
- Настройка CSP-правил
- Управление пользовательскими метаданными

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

### Метод get

Возвращает текущие метаданные для указанного пути.

**Параметры:**
- `path: RelativePath` - относительный путь к файлу

**Возвращает:**
- `DeepFrozen<Meta>` - замороженный объект с метаданными

```typescript
// Получение метаданных
const meta = metaService.get('path/to/file.md');
```

### Метод set

Устанавливает метаданные для указанного пути.

**Параметры:**
- `path: RelativePath` - относительный путь к файлу
- `meta: Meta` - объект с метаданными

```typescript
// Установка метаданных
metaService.set('path/to/file.md', {
    title: 'Page Title',
    description: 'Page Description'
});
```

### Метод dump

Возвращает нормализованные метаданные для сохранения.

**Параметры:**
- `path: RelativePath` - относительный путь к файлу

**Возвращает:**
- `Promise<Meta>` - промис с нормализованными метаданными

**Вызывает хуки:**
- `Dump` - перед возвратом метаданных

```typescript
// Получение нормализованных метаданных
const normalizedMeta = await metaService.dump('path/to/file.md');
```

### Метод add

Добавляет метаданные к существующим.

**Параметры:**
- `path: RelativePath` - относительный путь к файлу
- `record: Hash` - объект с метаданными для добавления

**Возвращает:**
- `Meta` - обновленный объект метаданных

```typescript
// Добавление метаданных
metaService.add('path/to/file.md', {
    title: 'Page Title',
    description: 'Page Description'
});
```

### Метод addMetadata

Добавляет пользовательские метаданные.

**Параметры:**
- `path: RelativePath` - относительный путь к файлу
- `metadata: Hash | undefined` - объект с пользовательскими метаданными или массив объектов `{name: string, content: string}`

```typescript
// Добавление пользовательских метаданных
metaService.addMetadata('path/to/file.md', {
    author: 'John Doe',
    category: 'API'
});

// Или в виде массива
metaService.addMetadata('path/to/file.md', [
    {name: 'author', content: 'John Doe'},
    {name: 'category', content: 'API'}
]);
```

### Метод addSystemVars

Добавляет системные переменные.

**Параметры:**
- `path: RelativePath` - относительный путь к файлу
- `vars: Hash | undefined` - объект с системными переменными

```typescript
// Добавление системных переменных
metaService.addSystemVars('path/to/file.md', {
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
```