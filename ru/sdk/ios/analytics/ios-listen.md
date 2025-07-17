# Отслеживание активности пользователей

{% include notitle [Отслеживание активности пользователей](../../_includes/listen-intro.md) %}

## Установка длительности таймаута сессии {#timeout}

{% include notitle [отсчет таймаута](../../_includes/timeout-notify-listen.md) %}

{% list tabs group=instructions %}

  - Swift

    Чтобы изменить длительность таймаута, передайте значение в секундах в свойство `sessionTimeout` конфигурации `AppMetricaConfiguration`.

    По умолчанию длительность таймаута сессии равна 10 секундам. Это минимально допустимое значение свойства `sessionTimeout`.

    ```swift translate=no
    // Creating an extended library configuration.
    let configuration = AppMetricaConfiguration(apiKey: "API key")
    // Setting the session timeout.
    configuration?.sessionTimeout = 15
    // Initializing the AppMetrica SDK.
    AppMetrica.activate(with: configuration!)
    ```

 - Objective-C
  
    Чтобы изменить длительность таймаута, передайте значение в секундах в свойство `sessionTimeout` конфигурации `AMAAppMetricaConfiguration`.

    По умолчанию длительность таймаута сессии равна 10 секундам. Это минимально допустимое значение свойства `sessionTimeout`.

    ```obj-c translate=no
    // Creating an extended library configuration.
    AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithAPIKey:@"API key"];
    // Setting the session timeout.
    configuration.sessionTimeout = 15;
    // Initializing the AppMetrica SDK.
    [AMAAppMetrica activateWithConfiguration:configuration];
    ```

{% endlist %}

## Отслеживание сессий вручную {#listen}

По умолчанию AppMetrica отслеживает жизненный цикл приложения в автоматическом режиме. Чтобы отслеживать сессии вручную:

1. Инициализируйте библиотеку с выключенным автоматическим отслеживанием сессий `sessionsAutoTracking`.

   {% list tabs group=instructions %}

   - Swift

     ```swift translate=no
     // Creating an extended library configuration.
     if let configuration = AppMetricaConfiguration(apiKey: "API key") {
        // Disabling automatic tracking user activity.
        configuration.sessionsAutoTracking = false
        // ...
        // Initializing the AppMetrica SDK.
        AppMetrica.activate(with: configuration)
     }
     ```

   - Objective-C

     ```obj-c translate=no
     // Creating an extended library configuration.
     AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithAPIKey:@"API key"];
     // Disabling automatic tracking user activity.
     configuration.sessionsAutoTracking = NO;
     // ...
     // Initializing the AppMetrica SDK.
     [AMAAppMetrica activateWithConfiguration:configuration];
     ```

   {% endlist %}

2. Настройте контроль сессий с помощью методов `resumeSession` и `pauseSession`.

   {% list tabs group=instructions %}

   - Swift

     ```swift translate=no
     AppMetrica.resumeSession()
     // ...
     AppMetrica.pauseSession()
     ```

   - Objective-C

     ```obj-c translate=no
     [AMAAppMetrica resumeSession];
     // ...
     [AMAAppMetrica pauseSession];
     ```

   {% endlist %}

При использовании ручного отслеживания убедитесь, что активная сессия всегда завершается вызовом метода `pauseSession`. Если вы не вызовете метод `pauseSession`, сессия будет завершена при следующем запуске приложения.

## Отслеживание сессий для репортеров {#reporter-listen}

Для корректного отслеживания сессий репортеров необходимо вручную настроить отправку событий о начале и приостановке сессии для каждого репортера:

{% list tabs group=instructions %}

- Swift

  ```swift translate=no
  guard let reporter = AppMetrica.reporter(for: "API key") else {
      print("AppMetrica reporter initialization failed.")
      return // or return someDefaultValue or throw someError
  }
  reporter.resumeSession()
  // ...
  reporter.reportEvent(name: "Updates installed", onFailure: { (error) in
      print("REPORT ERROR: \(error.localizedDescription)")
  })
  // ...
  reporter.pauseSession()
  ```

- Objective-C

  ```obj-c translate=no
  id<AMAAppMetricaReporting> reporter = [AMAAppMetrica reporterForAPIKey:@"API key"];
  [reporter resumeSession];
  // ...
  [reporter reportEvent:@"Updates installed" onFailure:^(NSError *error) {
      NSLog(@"REPORT ERROR: %@", [error localizedDescription]);
  }];
  // ...
  [reporter pauseSession];
  ```

{% endlist %}

## Сессии для App Extension

По умолчанию AppMetrica SDK не отслеживает сессии для App Extension и вся активность будет считаться в фоновых сессиях. При необходимости можно использовать методы из раздела [отслеживание сессий вручную](#listen).

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}

[*timeout-session]: Таймаут сессии, который настраивается в SDK.
