# VCS Service

VCS Service отвечает за работу с системой контроля версий в Diplodoc. Этот сервис позволяет получать информацию об авторах, контрибьюторах и времени изменения файлов, а также интегрироваться с различными VCS-провайдерами.

## Основные возможности

- Получение информации об авторах файлов
- Сбор данных о контрибьюторах
- Отслеживание времени изменения файлов
- Интеграция с различными VCS-провайдерами (GitHub, GitLab и др.)
- Управление путями к исходным файлам в VCS

## Получение доступа к сервису

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MyExtension', (run) => {
            // Получение сервиса из контекста
            const {vcs} = run;
            
            // Получение хуков сервиса
            const vcsHooks = getVcsHooks(vcs);
        });
    }
}
```

## Доступные хуки

### VcsConnector
Хук для регистрации VCS-коннектора. Вызывается при инициализации сервиса.

```typescript
vcsHooks.VcsConnector.tapPromise('MyConnector', async (connector) => {
    // connector: Текущий VCS-коннектор
    
    // Создаем и инициализируем новый коннектор
    const newConnector = new MyVcsConnector(run);
    await newConnector.init();
    
    return newConnector;
});
```

## API сервиса

### Метод init

Инициализирует сервис, загружая VCS-коннектор.

```typescript
await vcsService.init();
```

### Метод metadata

Получает метаданные VCS для файла.

**Параметры:**
- `path: RelativePath` - путь к файлу
- `meta: Meta` - метаданные файла
- `deps: NormalizedPath[]` - зависимости файла

**Возвращает:**
- `Promise<VcsMetadata>` - промис с метаданными VCS

```typescript
const metadata = await vcsService.metadata('path/to/file.md', meta, deps);
```

### Метод getContributorsByPath

Получает список контрибьюторов файла.

**Параметры:**
- `path: RelativePath` - путь к файлу
- `deps: RelativePath[]` - зависимости файла

**Возвращает:**
- `Promise<Contributor[]>` - промис с массивом контрибьюторов

```typescript
const contributors = await vcsService.getContributorsByPath('path/to/file.md', deps);
```

### Метод getModifiedTimeByPath

Получает время последнего изменения файла.

**Параметры:**
- `path: RelativePath` - путь к файлу

**Возвращает:**
- `Promise<number | null>` - промис с временем изменения в секундах

```typescript
const mtime = await vcsService.getModifiedTimeByPath('path/to/file.md');
```

### Метод getAuthorByPath

Получает автора файла.

**Параметры:**
- `path: RelativePath` - путь к файлу

**Возвращает:**
- `Promise<Contributor | null>` - промис с информацией об авторе

```typescript
const author = await vcsService.getAuthorByPath('path/to/file.md');
```

### Метод getUserByLogin

Получает информацию о пользователе по его логину.

**Параметры:**
- `author: string` - логин пользователя

**Возвращает:**
- `Promise<Contributor | null>` - промис с информацией о пользователе

```typescript
const user = await vcsService.getUserByLogin('username');
```

## Примеры использования

### Интеграция с GitHub

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('GithubVcsConnector', (run) => {
            const vcsHooks = getVcsHooks(run.vcs);
            
            vcsHooks.VcsConnector.tapPromise('GithubVcsConnector', async (_connector) => {
                const connector = new GithubVcsConnector(run);
                return connector.init();
            });
        });
    }
}
```

### Добавление информации об авторах

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('AuthorEnricher', (run) => {
            const markdownHooks = getMarkdownHooks(run.markdown);
            
            markdownHooks.Resolved.tapPromise('AuthorEnricher', async (content, meta, path) => {
                // Получаем информацию об авторе
                const author = await run.vcs.getAuthorByPath(path);
                
                if (author) {
                    // Добавляем информацию об авторе в метаданные
                    run.meta.addMetadata(path, {
                        author: author.name,
                        authorEmail: author.email
                    });
                }
                
                return content;
            });
        });
    }
}
```

### Отслеживание изменений

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('ChangeTracker', (run) => {
            const markdownHooks = getMarkdownHooks(run.markdown);
            
            markdownHooks.Resolved.tapPromise('ChangeTracker', async (content, meta, path) => {
                // Получаем время последнего изменения
                const mtime = await run.vcs.getModifiedTimeByPath(path);
                
                if (mtime) {
                    // Добавляем информацию о времени изменения
                    run.meta.addMetadata(path, {
                        lastModified: new Date(mtime * 1000).toISOString()
                    });
                }
                
                return content;
            });
        });
    }
}
```

### Сбор информации о контрибьюторах

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('ContributorsCollector', (run) => {
            const markdownHooks = getMarkdownHooks(run.markdown);
            
            markdownHooks.Resolved.tapPromise('ContributorsCollector', async (content, meta, path) => {
                // Получаем список контрибьюторов
                const contributors = await run.vcs.getContributorsByPath(path);
                
                if (contributors.length) {
                    // Добавляем информацию о контрибьюторах
                    run.meta.addMetadata(path, {
                        contributors: contributors.map(c => c.name).join(', ')
                    });
                }
                
                return content;
            });
        });
    }
} 