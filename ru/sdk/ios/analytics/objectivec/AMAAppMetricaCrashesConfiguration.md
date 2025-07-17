# Класс AMAAppMetricaCrashesConfiguration

Класс `AMAAppMetricaCrashesConfiguration` предоставляет настраиваемый интерфейс для управления тем, как приложение обрабатывает различные типы сбоев и проблем. Он позволяет включать или отключать определенные типы сообщений о сбоях и настраивать поведение репортера (механизма отправки сообщений).

## Свойства {#property_summary}

#|
|| [autoCrashTracking](#property_autoCrashTracking) | Управляет автоматическим отслеживанием сбоев в работе приложений. ||
|| [probablyUnhandledCrashReporting](#property_probablyUnhandledCrashReporting) | Управляет сообщениями о вероятных необработанных сбоях, таких как «Нехватка памяти» ('Out Of Memory'). ||
|| [ignoredCrashSignals](#property_ignoredCrashSignals) | Определяет массив сигналов, которые будут игнорироваться репортером. ||
|| [applicationNotRespondingDetection](#property_applicationNotRespondingDetection) | Управляет обнаружением состояния «Приложение не отвечает» (ANR). ||
|| [applicationNotRespondingWatchdogInterval](#property_applicationNotRespondingWatchdogInterval) | Устанавливает интервал времени, который будет ожидать `watchdog`, прежде чем сообщить о состоянии «Приложение не отвечает» (ANR). ||
|| [applicationNotRespondingPingInterval](#property_applicationNotRespondingPingInterval) | Устанавливает частоту, с которой `watchdog` будет проверять состояние «Приложение не отвечает» (ANR). ||
|#

### autoCrashTracking {#property_autoCrashTracking} 

```objectivec translate=no
@property (nonatomic, assign) BOOL autoCrashTracking;
```

Управляет автоматической отправкой сообщений о сбоях в работе приложения. По умолчанию включено. 

### probablyUnhandledCrashReporting {#property_probablyUnhandledCrashReporting}

```objectivec translate=no
@property (nonatomic, assign) BOOL probablyUnhandledCrashReporting;
```

Управляет сообщениями о вероятных необработанных сбоях, таких как «Нехватка памяти» ('Out Of Memory'). Используйте это свойство, чтобы включить/отключить отслеживание сбоев, которые, вероятно, не обрабатываются приложением. По умолчанию отключено.

### ignoredCrashSignals {#property_ignoredCrashSignals}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSArray<NSNumber *> *ignoredCrashSignals;
```

Определяет массив сигналов, которые будут игнорироваться репортером. Массив должен содержать `NSNumber` объектов, сконфигурированных с помощью значений сигналов так, как это определено в `sys/signal.h`. По умолчанию никакие сигналы не игнорируются.

### applicationNotRespondingDetection {#property_applicationNotRespondingDetection}

```objectivec translate=no
@property (nonatomic, assign) BOOL applicationNotRespondingDetection;
```

Управляет обнаружением состояния «Приложение не отвечает» (ANR). Если включено, репортер определит, заблокирован ли основной поток, и сообщит об этом. Обнаружение автоматически приостанавливается, когда приложение переходит в фоновый режим. По умолчанию отключено.

### applicationNotRespondingWatchdogInterval {#property_applicationNotRespondingWatchdogInterval}

```objectivec translate=no
@property (nonatomic, assign) NSTimeInterval applicationNotRespondingWatchdogInterval;
```

Устанавливает интервал времени, который будет ожидать `watchdog`, прежде чем сообщить о состоянии «Приложение не отвечает» (ANR). По умолчанию интервал равен 4 секундам. Начинает действовать только после активации и включения опции `allowsBackgroundLocationUpdates`.

### applicationNotRespondingPingInterval {#property_applicationNotRespondingPingInterval}

```objectivec translate=no
@property (nonatomic, assign) NSTimeInterval applicationNotRespondingPingInterval;
```

Устанавливает частоту, с которой `watchdog` будет проверять состояние «Приложение не отвечает» (ANR). По умолчанию интервал равен 0,1 секунды. Уменьшение интервала может привести к снижению производительности приложения. Начинает действовать только после активации и включения опции `allowsBackgroundLocationUpdates`.
