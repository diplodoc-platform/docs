# Leading Service

Leading Service отвечает за обработку страниц оглавления (leading pages) в Diplodoc. Эти специальные страницы описывают разделы документации и содержат метаданные для них.

## Основные возможности

- Обработка YAML-файлов с описанием разделов
- Управление метаданными разделов
- Поддержка шаблонов с условиями и подстановками
- Сбор и анализ зависимостей и ассетов

## Получение доступа к сервису

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

## Доступные хуки

### Plugins
Хук для регистрации плагинов обработки leading-страниц. Вызывается при инициализации сервиса.

```typescript
leadingHooks.Plugins.tapPromise('MyExtension', async (plugins) => {
    // plugins: Массив существующих плагинов
    
    // Добавляем новый плагин
    return [
        ...plugins,
        {
            name: 'my-plugin',
            transform: (leading) => {
                // Трансформация leading-страницы
                return leading;
            }
        }
    ];
});
```

### Loaded
Хук вызывается после загрузки и начальной обработки leading-страницы.

```typescript
leadingHooks.Loaded.tapPromise('MyProcessor', async (leading, meta, path) => {
    // leading: Загруженная leading-страница
    // meta: Метаданные страницы
    // path: Путь к файлу
    
    // Обработка загруженной страницы
    return leading;
});
```

### Resolved
Хук вызывается после полного разрешения leading-страницы.

```typescript
leadingHooks.Resolved.tapPromise('MyProcessor', async (leading, meta, path) => {
    // leading: Разрешенная leading-страница
    // meta: Метаданные страницы
    // path: Путь к файлу
    
    // Трансформация страницы
    return leading;
});
```

### Dump
Хук вызывается перед сохранением leading-страницы.

```typescript
leadingHooks.Dump.tapPromise('MyProcessor', async (vfile) => {
    // vfile: VFile с leading-страницей и метаданными
    
    // Модификация перед сохранением
    return vfile;
});
```

## API сервиса

### Метод init

Инициализирует сервис, загружая плагины.

```typescript
await leadingService.init();
```

### Метод load

Загружает и обрабатывает leading-страницу.

**Параметры:**
- `path: RelativePath` - относительный путь к файлу

**Возвращает:**
- `Promise<LeadingPage>` - промис с обработанной leading-страницей

**Вызывает хуки:**
- `Loaded` - после загрузки файла
- `Resolved` - после полного разрешения страницы

```typescript
const leading = await leadingService.load('path/to/leading.yaml');
```

### Метод dump

Сохраняет leading-страницу.

**Параметры:**
- `path: RelativePath` - путь к файлу
- `leading?: LeadingPage` - страница для сохранения (если не указана, загружается из файла)

**Возвращает:**
- `Promise<VFile<LeadingPage>>` - промис с VFile

**Вызывает хуки:**
- `Dump` - перед сохранением файла

```typescript
const vfile = await leadingService.dump('path/to/leading.yaml', leading);
```

### Метод walkLinks

Обходит все ссылки в leading-странице.

**Параметры:**
- `leading: LeadingPage | undefined` - leading-страница
- `walker: (link: string) => string | void` - функция обработки ссылки

**Возвращает:**
- `LeadingPage | undefined` - модифицированная leading-страница или undefined

```typescript
const modifiedLeading = leadingService.walkLinks(leading, (link) => {
    // Модификация ссылки
    return modifiedLink;
});
```

### Метод deps

Получает зависимости leading-страницы.

**Параметры:**
- `path: RelativePath` - путь к файлу

**Возвращает:**
- `Promise<never[]>` - промис с массивом зависимостей

```typescript
const deps = await leadingService.deps('path/to/leading.yaml');
```

### Метод assets

Получает список ассетов leading-страницы.

**Параметры:**
- `path: RelativePath` - путь к файлу

**Возвращает:**
- `Promise<NormalizedPath[]>` - промис с массивом путей к ассетам

```typescript
const assets = await leadingService.assets('path/to/leading.yaml');
```

## Примеры использования

### Добавление информации о разделе

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

### Валидация метаданных раздела

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

### Интеграция с внешними системами

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