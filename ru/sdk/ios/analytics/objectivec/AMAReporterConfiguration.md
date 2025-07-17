# Класс AMAReporterConfiguration

Класс содержит расширенную неизменяемую конфигурацию репортера.

Чтобы изменить конфигурацию репортера, воспользуйтесь классом [AMAMutableReporterConfiguration](AMAMutableReporterConfiguration.md).

## Методы экземпляра {#instance_summary}

#|
|| [-initWithAPIKey:](#method_initWithAPIKey) | Инициализирует экземпляр класса `AMAReporterConfiguration` с указанным API key. ||
|#

## Свойства {#property_summary}

#|
|| [APIKey](#property_APIKey) | API key, отличный от API key приложения. ||
|| [dataSendingEnabled](#property_dataSendingEnabled) | Признак включения отправки статистики. ||
|| [dispatchPeriod](#property_dispatchPeriod) | Временной интервал между отправкой событий в секундах. ||
|| [logsEnabled](#property_logsEnabled) | Признак включения логирования работы репортера. ||
|| [maxReportsCount](#property_maxReportsCount) | Отправка событий запускается, когда количество событий достигает `maxReportsCount`. ||
|| [maxReportsInDatabaseCount](#property_maxReportsInDatabaseCount) | Максимальное число отчетов об ошибках, которое хранится во внутренней БД. ||
|| [sessionTimeout](#property_sessionTimeout) | Таймаут сессии в секундах. ||
|| [userProfileID](#property_userProfileID) | Задает идентификатор пользовательского профиля (`ProfileID`) при активации. ||
|#

## Описание методов {#method_detail}

### -initWithAPIKey: {#method_initWithAPIKey}

```objectivec translate=no
- (nullable instancetype)initWithAPIKey:(NSString *)APIKey
```

Инициализирует экземпляр класса `AMAReporterConfiguration` с указанным API key.

**Параметры:**

#|
|| `APIKey` | API key, отличный от API key приложения. ||
|#

**Возвращает:**

Объект класса `AMAReporterConfiguration`.

## Описание свойств {#property_detail}

### APIKey {#property_APIKey}

`(nonatomic, copy, nullable, readonly) NSString *APIKey`

API key, отличный от API key приложения.

### dataSendingEnabled {#property_dataSendingEnabled}

`(nonatomic, assign, readonly) BOOL dataSendingEnabled`

Признак включения отправки статистики.
Значение по умолчанию — `YES`.

Возможные значения:
- `YES` — отправка статистики включена.
- `NO` — отправка статистики выключена.

### dispatchPeriod {#property_dispatchPeriod}

`(nonatomic, assign, readonly) NSUInteger dispatchPeriod`

Временной интервал между отправкой событий в секундах.

### logsEnabled {#property_logsEnabled}

`(nonatomic, assign, readonly, getter=areLogsEnabled) BOOL logsEnabled`

Признак включения логирования работы репортера.

Значение по умолчанию — `NO`.

Возможные значения:

- `YES` — логирование работы репортера включено.
- `NO` — логирование работы репортера выключено.

### maxReportsCount {#property_maxReportsCount}

`(nonatomic, assign, readonly) NSUInteger maxReportsCount`

Отправка событий запускается, когда количество событий достигает `maxReportsCount`.

### maxReportsInDatabaseCount {#property_maxReportsInDatabaseCount}

`(nonatomic, assign, readonly) NSUInteger maxReportsInDatabaseCount`

Максимальное число отчетов об ошибках, которое хранится во внутренней БД.

Допускаются значения в интервале [100; 10000]. Значения, не попадающие в данный интервал, будут автоматически заменены на значение ближайшей границы интервала.

Значение по умолчанию — 1000.

{% note info %}

Для различных `apiKey` используются отдельные БД и для них могут быть установлены независимые ограничения числа событий. Данный параметр влияет на ограничение только для соответствующего `apiKey`. Чтобы изменить максимально допустимое число событий для других `apiKey`, используйте [AMAAppMetricaConfiguration.maxReportsInDatabaseCount](AMAAppMetricaConfiguration.md#property_maxReportsInDatabaseCount).

{% endnote %}

### sessionTimeout {#property_sessionTimeout}

`(nonatomic, assign, readonly) NSUInteger sessionTimeout`

Таймаут сессии в секундах.

Значение по умолчанию — `10` (минимально допустимое значение).
  
### userProfileID {#property_userProfileID}

`(nonatomic, copy, nullable, readonly) NSString *userProfileID`

Задает идентификатор пользовательского профиля (`ProfileID`) при активации.

{% note alert %}

Максимальная длина строки `ProfileID` — 200 символов.

{% endnote %}
