# Leading Service

Leading Service is responsible for processing [leading pages](../../../project/leading-page.md) in Diplodoc. These pages describe documentation sections and simplify navigation through them.

## Main features

- Processing YAML files with section descriptions.
- Managing section metadata.
- Support for templates with conditions and substitutions.
- Collecting and analyzing dependencies and assets.

## Accessing the service

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MyExtension', (run) => {
            // Получение сервиса из контекста
            const {leading} = run;
            
            // Получение хуков сервиса
            const leadingHooks = getLeadingHooks(leading);
        });
    }
}
```

## Available hooks

### Plugins
Hook for registering leading page processing plugins. Called during service initialization.

```typescript
leadingHooks.Plugins.tapPromise('MyExtension', async (plugins) => {
    // plugins: Массив существующих плагинов
    
    // Добавляем новый плагин
    return [
        ...plugins,
        {
            name: 'my-plugin',
            transform: (leading) => {
                // Трансформация разводящей страницы
                return leading;
            }
        }
    ];
});
```

### Loaded
The hook is called after loading and initial processing of the leading page.

```typescript
leadingHooks.Loaded.tapPromise('MyProcessor', async (leading, meta, path) => {
    // leading: Загруженная разводящая страница
    // meta: Метаданные страницы
    // path: Путь к файлу
    
    // Обработка загруженной страницы
    return leading;
});
```

### Resolved
The hook is called after the leading page is fully resolved.

```typescript
leadingHooks.Resolved.tapPromise('MyProcessor', async (leading, meta, path) => {
    // leading: Разрешенная разводящая страница
    // meta: Метаданные страницы
    // path: Путь к файлу
    
    // Трансформация страницы
    return leading;
});
```

### Dump
The hook is called before saving the leading page.

```typescript
leadingHooks.Dump.tapPromise('MyProcessor', async (vfile) => {
    // vfile: VFile с разводящей страницей и метаданными
    
    // Модификация перед сохранением
    return vfile;
});
```

## Service API

### Method init

Initializes the service by loading plugins.

```typescript
await leadingService.init();
```

### Method load

Loads and processes the leading page.

**Parameters:**
- `path: RelativePath` — relative path to the file.

**Returns:**
- `Promise<LeadingPage>` — promise with the processed leading page.

**Calls hooks:**
- `Loaded` — after loading the file.
- `Resolved` — after the page is fully resolved.

```typescript
const leading = await leadingService.load('path/to/leading.yaml');
```

### Method dump

Saves the leading page.

**Parameters:**
- `path: RelativePath` — path to the file.
- `leading?: LeadingPage` — page to save (if not specified, loaded from the file).

**Returns:**
- `Promise<VFile<LeadingPage>>` — promise with VFile.

**Calls hooks:**
- `Dump` — before saving the file

```typescript
const vfile = await leadingService.dump('path/to/leading.yaml', leading);
```

### Method walkLinks

Walks through all links in the leading page.

**Parameters:**
- `leading: LeadingPage | undefined` — leading page.
- `walker: (link: string) => string | void` — link processing function.

**Returns:**
- `LeadingPage | undefined` — modified leading page or ##undefined##.

```typescript
const modifiedLeading = leadingService.walkLinks(leading, (link) => {
    // Модификация ссылки
    return modifiedLink;
});
```

### Method deps

Gets the dependencies of the leading page.

**Parameters:**
- `path: RelativePath` — path to the file.

**Returns:**
- `Promise<never[]>` — promise with an array of dependencies.

```typescript
const deps = await leadingService.deps('path/to/leading.yaml');
```

### Method assets

Gets the list of assets of the leading page.

**Parameters:**
- `path: RelativePath` — path to the file.

**Returns:**
- `Promise<NormalizedPath[]>` — promise with an array of asset paths.

```typescript
const assets = await leadingService.assets('path/to/leading.yaml');
```

## Usage examples

### Adding section information

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('SectionEnricher', (run) => {
            const leadingHooks = getLeadingHooks(run.leading);
            
            leadingHooks.Resolved.tapPromise('SectionEnricher', async (leading, meta, path) => {
                // Получаем дополнительную информацию о разделе
                const sectionInfo = await fetchSectionInfo(path);
                
                return {
                    ...leading,
                    title: sectionInfo.title,
                    description: sectionInfo.description,
                    meta: {
                        ...leading.meta,
                        ...sectionInfo.meta
                    }
                };
            });
        });
    }
}
```

### Validating section metadata

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MetadataValidator', (run) => {
            const leadingHooks = getLeadingHooks(run.leading);
            
            leadingHooks.Resolved.tapPromise('MetadataValidator', async (leading, meta, path) => {
                // Проверяем обязательные поля
                if (!leading.title) {
                    run.logger.warn(`Missing title in ${path}`);
                }
                
                // Проверяем корректность значений
                validateSectionValues(leading);
                
                return leading;
            });
        });
    }
}
```

### Integration with external systems

```typescript
export class Extension {
    constructor(private apiKey: string) {}
    
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('ExternalIntegration', (run) => {
            const leadingHooks = getLeadingHooks(run.leading);
            
            leadingHooks.Resolved.tapPromise('ExternalIntegration', async (leading, meta, path) => {
                // Получаем данные из внешней системы
                const externalData = await this.fetchExternalData(
                    this.apiKey,
                    leading.title
                );
                
                return {
                    ...leading,
                    meta: {
                        ...leading.meta,
                        externalData
                    }
                };
            });
        });
    }
    
    private async fetchExternalData(apiKey: string, sectionTitle: string) {
        // Логика получения данных из внешней системы
    }
}
``` 