# Vars Service

Vars Service отвечает за управление переменными в Diplodoc. Этот сервис позволяет работать с пресетами переменных, определенными в файлах `presets.yaml`, и применять их к документации.

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
Хук вызывается после загрузки пресетов из файла. Позволяет модифицировать или валидировать загруженные пресеты.

```