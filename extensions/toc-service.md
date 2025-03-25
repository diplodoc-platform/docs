# TOC Service

TOC Service управляет обработкой оглавления (Table of Contents) в Diplodoc. Этот сервис позволяет модифицировать структуру документации на различных этапах сборки.

## Получение доступа к сервису

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MyExtension', (run) => {
            // Получение сервиса из контекста
            const {toc} = run;
            
            // Получение hooks сервиса
            const tocHooks = getTocHooks(toc);
        });
    }
}
```

## Доступные hooks

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

## API сервиса

TOC Service предоставляет методы для работы со структурой документации:

### Основные методы

```typescript
// Получение списка всех entry в TOC
const entries = run.toc.entries;

// Загрузка TOC из файла
await run.toc.load(path);

// Включение TOC через директиву include
await run.toc.include(path, includeInfo);

// Сохранение TOC
await run.toc.dump(path);

// Установка TOC для пути
run.toc.set(path, toc);

// Получение нормализованного пути
run.toc.for(path);

// Получение директории TOC
run.toc.dir(path);
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