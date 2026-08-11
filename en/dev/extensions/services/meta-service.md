# Meta Service

Meta Service is responsible for managing metadata in Diplodoc. This service allows adding, modifying, and retrieving metadata for documentation pages.

## Main features

- Managing page metadata.
- Adding scripts and styles to documents.
- Configuring [CSP rules](../../../guides/csp.md).
- Managing custom metadata.

## Accessing the service

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

## Available hooks

### Dump

Hook for final metadata modification before saving.

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

## Service API

### get method

Returns the current metadata for the specified path.

**Parameters:**
- `path: RelativePath` — relative path to the file.

**Returns:**
- `DeepFrozen<Meta>` — frozen object with metadata.

```typescript
// Получение метаданных
const meta = metaService.get('path/to/file.md');
```

### set method

Sets metadata for the specified path.

**Parameters:**
- `path: RelativePath` — relative path to the file.
- `meta: Meta` — object with metadata.

```typescript
// Установка метаданных
metaService.set('path/to/file.md', {
    title: 'Page Title',
    description: 'Page Description'
});
```

### Method dump

Returns normalized metadata for saving.

**Parameters:**
- `path: RelativePath` — relative path to the file.

**Returns:**
- `Promise<Meta>` — promise with normalized metadata.

**Calls hooks:**
- `Dump` — before returning metadata.

```typescript
// Получение нормализованных метаданных
const normalizedMeta = await metaService.dump('path/to/file.md');
```

### Method add

Adds metadata to existing metadata.

**Parameters:**
- `path: RelativePath` — relative path to the file.
- `record: Hash` — object with metadata to add.

**Returns:**
- `Meta` — updated metadata object.

```typescript
// Добавление метаданных
metaService.add('path/to/file.md', {
    title: 'Page Title',
    description: 'Page Description'
});
```

### addMetadata method

Adds custom metadata.

**Parameters:**
- `path: RelativePath` — relative path to the file.
- `metadata: Hash | undefined` — object with custom metadata or an array of objects `{name: string, content: string}`.

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

### addSystemVars method

Adds system variables.

**Parameters:**
- `path: RelativePath` — relative path to the file.
- `vars: Hash | undefined` — object with system variables.

```typescript
// Добавление системных переменных
metaService.addSystemVars('path/to/file.md', {
    version: '1.0.0',
    buildTime: new Date().toISOString()
});
```

## Usage examples

### Adding metadata for a page

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

### Adding CSP rules

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