# TOC Service

TOC Service управляет обработкой оглавления (Table of Contents) в Diplodoc. 
Этот сервис позволяет модифицировать структуру документации на различных этапах сборки.

## Основные возможности

- Загрузка и обработка файлов `toc.yaml`
- Управление структурой документации
- Поддержка включателей (includers)
- Поддержка условной логики в TOC

## Получение доступа к сервису

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

## Доступные хуки

### Item

Hook для обработки отдельных элементов TOC. Вызывается для каждого элемента в процессе обработки.

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

Hook для регистрации пользовательских включателей. Позволяет добавлять динамически генерируемые разделы в TOC.

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

Hook для работы с полностью разрешенным TOC. На этом этапе TOC уже содержит все включенные элементы и является read-only.

```typescript
tocHooks.Resolved.tapPromise('MyProcessor', async (toc, tocPath) => {
    // Анализируем структуру
    validateStructure(toc);
    
    // Собираем статистику
    collectMetrics(toc);
});
```

### Included

Hook для обработки TOC после его включения через директиву include.

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

Hook для финальной модификации TOC перед сохранением.

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

Hook для обработки TOC после его загрузки из файла.

```typescript
tocHooks.Loaded.tapPromise('MyProcessor', async (toc, path) => {
    // Модифицируем загруженный TOC
    return {
        ...toc,
        meta: {
            ...toc.meta,
            loadedAt: new Date().toISOString()
        }
    };
});
```

## API сервиса

### Метод init

Инициализирует сервис, загружая TOC из указанных путей.

**Параметры:**
- `paths: NormalizedPath[]` - массив путей к файлам `toc.yaml` для загрузки

**Вызывает хуки:**
- `Loaded` - после загрузки каждого TOC файла

```typescript
// Инициализация сервиса с указанием путей
await tocService.init(['path/to/toc.yaml']);
```

### Метод for

Возвращает TOC для указанного пути.

**Параметры:**
- `path: RelativePath` - относительный путь к файлу, для которого нужно получить TOC

**Возвращает:**
- `Toc` - объект TOC, содержащий структуру документации

```typescript
// Получение TOC для конкретного пути
const toc = tocService.for('path/to/file.md');
```

### Метод dump

Сохраняет TOC в файл.

**Параметры:**
- `file: NormalizedPath` - путь к файлу для сохранения
- `toc?: Toc` - объект TOC для сохранения (если не указан, используется TOC из кэша)

**Возвращает:**
- `Promise<VFile<Toc>>` - промис с виртуальным файлом, содержащим сохраненный TOC

**Вызывает хуки:**
- `Dump` - перед сохранением TOC в файл

```typescript
// Сохранение TOC в файл
await tocService.dump('path/to/toc.yaml', toc);
```

### Метод load

Загружает TOC из файла.

**Параметры:**
- `path: NormalizedPath` - путь к файлу `toc.yaml`

**Возвращает:**
- `Promise<Toc | undefined>` - промис с загруженным TOC или undefined, если файл не найден

**Вызывает хуки:**
- `Loaded` - после успешной загрузки TOC
- `Item` - для каждого элемента в загруженном TOC

```typescript
// Загрузка TOC из файла
const toc = await tocService.load('path/to/toc.yaml');
```

### Метод include

Включает TOC через директиву include.

**Параметры:**
- `path: RelativePath` - путь к включаемому файлу `toc.yaml`
- `include: IncludeInfo` - информация о включении:
  - `from?: string` - путь к исходному файлу
  - `mode?: 'merge' | 'replace'` - режим включения
  - `base?: string` - базовый путь для относительных ссылок
  - `content?: string` - содержимое файла (если уже загружено)

**Возвращает:**
- `Promise<Toc | undefined>` - промис с включенным TOC или undefined, если файл не найден

**Вызывает хуки:**
- `Included` - после включения TOC
- `Item` - для каждого элемента во включенном TOC

```typescript
// Включение TOC
const includedToc = await tocService.include('path/to/toc.yaml', {
    from: 'source/path',
    mode: 'merge',
    base: 'base/path'
});
```

### Метод setToc

Устанавливает TOC для указанного пути.

**Параметры:**
- `toc: Toc` - объект TOC для установки:
  - `path: NormalizedPath` - путь к файлу
  - `items?: TocItem[]` - элементы TOC
  - `href?: string` - ссылка на страницу
  - `meta?: Record<string, unknown>` - метаданные

**Вызывает хуки:**
- `Item` - для каждого элемента в устанавливаемом TOC

```typescript
// Установка TOC
tocService.setToc({
    path: 'path/to/toc.yaml',
    items: [...]
});
```

### Свойство entries

Возвращает список всех entry во всех TOC.

**Возвращает:**
- `Set<NormalizedPath>` - множество путей к файлам, включенным в TOC

```typescript
// Получение всех entry
const entries = tocService.entries;
```

### Свойство tocs

Возвращает список всех загруженных TOC.

**Возвращает:**
- `Toc[]` - массив загруженных объектов TOC

```typescript
// Получение всех TOC
const tocs = tocService.tocs;
```

### Свойство copymap

Возвращает карту копирования файлов.

**Возвращает:**
- `Record<NormalizedPath, NormalizedPath>` - объект, где ключ - исходный путь, значение - целевой путь

```typescript
// Получение карты копирования
const copymap = tocService.copymap;
```

## Примеры использования

### Добавление метаданных к разделам

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

### Динамическая генерация разделов

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

### Валидация структуры

```typescript
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