# Vars Service

Vars Service is responsible for managing variables in Diplodoc. This service allows you to work with [variable presets](../../../project/presets.md) defined in `presets.yaml` files and apply them to documentation.

## Main features

- Loading and managing presets from `presets.yaml` files.
- Hierarchical preset system with inheritance support.
- Support for different environments through presets.
- Access to variables through a proxy object.

## Accessing the service

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('MyExtension', (run) => {
            // Получение сервиса из контекста
            const {vars} = run;
            
            // Получение хуков сервиса
            const varsHooks = getVarsHooks(vars);
        });
    }
}
```

## Available hooks

### PresetsLoaded

The hook is called after loading presets from a file. Allows modifying the loaded presets.

```typescript
varsHooks.PresetsLoaded.tap('MyExtension', (presets, path) => {
    // Модификация пресетов
    return presets;
});
```

### Resolved

The hook is called after resolving variables at any level. Variable data is sealed at this stage.

```typescript
varsHooks.Resolved.tap('MyExtension', (vars, path) => {
    // Обработка разрешенных переменных
});
```

## Service API

### Method init

Initializes the service by loading all `presets.yaml` files from the `input` directory.

```typescript
// Инициализация сервиса
await varsService.init();
```

### Method for

Returns a proxy object with access to variables for the specified path.

**Parameters:**
- `path` — relative path to the file.

**Returns:**
- Proxy object with access to variables.

```typescript
// Получение переменных для конкретного пути
const vars = varsService.for('path/to/file.md');

// Доступ к переменным
console.log(vars.version);
console.log(vars['version']);
```

### Method dump

Converts a preset object into a YAML string.

**Parameters:**
- `presets` — object with presets.

**Returns:**
- YAML string.

```typescript
// Дамп пресетов в YAML
const yaml = varsService.dump({
    default: {
        version: "1.0.0"
    }
});
```

### Property `entries`

Returns an object with all loaded presets.

**Returns:**
- An object where the key is the normalized directory path and the value is the presets.

```typescript
// Получение всех загруженных пресетов
const entries = varsService.entries;
```

### Working with presets

Presets are loaded from `presets.yaml` files and have the following structure:

```yaml
# Корневой presets.yaml
default:
  version: "1.0.0"
  environment: "production"

# Поддиректория/subfolder/presets.yaml
default:
  subfolder_var: "value"
  # Переопределяет значение из родительского пресета
  version: "2.0.0"
```

When accessing variables through `varsService.for(path)`, the following happens:

1. The directory hierarchy for the path is determined.
2. Each directory is checked for the presence of `presets.yaml`.
3. Variables are merged in the following order:
   - variables from the configuration (`config.vars`),
   - presets from the current directory,
   - presets from parent directories.

{% cut "Example" %}

```typescript
// Структура директорий:
// /docs
//   presets.yaml
//   /api
//     presets.yaml
//     page.md

// /docs/presets.yaml
default:
  version: "1.0.0"
  environment: "production"

// /docs/api/presets.yaml
default:
  api_version: "2.0.0"
  version: "2.0.0" // Переопределяет версию из родительского пресета

// Получение переменных для /docs/api/page.md
const vars = varsService.for('api/page.md');

// Доступ к переменным
console.log(vars.version); // "2.0.0"
console.log(vars.environment); // "production"
console.log(vars.api_version); // "2.0.0"
```

{% endcut %}

### Configuration

The service can be configured at creation time via the `options` parameter:

```typescript
const varsService = new VarsService(run, {
    // Отключить загрузку presets.yaml
    usePresets: false
});
```

## Usage examples

### Working with presets

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('PresetProcessor', (run) => {
            const varsHooks = getVarsHooks(run.vars);
            
            varsHooks.PresetsLoaded.tap('PresetProcessor', (presets, path) => {
                // Добавляем новые поля в пресеты
                return {
                    ...presets,
                    default: {
                        ...presets.default,
                        newField: 'value'
                    }
                };
            });
        });
    }
}
```

### Integration with other services

```typescript
export class Extension {
    apply(program: Build) {
        getBaseHooks(program).BeforeAnyRun.tap('ServiceIntegration', (run) => {
            const {vars, meta} = run;
            
            // Получение переменных для страницы
            const pageVars = vars.for('path/to/page.md');
            
            // Использование переменных в метаданных
            meta.addMetadata('path/to/page.md', {
                title: pageVars.title,
                description: pageVars.description
            });
        });
    }
}
```
