# Класс MutableReporterConfiguration

Изменяемая версия класса [ReporterConfiguration](ReporterConfiguration.md) с расширенной конфигурацией репортера.

## Свойства {#property_summary}

#|
|| [areLogsEnabled](#property_areLogsEnabled) | Включает/отключает логирование работы библиотеки. ||
|| [dataSendingEnabled](#property_dataSendingEnabled) | Включает/отключает отправку статистики на сервер AppMetrica. ||
|| [dispatchPeriod](#property_dispatchPeriod) | Временной интервал между отправкой событий в секундах. ||
|| [maxReportsCount](#property_maxReportsCount) | Отправка событий запускается, когда количество событий достигает `maxReportsCount`. ||
|| [maxReportsInDatabaseCount](#property_maxReportsInDatabaseCount) | Максимальное число отчетов об ошибках, которое хранится во внутренней БД. ||
|| [sessionTimeout](#property_sessionTimeout) | Задает длительность таймаута сессии в секундах. ||
|| [userProfileID](#property_userProfileID) | Задает идентификатор пользовательского профиля (`ProfileID`) при активации. ||
|#

## Описание свойств {#property_detail}

### areLogsEnabled {#property_areLogsEnabled}

`var areLogsEnabled: Bool`

Включает/отключает логирование работы библиотеки.

По умолчанию логирование выключено.

### dataSendingEnabled {#property_dataSendingEnabled}

`var dataSendingEnabled: Bool`

Включает/отключает отправку статистики на сервер AppMetrica.

{% note info %}

Отключение отправки статистики для репортера не влияет на отправку данных с главного API key. Но отключение отправки данных для главного API key прекращает отправку статистики со всех репортеров.

{% endnote %}

По умолчанию отправка статистики включена.

### dispatchPeriod {#property_dispatchPeriod}

`var dispatchPeriod: UInt`

Временной интервал между отправкой событий в секундах.

### maxReportsCount {#property_maxReportsCount}

`var maxReportsCount: UInt`

Отправка событий запускается, когда количество событий достигает `maxReportsCount`.

### maxReportsInDatabaseCount {#property_maxReportsInDatabaseCount}

`var maxReportsInDatabaseCount: UInt`

Максимальное число отчетов об ошибках, которое хранится во внутренней БД.

Допускаются значения в интервале [100; 10000]. Значения, не попадающие в данный интервал, будут автоматически заменены на значение ближайшей границы интервала.

Значение по умолчанию — 1000.

{% note info %}

Для различных `apiKey` используются отдельные БД и для них могут быть установлены независимые ограничения числа событий. Данный параметр влияет на ограничение только для соответствующего `apiKey`. Чтобы изменить максимально допустимое число событий для других `apiKey`, используйте [AppMetricaConfiguration.maxReportsInDatabaseCount](AppMetricaConfiguration.md#property_maxReportsInDatabaseCount).

{% endnote %}

### sessionTimeout {#property_sessionTimeout}

`var sessionTimeout: UInt`

Задает длительность тайм-аута сессии в секундах.

Значение по умолчанию — `10` (минимально допустимое значение).

### userProfileID {#property_userProfileID}

`var userProfileID: String?`

Задает идентификатор пользовательского профиля (`ProfileID`) при активации.

{% note alert %}

Максимальная длина строки `ProfileID` — 200 символов.

{% endnote %}
