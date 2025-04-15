# Markdown Service

Markdown Service отвечает за обработку markdown-контента в Diplodoc. Этот сервис позволяет трансформировать контент, добавлять пользовательские блоки и валидировать документацию.

## Получение доступа к сервису

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MyExtension', (run) => {
            // Получение сервиса из контекста
            const {markdown} = run;
            
            // Получение hooks сервиса
            const markdownHooks = getMarkdownHooks(markdown);
        });
    }
}
```

## Доступные hooks

### Resolved
Hook для обработки markdown-контента после его разрешения. Вызывается после обработки всех включений и переменных.

```typescript
markdownHooks.Resolved.tapPromise('MyProcessor', async (content, path, from) => {
    // content: Разрешенный markdown-контент
    // path: Путь к текущему файлу
    // from: Путь к исходному файлу (для включений)
    
    // Трансформация контента
    const transformed = transformContent(content);
    
    return transformed;
});
```

## API сервиса

Markdown Service предоставляет методы для работы с markdown-контентом:

### Основные методы

```typescript
// Инициализация сервиса
await run.markdown.init();

// Загрузка и обработка markdown-файла
await run.markdown.load(path, from);

// Сохранение markdown-файла
await run.markdown.dump(path, content);

// Получение метаданных
await run.markdown.meta(path, from);

// Получение зависимостей
await run.markdown.deps(path, from);

// Получение ассетов
await run.markdown.assets(path, from);

// Получение заголовков
await run.markdown.headings(path, from);

// Анализ контента
await run.markdown.analyze(path, content, vars);

// Ремаппинг строк
run.markdown.remap(path, line);
```

### Работа с контентом

```typescript
// Получение frontmatter из контента
const frontmatter = run.markdown.frontmatter(content);

// Получение чистого контента без frontmatter
const cleanContent = run.markdown.content(content);

// Проверка наличия frontmatter
const hasFrontmatter = run.markdown.hasFrontmatter(content);
```

### Работа с включениями

```typescript
// Проверка наличия включений в контенте
const hasIncludes = run.markdown.hasIncludes(content);

// Получение списка включений
const includes = run.markdown.includes(content);

// Разрешение включений
const resolvedContent = await run.markdown.resolveIncludes(content, path);
```

### Работа с переменными

```typescript
// Проверка наличия переменных в контенте
const hasVars = run.markdown.hasVars(content);

// Получение списка переменных
const vars = run.markdown.vars(content);

// Разрешение переменных
const resolvedContent = await run.markdown.resolveVars(content, vars);
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

```typescript
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