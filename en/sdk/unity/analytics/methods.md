# Methods

In the code, use static methods from the `Io.AppMetrica.AppMetrica` class for accessing AppMetrica.

For details and the method reference, go to [GitHub](https://github.com/appmetrica/appmetrica-unity-plugin/blob/main/Runtime/AppMetrica.cs).

<!-- ## Активация плагина

```csharp translate=no
void Activate([NotNull] AppMetricaConfig config);
```

## Отслеживание событий

```csharp translate=no
void ReportEvent([NotNull] string message);
void ReportEvent([NotNull] string message, [CanBeNull] string json);
```

## Отслеживание крэшей и ошибок

```csharp translate=no
void ReportError([NotNull] string message, [NotNull] Exception exception);
void ReportError([NotNull] string identifier, [CanBeNull] string message, [CanBeNull] Exception exception);
void ReportUnhandledException([NotNull] Exception exception);
```

## Отслеживание сессий

```csharp translate=no
void ResumeSession();
void PauseSession();
```

## Настройки AppMetrica

```csharp translate=no
void SetLocationTracking(bool enabled);
void SetLocation([CanBeNull] Location coordinates);
void SetUserProfileID([CanBeNull] string userProfileID);
```

## Отправка Revenue

```csharp translate=no
void ReportRevenue([NotNull] Revenue revenue);
```

## Отправка AdRevenue

```csharp translate=no
void ReportAdRevenue([NotNull] AdRevenue adRevenue);
```

## Отправка пользовательских профилей

```csharp translate=no
void ReportUserProfile([NotNull] UserProfile userProfile);
```

## Отправка сообщения об открытии приложения с помощью deeplink

```csharp translate=no
void ReportAppOpen([NotNull] string deeplink);
```

## Отключение отправки статистики

```csharp translate=no
void SetDataSendingEnabled(bool enabled);
```

## Принудительная отправка событий из буфера

```csharp translate=no
void SendEventsBuffer();
```

## Получение идентификаторов AppMetrica

```csharp translate=no
void RequestStartupParams([NotNull] StartupParamsDelegate action, [NotNull] IEnumerable<string> identifiers);
```

## Информация об используемой версии AppMetrica

```csharp translate=no
string GetLibraryVersion();
```

## Установка окружения ошибки

```csharp translate=no
void PutErrorEnvironmentValue([NotNull] string key, [CanBeNull] string value);
```

## См. также

- [Как включить отправку данных о местоположении пользователей?](../../../troubleshooting/region.md)

-->

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
