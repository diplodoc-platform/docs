# TOC Service

TOC Service manages the processing of the [table of contents](../../../project/toc.md) (Table of Contents, ToC) in Diplodoc. This service allows modifying the documentation structure at various build stages.

## Main features

- Loading and processing of `toc.yaml` files.
- Managing the documentation structure.
- Support for [includers](../../../guides/includers.md).
- Support for conditional logic in ToC.

## Accessing the service

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MyExtension', (run) => {
            // Получение сервиса из контекста
            const {toc} = run;
            
            // Получение hooks сервиса
            const tocHooks = getTocHooks(run.toc);
        });
    }
}
```

## Available hooks

### Item

Processing individual ToC items. Called for each item during processing.

```typescript
tocHooks.Item.tapPromise('MyProcessor', async (item, tocPath) => {
    // Скрываем определенные разделы
    if (item.name === 'Internal') {
        item.hidden = true;
    }
    
    // Добавляем метаданные
    item.meta = {
        ...item.meta,
        category: 'docs'
    };
    
    return item;
});
```

### Includer

Hook for registering custom includers. Allows adding dynamically generated sections to the ToC.

```typescript
tocHooks.Includer.for('my-includer').tapPromise('MyProcessor', async (toc, options, tocPath) => {
    // Генерируем дополнительные элементы
    const generatedItems = await generateItems();
    
    return {
        ...toc,
        items: [...(toc.items || []), ...generatedItems]
    };
});
```

### Resolved

Hook for working with a fully resolved ToC. At this stage, the ToC already contains all included items and is read-only.

```typescript
tocHooks.Resolved.tapPromise('MyProcessor', async (toc, tocPath) => {
    // Анализируем структуру
    validateStructure(toc);
    
    // Собираем статистику
    collectMetrics(toc);
});
```

### Included

Hook for processing the ToC after it has been included via ##[include](../../../project/toc-includes.md)##.

```typescript
tocHooks.Included.tapPromise('MyProcessor', async (toc, tocPath, includeInfo) => {
    // Модифицируем включенный TOC
    return {
        ...toc,
        meta: {
            ...toc.meta,
            includedFrom: includeInfo.source
        }
    };
});
```

### Dump

Hook for final modification of the ToC before saving.

```typescript
tocHooks.Dump.tapPromise('MyProcessor', async (toc, path) => {
    // Добавляем общие элементы навигации
    return {
        ...toc,
        items: [...(toc.items || []), {
            name: 'Support',
            href: '/support'
        }]
    };
});
```

### Loaded

Hook for processing the ToC after it has been loaded from a file.

```typescript
tocHooks.Loaded.tapPromise('MyProcessor', async (toc, path) => {
    // Модифицируем загруженный ToC
    return {
        ...toc,
        meta: {
            ...toc.meta,
            loadedAt: new Date().toISOString()
        }
    };
});
```

## Service API

### Method init

Initializes the service by loading the ToC from the specified paths.

**Parameters:**
- `paths: NormalizedPath[]` — an array of paths to `toc.yaml` files to load.

**Calls hooks:**
- `Loaded` — after loading each ToC file.

```typescript
// Инициализация сервиса с указанием путей
await tocService.init(['path/to/toc.yaml']);
```

### Method for

Returns the ToC for the specified path.

**Parameters:**
- `path: RelativePath` — the relative path to the file for which the ToC should be retrieved.

**Returns:**
- `Toc` — a ToC object containing the documentation structure.

```typescript
// Получение ToC для конкретного пути
const toc = tocService.for('path/to/file.md');
```

### Method dump

Saves the ToC to a file.

**Parameters:**
- `file: NormalizedPath` — the path to the file for saving.
- `toc?: Toc` — the ToC object to save (if not specified, the ToC from the cache is used).

**Returns:**
- `Promise<VFile<Toc>>` — a promise with a virtual file containing the saved ToC.

**Calls hooks:**
- `Dump` — before saving the ToC to a file.

```typescript
// Сохранение ToC в файл
await tocService.dump('path/to/toc.yaml', toc);
```

### Method load

Loads the ToC from a file.

**Parameters:**
- `path: NormalizedPath` — the path to the `toc.yaml` file.

**Returns:**
- `Promise<Toc | undefined>` — a promise with the loaded ToC or undefined if the file is not found.

**Calls hooks:**
- `Loaded` — after successful loading of the ToC.
- `Item` — for each item in the loaded ToC.

```typescript
// Загрузка ToC из файла
const toc = await tocService.load('path/to/toc.yaml');
```

### Method include

Includes the ToC via the ##include## directive.

**Parameters:**
- `path: RelativePath` — the path to the included `toc.yaml` file.
- `include: IncludeInfo` — inclusion information:
  - `from?: string` — the path to the source file.
  - `mode?: 'merge' | 'replace'` — the inclusion mode.
  - `base?: string` — the base path for relative links.
  - `content?: string` — the file content (if already loaded).

**Returns:**
- `Promise<Toc | undefined>` — a promise with the included ToC or ##undefined## if the file is not found.

**Calls hooks:**
- `Included` — after including the ToC.
- `Item` — for each item in the included ToC.

```typescript
// Включение ToC
const includedToc = await tocService.include('path/to/toc.yaml', {
    from: 'source/path',
    mode: 'merge',
    base: 'base/path'
});
```

### Method setToc

Sets the ToC for the specified path.

**Parameters:**
- `toc: Toc` — the ToC object to set:
  - `path: NormalizedPath` — path to the file.
  - `items?: TocItem[]` — ToC items.
  - `href?: string` — link to the page.
  - `meta?: Record<string, unknown>` — metadata.

**Calls hooks:**
- `Item` — for each item in the ToC being set.

```typescript
// Установка ToC
tocService.setToc({
    path: 'path/to/toc.yaml',
    items: [...]
});
```

### entries property

Returns the list of all entries in all ToCs.

**Returns:**
- `Set<NormalizedPath>` — a set of paths to files included in the ToC.

```typescript
// Получение всех entry
const entries = tocService.entries;
```

### tocs property

Returns the list of all loaded ToCs.

**Returns:**
- `Toc[]` — an array of loaded ToC objects.

```typescript
// Получение всех ToC
const tocs = tocService.tocs;
```

### copymap property

Returns the file copy map.

**Returns:**
- `Record<NormalizedPath, NormalizedPath>` — an object where the key is the source path and the value is the target path.

```typescript
// Получение карты копирования
const copymap = tocService.copymap;
```

## Usage examples

### Adding metadata to sections

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MetadataProcessor', (run) => {
            const tocHooks = getTocHooks(run.toc);
            
            tocHooks.Item.tapPromise('MetadataProcessor', async (item) => {
                return {
                    ...item,
                    meta: {
                        ...item.meta,
                        lastUpdated: new Date().toISOString(),
                        category: getCategoryFromPath(item.href)
                    }
                };
            });
        });
    }
}
```

### Dynamic generation of sections

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('DynamicSections', (run) => {
            const tocHooks = getTocHooks(run.toc);
            
            tocHooks.Includer.for('generated-docs').tapPromise(
                'DynamicSections',
                async (toc, options) => {
                    const items = await fetchDocumentationItems();
                    
                    return {
                        ...toc,
                        items: [...(toc.items || []), ...items]
                    };
                }
            );
        });
    }
}
```

### Structure validation

```typescript translate=no
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('StructureValidator', (run) => {
            const tocHooks = getTocHooks(run.toc);
            
            tocHooks.Resolved.tapPromise('StructureValidator', async (toc) => {
                validateMaxDepth(toc, 3);
                validateUniqueUrls(toc);
                validateRequiredSections(toc);
            });
        });
    }
} 
```