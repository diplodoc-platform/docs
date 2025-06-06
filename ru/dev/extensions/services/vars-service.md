# Vars Service

Vars Service отвечает за управление переменными в Diplodoc. Этот сервис позволяет работать с пресетами переменных, определенными в файлах `presets.yaml`, и применять их к документации.

## Основные возможности

- Загрузка и управление пресетами из файлов `presets.yaml`
- Иерархическая система пресетов с поддержкой наследования
- Поддержка различных окружений через пресеты
- Доступ к переменным через прокси-объект

## Получение доступа к сервису

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

## Доступные хуки

### PresetsLoaded

Хук вызывается после загрузки пресетов из файла. Позволяет модифицировать загруженные пресеты.

```typescript
varsHooks.PresetsLoaded.tap('MyExtension', (presets, path) => {
    // Модификация пресетов
    return presets;
});
```

### Resolved

Хук вызывается после разрешения переменных на любом уровне. Данные переменных на этом этапе заморожены (sealed).

```typescript
varsHooks.Resolved.tap('MyExtension', (vars, path) => {
    // Обработка разрешенных переменных
});
```

## API сервиса

### Метод init

Инициализирует сервис, загружая все файлы `presets.yaml` из директории `input`.

```typescript
// Инициализация сервиса
await varsService.init();
```

### Метод for

Возвращает прокси-объект с доступом к переменным для указанного пути.

**Параметры:**
- `path` - относительный путь к файлу

**Возвращает:**
- Прокси-объект с доступом к переменным

```typescript
// Получение переменных для конкретного пути
const vars = varsService.for('path/to/file.md');

// Доступ к переменным
console.log(vars.version);
console.log(vars['version']);
```

### Метод dump

Преобразует объект с пресетами в YAML-строку.

**Параметры:**
- `presets` - объект с пресетами

**Возвращает:**
- YAML-строку

```typescript
// Дамп пресетов в YAML
const yaml = varsService.dump({
    default: {
        version: "1.0.0"
    }
});
```

### Свойство `entries`

Возвращает объект со всеми загруженными пресетами.

**Возвращает:**
- Объект, где ключ - нормализованный путь к директории, значение - пресеты

```typescript
// Получение всех загруженных пресетов
const entries = varsService.entries;
```

### Работа с пресетами

Пресеты загружаются из файлов `presets.yaml` и имеют следующую структуру:

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

При обращении к переменным через `varsService.for(path)` происходит следующее:

1. Определяется иерархия директорий для пути
2. Для каждой директории проверяется наличие `presets.yaml`
3. Переменные объединяются в следующем порядке:
   - Переменные из конфигурации (`config.vars`)
   - Пресеты из текущей директории
   - Пресеты из родительских директорий

{% cut "Пример" %}

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

### Конфигурация

Сервис можно настроить при создании через параметр `options`:

```typescript
const varsService = new VarsService(run, {
    // Отключить загрузку presets.yaml
    usePresets: false
});
```

## Примеры использования

### Работа с пресетами

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

### Интеграция с другими сервисами

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
