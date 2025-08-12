# Markdown Service

Markdown Service отвечает за обработку markdown-контента в Diplodoc. Этот сервис позволяет трансформировать контент, добавлять пользовательские блоки и валидировать документацию.

## Основные возможности

- Обработка markdown-файлов с поддержкой включений и переменных
- Управление метаданными и frontmatter
- Поддержка шаблонов с условиями и подстановками
- Сбор и анализ зависимостей и ассетов
- Работа с заголовками и их якорями

## Получение доступа к сервису

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

## Доступные хуки

### Plugins
Хук для регистрации плагинов обработки markdown-файлов. Вызывается при инициализации сервиса.

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
Хук для регистрации анализаторов контента. Вызывается при инициализации сервиса.

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
Хук вызывается после загрузки и начальной обработки markdown-файла.

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
Хук вызывается после полного разрешения контента (включения, переменные).

```typescript
markdownHooks.Resolved.tapPromise('MyProcessor', async (content, path) => {
    // content: Разрешенный markdown-контент
    // path: Путь к файлу
    
    // Трансформация контента
    return content;
});
```

### Dump
Хук вызывается перед сохранением markdown-файла.

```typescript
markdownHooks.Dump.tapPromise('MyProcessor', async (vfile) => {
    // vfile: VFile с контентом и метаданными
    
    // Модификация перед сохранением
    return vfile;
});
```

## API сервиса

### Метод init

Инициализирует сервис. Вычисляет финальный набор анализаторов и плагинов для обработки файлов.

```typescript
await markdownService.init();
```

### Метод load

Загружает и обрабатывает markdown-файл.

**Параметры:**
- `path: RelativePath` - относительный путь к файлу
- `from: NormalizedPath[]` - массив путей исходных файлов (для включений)

**Возвращает:**
- `Promise<string>` - промис с обработанным контентом

**Вызывает хуки:**
- `Loaded` - после загрузки файла
- `Resolved` - после полного разрешения контента

```typescript
const content = await markdownService.load('path/to/file.md');
```

### Метод dump

Сохраняет markdown-файл.

**Параметры:**
- `file: NormalizedPath` - путь к файлу
- `markdown?: string` - контент для сохранения (если не указан, загружается из файла)

**Возвращает:**
- `Promise<VFile>` - промис с VFile

**Вызывает хуки:**
- `Dump` - перед сохранением файла

```typescript
const vfile = await markdownService.dump('path/to/file.md', content);
```

### Метод meta

Получает метаданные файла.

**Параметры:**
- `path: RelativePath` - путь к файлу

**Возвращает:**
- `Promise<Meta>` - промис с метаданными

```typescript
const meta = await markdownService.meta('path/to/file.md');
```

### Метод graph

Получает граф зависимостей файла.

**Параметры:**
- `path: RelativePath` - путь к файлу

**Возвращает:**
- `Promise<EntryGraph>` - промис с графом зависимостей

```typescript
const graph = await markdownService.graph('path/to/file.md');
```

### Метод assets

Получает список ассетов файла.

**Параметры:**
- `path: RelativePath` - путь к файлу

**Возвращает:**
- `Promise<NormalizedPath[]>` - промис с массивом путей к ассетам

```typescript
const assets = await markdownService.assets('path/to/file.md');
```

### Метод headings

Получает информацию о заголовках файла.

**Параметры:**
- `path: RelativePath` - путь к файлу

**Возвращает:**
- `Promise<HeadingInfo[]>` - промис с массивом информации о заголовках

```typescript
const headings = await markdownService.headings('path/to/file.md');
```

### Метод titles

Получает словарь заголовков и их якорей.

**Параметры:**
- `path: RelativePath` - путь к файлу

**Возвращает:**
- `Promise<Hash<string>>` - промис со словарем заголовков

```typescript
const titles = await markdownService.titles('path/to/file.md');
```

### Метод inspect

Анализирует контент без сохранения состояния.

**Параметры:**
- `path: RelativePath` - путь к файлу
- `raw: string` - исходный контент
- `vars: Hash` - переменные для подстановки

**Возвращает:**
- `Promise<{content: string, deps: IncludeInfo[], assets: NormalizedPath[]}>` - промис с результатами анализа

```typescript
const {content, deps, assets} = await markdownService.inspect('path/to/file.md', raw, vars);
```

### Метод remap

Преобразует номер строки с учетом sourcemap.

**Параметры:**
- `path: RelativePath` - путь к файлу
- `line: number` - номер строки

**Возвращает:**
- `number` - преобразованный номер строки

```typescript
const mappedLine = markdownService.remap('path/to/file.md', 10);
```

## Примеры использования

### Добавление пользовательских блоков

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

### Валидация контента

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

### Обработка включений

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

### Интеграция с внешними сервисами

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