# Leading Service

Leading Service отвечает за обработку страниц оглавления (leading pages) в Diplodoc. Эти специальные страницы описывают разделы документации и содержат метаданные для них.

## Получение доступа к сервису

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MyExtension', (run) => {
            // Получение сервиса из контекста
            const {leading} = run;
            
            // Получение hooks сервиса
            const leadingHooks = getLeadingHooks(leading);
        });
    }
}
```

## Доступные hooks

### Resolved
Hook для обработки страницы оглавления после её разрешения. На этом этапе все метаданные уже загружены и могут быть модифицированы.

```typescript
leadingHooks.Resolved.tapPromise('MyProcessor', async (content, meta, path) => {
    return {
        ...content,
        section: {
            ...content.section,
            description: 'Обновленное описание раздела',
            maintainers: ['user1', 'user2'],
            meta: {
                category: 'api',
                status: 'stable'
            }
        }
    };
});
```

## API сервиса

Leading Service предоставляет методы для работы с leading-страницами:

### Основные методы

```typescript
// Инициализация сервиса
await run.leading.init();

// Загрузка leading-страницы
await run.leading.load(path);

// Сохранение leading-страницы
await run.leading.dump(path, leading);

// Обход ссылок в leading-странице
run.leading.walkLinks(leading, (link) => {
    // Обработка ссылки
    return modifiedLink;
});

// Получение зависимостей
await run.leading.deps(path);

// Получение ассетов
await run.leading.assets(path);
```

## Примеры использования

### Добавление информации о разделе

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('SectionEnricher', (run) => {
            const leadingHooks = getLeadingHooks(run.leading);
            
            leadingHooks.Resolved.tapPromise('SectionEnricher', async (content, meta, path) => {
                // Получаем дополнительную информацию о разделе
                const sectionInfo = await fetchSectionInfo(path);
                
                return {
                    ...content,
                    section: {
                        ...content.section,
                        ...sectionInfo,
                        lastUpdated: new Date().toISOString()
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
            
            leadingHooks.Resolved.tapPromise('MetadataValidator', async (content, meta, path) => {
                // Проверяем обязательные поля
                validateRequiredFields(content.section);
                
                // Проверяем корректность значений
                validateSectionValues(content.section);
                
                return content;
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
            
            leadingHooks.Resolved.tapPromise('ExternalIntegration', async (content, meta, path) => {
                // Получаем данные из внешней системы
                const externalData = await this.fetchExternalData(
                    this.apiKey,
                    content.section.id
                );
                
                return {
                    ...content,
                    section: {
                        ...content.section,
                        externalData
                    }
                };
            });
        });
    }
    
    private async fetchExternalData(apiKey: string, sectionId: string) {
        // Логика получения данных из внешней системы
    }
}
``` 