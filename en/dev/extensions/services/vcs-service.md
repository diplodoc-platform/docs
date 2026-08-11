# VCS Service

VCS Service is responsible for working with the version control system in Diplodoc. This service allows you to obtain information about authors, contributors, and file modification times, as well as integrate with various VCS providers.

## Main features

- Obtaining information about file authors.
- Collecting data about contributors.
- Tracking file modification times.
- Integration with various VCS providers (GitHub, GitLab, etc.).
- Managing paths to source files in VCS.

## Accessing the service

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

## Available hooks

### VcsConnector
Hook for registering a VCS connector. Called during service initialization.

```typescript
vcsHooks.VcsConnector.tapPromise('MyConnector', async (connector) => {
    // connector: Текущий VCS-коннектор
    
    // Создаем и инициализируем новый коннектор
    const newConnector = new MyVcsConnector(run);
    await newConnector.init();
    
    return newConnector;
});
```

## Service API

### Method init

Initializes the service by loading the VCS connector.

```typescript
await vcsService.init();
```

### Method metadata

Retrieves VCS metadata for a file.

**Parameters:**
- `path: RelativePath` — path to the file.
- `meta: Meta` — file metadata.
- `deps: NormalizedPath[]` — file dependencies.

**Returns:**
- `Promise<VcsMetadata>` — a promise with VCS metadata.

```typescript
const metadata = await vcsService.metadata('path/to/file.md', meta, deps);
```

### Method getContributorsByPath

Retrieves the list of contributors for a file.

**Parameters:**
- `path: RelativePath` — path to the file.
- `deps: RelativePath[]` — file dependencies.

**Returns:**
- `Promise<Contributor[]>` — a promise with an array of contributors.

```typescript
const contributors = await vcsService.getContributorsByPath('path/to/file.md', deps);
```

### Method getModifiedTimeByPath

Retrieves the last modification time of a file.

**Parameters:**
- `path: RelativePath` — path to the file.

**Returns:**
- `Promise<number | null>` — a promise with the modification time in seconds.

```typescript
const mtime = await vcsService.getModifiedTimeByPath('path/to/file.md');
```

### Method getAuthorByPath

Retrieves the author of a file.

**Parameters:**
- `path: RelativePath` — path to the file.

**Returns:**
- `Promise<Contributor | null>` — a promise with information about the author.

```typescript
const author = await vcsService.getAuthorByPath('path/to/file.md');
```

### Method getUserByLogin

Retrieves information about a user by their login.

**Parameters:**
- `author: string` — user login.

**Returns:**
- `Promise<Contributor | null>` — a promise with information about the user.

```typescript
const user = await vcsService.getUserByLogin('username');
```

## Usage examples

### Integration with GitHub

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

### Adding information about authors

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

### Tracking changes

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

### Collecting information about contributors

```typescript translate=no
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
```