# Markdown Service

The Markdown Service is responsible for processing markdown content in Diplodoc. This service allows transforming content, adding custom blocks, and validating documentation.

## Main features

- Processing markdown files with support for includes and variables.
- Managing [metadata and frontmatter](../../../project/meta.md).
- Support for templates with conditions and substitutions.
- Collecting and analyzing dependencies and assets.
- Working with headings and their anchors.

## Accessing the service

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MyExtension', (run) => {
            // Получение сервиса из контекста
            const {markdown} = run;
            
            // Получение хуков сервиса
            const markdownHooks = getMarkdownHooks(markdown);
        });
    }
}
```

## Available hooks

### Plugins
Hook for registering markdown file processing plugins. Called during service initialization.

```typescript
markdownHooks.Plugins.tapPromise('MyExtension', async (plugins) => {
    // plugins: Массив существующих плагинов
    
    // Добавляем новый плагин
    return [
        ...plugins,
        {
            name: 'my-plugin',
            transform: (content) => {
                // Трансформация контента
                return content;
            }
        }
    ];
});
```

### Collects
Hook for registering content analyzers. Called during service initialization.

```typescript
markdownHooks.Collects.tapPromise('MyExtension', async (collects) => {
    // collects: Массив существующих анализаторов
    
    // Добавляем новый анализатор
    return [
        ...collects,
        {
            name: 'my-collector',
            collect: (content, path) => {
                // Анализ контента
                return {
                    // Результаты анализа
                };
            }
        }
    ];
});
```

### Loaded
The hook is called after loading and initial processing of a markdown file.

```typescript
markdownHooks.Loaded.tapPromise('MyProcessor', async (raw, meta, path) => {
    // raw: Исходный контент файла
    // meta: Метаданные файла
    // path: Путь к файлу
    
    // Обработка загруженного контента
    return raw;
});
```

### Resolved
The hook is called after full content resolution (includes, variables).

```typescript
markdownHooks.Resolved.tapPromise('MyProcessor', async (content, path) => {
    // content: Разрешенный markdown-контент
    // path: Путь к файлу
    
    // Трансформация контента
    return content;
});
```

### Dump
The hook is called before saving a markdown file.

```typescript
markdownHooks.Dump.tapPromise('MyProcessor', async (vfile) => {
    // vfile: VFile с контентом и метаданными
    
    // Модификация перед сохранением
    return vfile;
});
```

## Service API

### Method init

Initializes the service. Computes the final set of analyzers and plugins for file processing.

```typescript
await markdownService.init();
```

### Method load

Loads and processes a markdown file.

**Parameters:**
- `path: RelativePath` — relative path to the file
- `from: NormalizedPath[]` — array of source file paths (for includes)

**Returns:**
- `Promise<string>` — promise with processed content

**Calls hooks:**
- `Loaded` — after file loading
- `Resolved` — after full content resolution

```typescript
const content = await markdownService.load('path/to/file.md');
```

### Method dump

Saves a markdown file.

**Parameters:**
- `file: NormalizedPath` — path to the file
- `markdown?: string` — content to save (if not specified, loaded from the file)

**Returns:**
- `Promise<VFile>` — promise with VFile

**Calls hooks:**
- `Dump` — before saving the file

```typescript
const vfile = await markdownService.dump('path/to/file.md', content);
```

### Method meta

Gets file metadata.

**Parameters:**
- `path: RelativePath` — path to the file

**Returns:**
- `Promise<Meta>` — promise with metadata

```typescript
const meta = await markdownService.meta('path/to/file.md');
```

### Method graph

Gets the file dependency graph.

**Parameters:**
- `path: RelativePath` — path to the file

**Returns:**
- `Promise<EntryGraph>` — promise with the dependency graph

```typescript
const graph = await markdownService.graph('path/to/file.md');
```

### Method assets

Gets the list of file assets.

**Parameters:**
- `path: RelativePath` — path to the file

**Returns:**
- `Promise<NormalizedPath[]>` — promise with an array of asset paths

```typescript
const assets = await markdownService.assets('path/to/file.md');
```

### Method headings

Gets information about file headings.

**Parameters:**
- `path: RelativePath` — path to the file

**Returns:**
- `Promise<HeadingInfo[]>` — promise with an array of heading information

```typescript
const headings = await markdownService.headings('path/to/file.md');
```

### Method titles

Gets a dictionary of headings and their anchors.

**Parameters:**
- `path: RelativePath` — path to the file

**Returns:**
- `Promise<Hash<string>>` — promise with a dictionary of headings

```typescript
const titles = await markdownService.titles('path/to/file.md');
```

### Method inspect

Analyzes content without saving state.

**Parameters:**
- `path: RelativePath` — path to the file
- `raw: string` — raw content
- `vars: Hash` — variables for substitution

**Returns:**
- `Promise<{content: string, deps: IncludeInfo[], assets: NormalizedPath[]}>` — promise with analysis results

```typescript
const {content, deps, assets} = await markdownService.inspect('path/to/file.md', raw, vars);
```

### Method remap

Transforms a line number taking into account the sourcemap.

**Parameters:**
- `path: RelativePath` — path to the file
- `line: number` — line number

**Returns:**
- `number` — transformed line number

```typescript
const mappedLine = markdownService.remap('path/to/file.md', 10);
```

## Usage examples

### Adding custom blocks

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('CustomBlocks', (run) => {
            const markdownHooks = getMarkdownHooks(run.markdown);
            
            markdownHooks.Resolved.tapPromise('CustomBlocks', async (content) => {
                // Добавляем пользовательский блок
                return content.replace(
                    /:::custom-block([\s\S]*?):::/g,
                    (_, body) => `<div class="custom-block">${body}</div>`
                );
            });
        });
    }
}
```

### Content validation

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('ContentValidator', (run) => {
            const markdownHooks = getMarkdownHooks(run.markdown);
            
            markdownHooks.Resolved.tapPromise('ContentValidator', async (content, path) => {
                // Проверяем наличие заголовка
                if (!content.match(/^#\s/)) {
                    run.logger.warn(`Missing title in ${path}`);
                }
                
                // Проверяем длину разделов
                validateSectionLengths(content);
                
                // Проверяем корректность ссылок
                await validateLinks(content, path);
                
                return content;
            });
        });
    }
}
```

### Processing includes

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('IncludeProcessor', (run) => {
            const markdownHooks = getMarkdownHooks(run.markdown);
            
            markdownHooks.Resolved.tapPromise('IncludeProcessor', async (content, path, from) => {
                // Если это включенный контент
                if (from) {
                    // Добавляем информацию об источнике
                    return `<!-- Included from: ${from} -->\n${content}`;
                }
                
                return content;
            });
        });
    }
}
```

### Integration with external services

```typescript translate=no
export class Extension {
    constructor(private apiKey: string) {}
    
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('ExternalIntegration', (run) => {
            const markdownHooks = getMarkdownHooks(run.markdown);
            
            markdownHooks.Resolved.tapPromise('ExternalIntegration', async (content) => {
                // Обрабатываем специальные теги
                return content.replace(
                    /{external-data\sid="([^"]+)"}/g,
                    async (_, id) => {
                        const data = await this.fetchExternalData(id);
                        return this.formatExternalData(data);
                    }
                );
            });
        });
    }
    
    private async fetchExternalData(id: string) {
        // Получение данных из внешнего API
    }
    
    private formatExternalData(data: any) {
        // Форматирование данных в markdown
    }
}
```