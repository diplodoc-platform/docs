# Класс ReporterConfiguration

Класс содержит расширенную неизменяемую конфигурацию репортера.

Чтобы изменить конфигурацию репортера, воспользуйтесь классом [MutableReporterConfiguration](MutableReporterConfiguration.md).

## Методы экземпляра {#instance_summary}

#|
|| [init?(apiKey:)](#method_initWithApiKey) | Инициализирует экземпляр класса `ReporterConfiguration` с указанным API key. ||
|#

## Свойства {#property_summary}

#|
|| [apiKey](#property_apiKey) | API key, отличный от API key приложения. ||
|| [areLogsEnabled](#property_areLogsEnabled) | Признак включения логирования работы репортера. ||
|| [dataSendingEnabled](#property_dataSendingEnabled) | Признак включения отправки статистики. ||
|| [dispatchPeriod](#property_dispatchPeriod) | Временной интервал между отправкой событий в секундах. ||
|| [maxReportsCount](#property_maxReportsCount) | Отправка событий запускается, когда количество событий достигает `maxReportsCount`. ||
|| [maxReportsInDatabaseCount](#property_maxReportsInDatabaseCount) | Максимальное число отчетов об ошибках, которое хранится во внутренней БД. ||
|| [sessionTimeout](#property_sessionTimeout) | Таймаут сессии в секундах. ||
|| [userProfileID](#property_userProfileID) | Задает идентификатор пользовательского профиля (`ProfileID`) при активации. ||
|#

## Описание методов {#method_detail}

### init?(apiKey:) {#method_initWithApiKey}

```objectivec translate=no
init?(apiKey: String)
```

Инициализирует экземпляр класса `ReporterConfiguration` с указанным API key.

**Параметры:**

#|
|| `apiKey` | API key, отличный от API key приложения. ||
|#

**Возвращает:**

Объект класса `ReporterConfiguration`.

## Описание свойств {#property_detail}

### apiKey {#property_apiKey}

`var apiKey: String? { get }`

API key, отличный от API key приложения.

### areLogsEnabled {#property_areLogsEnabled}

`var areLogsEnabled: Bool { get }`

Признак включения логирования работы репортера.

Значение по умолчанию — `NO`.

Возможные значения:

- `YES` — логирование работы репортера включено.
- `NO` — логирование работы репортера выключено.

### dataSendingEnabled {#property_dataSendingEnabled}

`var dataSendingEnabled: Bool { get }`

Признак включения отправки статистики.
Значение по умолчанию — `YES`.

Возможные значения:
- `YES` — отправка статистики включена.
- `NO` — отправка статистики выключена.

### dispatchPeriod {#property_dispatchPeriod}

`var dispatchPeriod: UInt { get }`

Временной интервал между отправкой событий в секундах.

### maxReportsCount {#property_maxReportsCount}

`var maxReportsCount: UInt { get }`

Отправка событий запускается, когда количество событий достигает `maxReportsCount`.

### maxReportsInDatabaseCount {#property_maxReportsInDatabaseCount}

`var maxReportsInDatabaseCount { get }`

Максимальное число отчетов об ошибках, которое хранится во внутренней БД.

Допускаются значения в интервале [100; 10000]. Значения, не попадающие в данный интервал, будут автоматически заменены на значение ближайшей границы интервала.

Значение по умолчанию — 1000.

{% note info %}

Для различных `apiKey` используются отдельные БД и для них могут быть установлены независимые ограничения числа событий. Данный параметр влияет на ограничение только для соответствующего `apiKey`. Чтобы изменить максимально допустимое число событий для других `apiKey`, используйте [AppMetricaConfiguration.maxReportsInDatabaseCount](AppMetricaConfiguration.md#property_maxReportsInDatabaseCount).

{% endnote %}

### sessionTimeout {#property_sessionTimeout}

`var sessionTimeout: UInt { get }`

Таймаут сессии в секундах.

Значение по умолчанию — `10` (минимально допустимое значение).

### userProfileID {#property_userProfileID}

`var userProfileID: String? { get }`

Задает идентификатор пользовательского профиля (`ProfileID`) при активации.

{% note alert %}

Максимальная длина строки `ProfileID` — 200 символов.

{% endnote %}
