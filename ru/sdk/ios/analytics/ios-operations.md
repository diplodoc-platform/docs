# Примеры использования методов

## Инициализация библиотеки с расширенной конфигурацией {#initialize}

Чтобы инициализировать библиотеку с расширенной стартовой конфигурацией:

{% list tabs group=instructions %}

- Swift

  1. Инициализируйте объект класса `AppMetricaConfiguration`.
  2. Задайте настройки конфигурации с помощью методов класса `AppMetricaConfiguration`. Например, включите логирование или установите таймаут сессии.
  3. Передайте объект `AppMetricaConfiguration` в метод `activate(with:)` класса `AppMetrica`.

  Настройки расширенной конфигурации применяются с момента инициализации библиотеки. Чтобы настроить библиотеку в процессе работы приложения, используйте методы класса `AppMetrica`.

  ```swift translate=no
  func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey : AnyObject]? = nil) -> Bool {
      // Creating an extended library configuration.
      if let configuration = AppMetricaConfiguration(apiKey: "API key") {
          // Setting up the configuration. For example, to enable logging.
          configuration.areLogsEnabled = true
          // ...
          // Initializing the AppMetrica SDK.
          AppMetrica.activate(with: configuration)
      }
  }
  ```

- Objective-c

  1. Инициализируйте объект класса `AMAAppMetricaConfiguration`.
  2. Задайте настройки конфигурации с помощью методов класса `AMAAppMetricaConfiguration`. Например, включите логирование или установите таймаут сессии.
  3. Передайте объект `AMAAppMetricaConfiguration` в метод `+activateWithConfiguration:` класса `AMAAppMetrica`.

  Настройки расширенной конфигурации применяются с момента инициализации библиотеки. Чтобы настроить библиотеку в процессе работы приложения, используйте методы класса `AMAAppMetrica`.

  ```obj-c translate=no
  - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
  {
      // Creating an extended library configuration.
      AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithAPIKey:@"API key"];
      // Setting up the configuration. For example, to enable logging.
      configuration.logsEnabled = YES;
      // ...
      // Initializing the AppMetrica SDK.
      [AMAAppMetrica activateWithConfiguration:configuration];
      return YES;
  }
  ```

{% endlist %}

{% cut "Что такое API key?" %}

{{ api-key }}

{% endcut %}

## Отправка статистики на дополнительный API key {#reporter-different-apikey}

Отправка данных на дополнительный API key позволяет собирать для каждого API key свою статистику. Это можно использовать для управления доступом к информации. Например, чтобы предоставить доступ к статистике для аналитиков, можно продублировать отправку маркетинговых данных на дополнительный API key и предоставить им доступ к этой статистике. Так у них будет доступ только к той информации, которая им необходима.

Для отправки данных на дополнительный API key необходимо использовать репортеры. С помощью них можно отправлять события, сообщения об ошибках, профили и информацию о покупках в приложении. Репортеры могут работать без инициализации AppMetrica SDK.

### Шаг 1. (Опционально) Инициализируйте репортер с расширенной конфигурацией {#reporter-different-apikey-initialize}

{% note warning %}

Инициализацию репортера с расширенной конфигурацией необходимо проводить до первого обращения к репортеру. Иначе репортер будет инициализирован без конфигурации.

{% endnote %}

Чтобы инициализировать репортер с расширенной конфигурацией:

{% list tabs group=instructions %}

- Swift

  1. Инициализируйте объект класса `MutableReporterConfiguration`.
  2. Задайте настройки конфигурации с помощью методов класса `MutableReporterConfiguration`. Например, включите логирование или установите таймаут сессии.
  3. Передайте объект `MutableReporterConfiguration` в метод `activateReporter(with:)` класса `AppMetrica`.
  4. Конфигурация применяется для репортера с указанным API key. Для каждого дополнительного API key можно настроить свою конфигурацию.

  ```swift translate=no
  // Creating an extended library configuration.
  // To create it, pass an API key that is different from the app's API key.
  if let reporterConfiguration = MutableReporterConfiguration(apiKey: "API key") {
      // Setting up the configuration. For example, to enable logging.
      reporterConfiguration.areLogsEnabled = true
      // ...
      // Initializing a reporter.
      AppMetrica.activateReporter(with: reporterConfiguration)
  }
  ```

- Objective-c

  1. Инициализируйте объект класса `AMAMutableReporterConfiguration`.
  2. Задайте настройки конфигурации с помощью методов класса `AMAMutableReporterConfiguration`. Например, включите логирование или установите таймаут сессии.
  3. Передайте объект `AMAMutableReporterConfiguration` в метод `+activateReporterWithConfiguration:` класса `AMAAppMetrica`.
  4. Конфигурация применяется для репортера с указанным API key. Для каждого дополнительного API key можно настроить свою конфигурацию.

  ```obj-c translate=no
  // Creating an extended library configuration.
  // To create it, pass an API key that is different from the app's API key.
  AMAMutableReporterConfiguration *reporterConfiguration = [[AMAMutableReporterConfiguration alloc] initWithAPIKey:@"API key"];
  // Setting up the configuration. For example, to enable logging.
  reporterConfiguration.logsEnabled = YES;
  // ...
  // Initializing a reporter.
  [AMAAppMetrica activateReporterWithConfiguration:[reporterConfiguration copy]];
  ```

{% endlist %}

{% cut "Что такое API key?" %}

{{ api-key }}

{% endcut %}

### Шаг 2. Настройте отправку данных с помощью репортера {#reporter-different-apikey-send}

Чтобы отправить данные на другой API key:

{% list tabs group=instructions %}

- Swift

  1. С помощью метода `reporter(for:)` класса `AppMetrica` получите объект, который реализует протокол `AppMetricaReporting`.

     Если репортер не был инициализирован с расширенной конфигурацией, то вызов данного метода произведет инициализацию репортера для указанного API key.

  2. Используйте методы протокола `AppMetricaReporting` для отправки событий и Revenue.
  3. Чтобы сессии отслеживались правильно, настройте отправку событий о начале и приостановке сессии для каждого репортера.


  ```swift translate=no
  guard let reporter = AppMetrica.reporter(for: "API key") else {
      print("REPORT ERROR: Failed to create AppMetrica reporter")
      return // or return someDefaultValue or throw someError
  }
  reporter.resumeSession()
  // ...
  reporter.reportEvent(name: "Updates installed", onFailure: { (error) in
      print("REPORT ERROR: %@", error.localizedDescription)
  })
  // ...
  reporter.pauseSession()
  ```

- Objective-C

  1. С помощью метода `+reporterForAPIKey:` класса `AMAAppMetrica` получите объект, который реализует протокол `AMAAppMetricaReporting`.

     Если репортер не был инициализирован с расширенной конфигурацией, то вызов данного метода произведет инициализацию репортера для указанного API key.

  2. Используйте методы протокола `AMAAppMetricaReporting` для отправки событий и Revenue.
  3. Чтобы сессии отслеживались правильно, настройте отправку событий о начале и приостановке сессии для каждого репортера.

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

{% cut "Что такое API key?" %}

{{ api-key }}

{% endcut %}

## Отслеживание аварийных остановок приложения {#set-report-crash}

Отчеты об аварийных остановках приложения отправляются по умолчанию.

Чтобы отключить автоматическое отслеживание, передайте крэш модулю конфигурацию, в которой отправка информации об аварийных остановках приложения отключена.

{% list tabs group=instructions %}

- Swift

  Для этого установите значение `false` для свойства `autoCrashTracking` конфигурации `AppMetricaCrashesConfiguration`.

  ```swift translate=no
  // Creating an crashes configuration.
  let configuration = AppMetricaCrashesConfiguration()
  // Disabling sending the information on crashes of the application.
  configuration.autoCrashTracking = false
  // Set the configuration for AppMetricaCrashes.
  AppMetricaCrashes.crashes().setConfiguration(configuration)
  ```

- Objective-C

  Для этого установите значение `NO` для свойства `autoCrashTracking` конфигурации `AMAAppMetricaCrashesConfiguration`.

  ```obj-c translate=no
  // Creating an crashes configuration.
  AMAAppMetricaCrashesConfiguration *configuration = [[AMAAppMetricaCrashesConfiguration alloc] init];
  // Disabling sending the information on crashes of the application.
  configuration.autoCrashTracking = NO;
  // Set the configuration in AppMetricaCrashes.
  [[AMAAppMetricaCrashes crashes] setConfiguration:configuration];
  ```

{% endlist %}

## Определение местоположения {#track-location}

AppMetrica умеет определять местоположение устройства. Точность определения зависит от конфигурации, с которой инициализируется библиотека:

1. С включенной опцией `locationTracking`. Для iOS опция включена по умолчанию.

   Местоположение определяется с точностью до города. Информация доступна в [отчетах](../../../mobile-reports/index.md) и в [Logs API](../../../mobile-api/logs/about.md).

   Приложение запрашивает доступ к GPS. Расход заряда аккумулятора может увеличиться.

2. С отключенной опцией `locationTracking`.

   Местоположение определяется по IP-адресу с точностью до страны. Информация доступна в [отчетах](../../../mobile-reports/index.md) и в [Logs API](../../../mobile-api/logs/about.md).

   Приложение не запрашивает доступ к GPS. Расход заряда аккумулятора не увеличивается.

   {% note info %}

   Если у вас включена маскировка IP-адреса, местоположение определяется так же с точностью до страны по немаскированной части IP-адреса.

   {% endnote %}

По умолчанию AppMetrica SDK инициализируется с включенным `locationTracking`, но AppMetrica SDK не запрашивает разрешение на получение данных о местоположении. Это необходимо сделать самостоятельно с помощью методов класса [CLLocationManager](https://developer.apple.com/documentation/corelocation/cllocationmanager?language=objc).

{% list tabs group=instructions %}

  - Swift

    Чтобы инициализировать библиотеку с отключенным `locationTracking`, установите значение `false` для свойства `locationTracking` конфигурации `AppMetricaConfiguration`.

    ```swift translate=no
    // Creating an extended library configuration.
    if let configuration = AppMetricaConfiguration(apiKey: "API key") {
        // Disabling sending information about the location of the device.
        configuration.locationTracking = false
        // Initializing the AppMetrica SDK.
        AppMetrica.activate(with: configuration)
    }
    ```

    Чтобы отключить `locationTracking` после инициализации библиотеки, используйте свойство `isLocationTrackingEnabled` класса `AppMetrica`:

    ```swift translate=no
    AppMetrica.isLocationTrackingEnabled = false
    ```

  - Objective-C

    Чтобы инициализировать библиотеку с отключенным `locationTracking`, установите значение `NO` для свойства `locationTracking` конфигурации `AMAAppMetricaConfiguration`.

    ```obj-c translate=no
    // Creating an extended library configuration.
    AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithAPIKey:@"API key"];
    // Disabling sending information about the device location.
    configuration.locationTracking = NO;
    // Initializing the AppMetrica SDK.
    [AMAAppMetrica activateWithConfiguration:configuration];
    ```

    Чтобы отключить `locationTracking` после инициализации библиотеки, используйте метод `+setLocationTrackingEnabled:` класса `AMAAppMetrica`:

    ```obj-c translate=no
    AMAAppMetrica.locationTrackingEnabled = NO;
    ```

{% endlist %}

## Установка местоположения устройства вручную {#location-manual}

Перед отправкой собственной информации о местоположении устройства убедитесь, что отправка отчетов была включена.

По умолчанию местоположение устройства определяется библиотекой.

{% list tabs group=instructions %}

  - Swift

    Чтобы отправить собственную информацию о местоположении устройства, передайте объект [CLLocation](https://developer.apple.com/documentation/corelocation/cllocation) в свойство `customLocation` класса `AppMetrica`.

    ```swift translate=no
    func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
        AppMetrica.customLocation = locations.last
    }
    ```

    Чтобы отправить собственную информацию о местоположении устройства с помощью стартовой конфигурации, передайте объект [CLLocation](https://developer.apple.com/documentation/corelocation/cllocation) в свойство `customLocation` конфигурации `AppMetricaConfiguration`.

    ```swift translate=no
    // Creating an extended library configuration.
    if let configuration = AppMetricaConfiguration(apiKey: "API key") {
      // Set a custom location.
      configuration.customLocation = CLLocation(latitude: 0, longitude: 0)
      // Initializing the AppMetrica SDK.
      AppMetrica.activate(with: configuration)
    }
    ```

  - Objective-C

    Чтобы отправить собственную информацию о местоположении устройства, передайте объект [CLLocation](https://developer.apple.com/documentation/corelocation/cllocation) в метод `setCustomLocation` класса `AMAAppMetrica`.

    ```obj-c translate=no
    - (void)locationManager:(CLLocationManager *)manager
        didUpdateToLocation:(CLLocation *)newLocation
               fromLocation:(CLLocation *)oldLocation
    {
        AMAAppMetrica.customLocation = newLocation;
    }
    ```

    Чтобы отправить собственную информацию о местоположении устройства с помощью стартовой конфигурации, передайте объект [CLLocation](https://developer.apple.com/documentation/corelocation/cllocation) в свойство `customLocation` конфигурации `AMAAppMetricaConfiguration`.

    ```obj-c translate=no
    // Creating an extended library configuration.
    AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithAPIKey:@"API key"];
    // Set a custom location.
    configuration.customLocation = [[CLLocation alloc] initWithLatitude:0 longitude:0];
    // Initializing the AppMetrica SDK.
    [AMAAppMetrica activateWithConfiguration:configuration];
    ```

{% endlist %}

## Отправка собственного события {#report-event}

{% list tabs group=instructions %}

  - Swift

    Чтобы отправить собственное событие без вложенных параметров, передайте в метод `reportEvent(name:onFailure:)` класса `AppMetrica` следующие параметры:

    * `name` — короткое название или описание события.
    * `onFailure` — блок, в который передается ошибка. Если вы не хотите отслеживать ошибку, то передайте в качестве блока значение `nil`.

    ```swift translate=no
    var message = "Updates installed"
    AppMetrica.reportEvent(name: message, onFailure: { (error) in
        print("DID FAIL TO REPORT EVENT: %@", message)
        print("REPORT ERROR: %@", error.localizedDescription)
    })
    ```

  - Objective-C

    Чтобы отправить собственное событие без вложенных параметров, передайте в метод `+reportEvent:onFailure:` класса `AMAAppMetrica` следующие параметры:

    * `message` — короткое название или описание события.
    * `onFailure` — блок, в который передается ошибка. Если вы не хотите отслеживать ошибку, то передайте в качестве блока значение `nil`.

    ```obj-c translate=no
    NSString *message = @"Updates installed";
    [AMAAppMetrica reportEvent:message onFailure:^(NSError *error) {
        NSLog(@"DID FAIL REPORT EVENT: %@", message);
        NSLog(@"REPORT ERROR: %@", [error localizedDescription]);
    }];
    ```

{% endlist %}

## Отправка собственного события с вложенными параметрами {#report-event-params}

{% list tabs group=instructions %}

  - Swift

    Чтобы отправить собственное событие с вложенными параметрами, передайте в метод `reportEvent(name:parameters:onFailure:)` класса `AppMetrica` следующие параметры:

    * `name` — короткое название или описание события.
    * `parameters` — вложенные параметры в виде пар «ключ-значение».
    
      Веб-интерфейс AppMetrica отображает до пяти уровней вложенности события. Если событие содержит шесть уровней и более, в отчете отобразятся пять верхних. С помощью [API отчетов](../../../mobile-api/api_v1/intro.md) можно выгрузить до десяти уровней.
    
    * `onFailure` — блок, в который передается ошибка. Если вы не хотите отслеживать ошибку, то передайте в качестве блока значение `nil`.

    ```swift translate=no
    var message = "Updates installed"
    let params = ["key1": "value1", "key2": "value2"]
    AppMetrica.reportEvent(name: message, parameters: params, onFailure: { (error) in
        print("DID FAIL REPORT EVENT: %@", message)
        print("REPORT ERROR: %@", error.localizedDescription)
    })
    ```

  - Objective-C

    Чтобы отправить собственное событие с вложенными параметрами, передайте в метод `+reportEvent:parameters:onFailure:` класса `AMAAppMetrica` следующие параметры:

    * `message` — короткое название или описание события.
    * `parameters` — вложенные параметры в виде пар «ключ-значение».
    
      Веб-интерфейс AppMetrica отображает до пяти уровней вложенности события. Если событие содержит шесть уровней и более, в отчете отобразятся пять верхних. С помощью [API отчетов](../../../mobile-api/api_v1/intro.md) можно выгрузить до десяти уровней.
    
    * `onFailure` — блок, в который передается ошибка. Если вы не хотите отслеживать ошибку, то передайте в качестве блока значение `nil`.

    ```obj-c translate=no
    NSString *message = @"Updates installed";
    NSDictionary *params = @{@"key1": @"value1", @"key2": @"value2"};
    [AMAAppMetrica reportEvent:message parameters:params onFailure:^(NSError *error) {
        NSLog(@"DID FAIL REPORT EVENT: %@", message);
        NSLog(@"REPORT ERROR: %@", [error localizedDescription]);
    }];
    ```

{% endlist %}

Подробнее о событиях в разделе [События](../../../data-collection/about-events.md).

## Отправка события из JavaScript-кода WebView {#js-event}

AppMetrica SDK позволяет отправлять клиентские события из JavaScript-кода. Для этого требуется подключить модуль `AppMetricaWebKit` через систему управления зависимостями, которую вы используете.

{% list tabs group=instructions %}

  - Swift

    Добавьте импорт:
    ```swift translate=no
    import AppMetricaWebKit
    ```

    Инициализируйте отправку вызовом метода `setupWebViewReporting(with:onFailure:)`:

    ```swift translate=no
    let userController = WKUserContentController()
    AppMetrica.setupWebViewReporting(with: JSController(userContentController:userController), onFailure: nil)
    userController.add(myHandler, name: myScriptName)
    let configuration = WKWebViewConfiguration()
    configuration.userContentController = userController;
    let webView = WKWebView(frame: .zero, configuration: configuration)
    ```

  - Objective-C

    Добавьте импорт:

    ```obj-c translate=no
    #import <AppMetricaWebKit/AppMetricaWebKit.h>
    ```

    Инициализируйте отправку вызовом метода `+setupWebViewReporting:onFailure:`:

    ```obj-c translate=no
    WKUserContentController *userController = [[WKUserContentController alloc] init];
    [AMAAppMetrica setupWebViewReporting:[[AMAJSController alloc] initWithUserContentController:userController] onFailure:nil];
    [userController addScriptMessageHandler:myHandler name:myScriptName];
    WKWebViewConfiguration *configuration = [[WKWebViewConfiguration alloc] init];
    configuration.userContentController = userController;
    WKWebView *webView = [[WKWebView alloc] initWithFrame:CGRectZero configuration:configuration];
    ```

{% endlist %}

Метод необходимо вызывать до загрузки любого контента. Рекомендуется вызывать метод до создания вебвью и до добавления своих скриптов в [WKUserContentController](https://developer.apple.com/documentation/webkit/wkusercontentcontroller).

Для отправки события из JavaScript-кода используйте метод `reportEvent(name, value)` интерфейса AppMetrica:

```javascript translate=no
function buttonClicked() {
  AppMetrica.reportEvent('Button clicked!', '{}');
}
```

Аргументы метода `reportEvent`:

* `name` — строка. Не может быть `null` или пустым.
* `value` — JSON-строка. Может быть `null`.

## Отправка собственного сообщения об ошибке {#send-report-error}

Для отправки сообщения об ошибке требуется подключить модуль `AppMetricaCrashes` через систему управления зависимостями, которую вы используете.

{% list tabs group=instructions %}

- Swift

  Чтобы отправить собственное сообщение об ошибке, необходимо добавить импорт:

  ```swift translate=no
  import AppMetricaCrashes
  ```
  
  Даллее используйте методы класса `AppMetricaCrashes` и протокола `AppMetricaCrashReporting`:

  * `report(error:onFailure:)`
  * `report(error:options:onFailure:)`
  * `report(nserror:onFailure:)`
  * `report(nserror:options:onFailure:)`

  Для отправки можно использовать стандартный класс [NSError](https://developer.apple.com/documentation/foundation/nserror?changes=_1), упрощенный класс `AppMetricaError` или протокол `ErrorRepresentable`.

- Objective-C

  Чтобы отправить собственное сообщение об ошибке, необходимо добавить импорт:

  ```obj-c translate=no
  #import <AppMetricaCrashes/AppMetricaCrashes.h>
  ```

  Далее используйте методы класса `AMAAppMetricaCrashes` и протокола `AMAAppMetricaCrashReporting`:

  * `-reportError:onFailure:`
  * `-reportError:options:onFailure:`
  * `-reportNSError:onFailure:`
  * `-reportNSError:options:onFailure:`

  Для отправки можно использовать стандартный класс [NSError](https://developer.apple.com/documentation/foundation/nserror?changes=_1), упрощенный класс `AMAError` или протокол `AMAErrorRepresentable`.

{% endlist %}

### Пример с NSError {#send-report-error-nserror}

Если ошибки отправляются с использованием класса [NSError](https://developer.apple.com/documentation/foundation/nserror?changes=_1&language=objc), они группируются по домену [domain](https://developer.apple.com/documentation/foundation/nserror/1413924-domain?changes=_1) и коду ошибки [code](https://developer.apple.com/documentation/foundation/nserror/1409165-code?changes=_1).

{% list tabs group=instructions %}

- Swift

  ```swift translate=no
  let firstError = NSError(domain: "io.appmetrica.error-a", code: 12, userInfo: [
      BacktraceErrorKey: Thread.callStackReturnAddresses,
      NSLocalizedDescriptionKey: "Error A"
  ])
  AppMetricaCrashes.crashes().report(nserror: firstError)
  ```

- Objective-C

  ```obj-c translate=no
  NSError *firstError = [NSError errorWithDomain:@"io.appmetrica.error-a"
                                            code:12
                                        userInfo:@{
                                             AMABacktraceErrorKey: NSThread.callStackReturnAddresses,
                                             NSLocalizedDescriptionKey: @"Error A"
                                        }];
  [[AMAAppMetricaCrashes crashes] reportNSError:firstError onFailure:nil];
  ```

{% endlist %}

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/domain-groups.png){style="border: solid 1px #cccccc;"}

### Пример c AppMetricaError {#send-report-error-appmetricaerror}

{% list tabs group=instructions %}

  - Swift

    Если ошибки отправляются с использованием класса `AppMetricaError` или протокола `ErrorRepresentable`, они группируются по идентификатору `identifier`.

    ```swift translate=no
    let underlyingError = AppMetricaError(identifier: "Underlying AMAError")
    let error = AppMetricaError(
        identifier: "AMAError identifier",
        message: "Another custom message",
        parameters: [
            "foo": "bar"
        ],
        backtrace: Thread.callStackReturnAddresses,
        underlyingError: underlyingError
    )
    AppMetricaCrashes.crashes().report(error: error)
    ```

  - Objective-C

    Если ошибки отправляются с использованием класса `AMAError` или протокола `AMAErrorRepresentable`, они группируются по идентификатору `identifier`.

    ```obj-c translate=no
    AMAError *underlyingError = [AMAError errorWithIdentifier:@"Underlying AMAError"];
    AMAError *error = [AMAError errorWithIdentifier:@"AMAError identifier"
                                            message:@"Another custom message"
                                         parameters:@{ @"foo": @"bar" }
                                          backtrace:NSThread.callStackReturnAddresses
                                    underlyingError:underlyingError];
    [[AMAAppMetricaCrashes crashes] reportError:error onFailure:nil];
    ```

{% endlist %}

Не используйте переменные значения в качестве идентификатора для группировки. Иначе количество групп будет увеличиваться и их будет сложно анализировать.

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/id-groups.png){style="border: solid 1px #cccccc;"}

## Отправка ProfileId {#send-profile-id}

Если отправка `ProfileId` не настроена, в веб-интерфейсе будет отображаться `appmetrica_device_id`.

{% list tabs group=instructions %}

  - Swift

    Чтобы отправить `ProfileId`, используйте свойство `userProfileID` класса `AppMetrica`.

    ```swift translate=no
    AppMetrica.userProfileID = "id"
    ```

  - Objective-C

    Чтобы отправить `ProfileId`, используйте метод `+setUserProfileID:` класса `AMAAppMetrica`.

    ```obj-c translate=no
    AMAAppMetrica.userProfileID = @"id";
    ```

{% endlist %}

## Отправка событий из буфера {#send-events-buffer}

AppMetrica SDK не отправляет событие сразу после того, как оно произошло. Библиотека хранит данные о событиях в буфере. Метод `sendEventsBuffer` инициирует отправку данных из буфера и очищает его. Используйте этот метод для принудительной отправки сохраненных событий после прохождения важных сценариев пользователя.

{% list tabs group=instructions %}

- Swift

  ```swift translate=no
  AppMetrica.sendEventsBuffer()
  ```

- Objective-C

  ```obj-c translate=no
  [AMAAppMetrica sendEventsBuffer];
  ```

{% endlist %}

{% note alert "" %}

Частое использование метода может привести к повышению энергопотребления и расходу интернет-трафика.

{% endnote %}

## Отправка атрибутов профиля {#send-attribute-profile}

{% list tabs group=instructions %}

  - Swift

    Чтобы отправить атрибуты профиля, передайте в метод `reportUserProfile(_:onFailure:)` класса `AppMetrica` следующие параметры:

    * `userProfile` — объект `UserProfile`, который содержит массив обновлений атрибутов. Атрибуты профиля создаются с помощью методов класса `ProfileAttribute`.
    * `onFailure` — блок, в который передается ошибка. Если вы не хотите отслеживать ошибку, то передайте в качестве блока значение `nil`.

    ```swift translate=no
    let profile = MutableUserProfile()
    // Updating a single user profile attribute.
    let timeLeftAttribute = ProfileAttribute.customCounter("time_left")
    profile.apply(timeLeftAttribute.withDelta(-4.42))
    // Updating multiple attributes.
    profile.apply(from: [
        // Updating predefined attributes.
        ProfileAttribute.name().withValue("John"),
        ProfileAttribute.gender().withValue(GenderType.male),
        ProfileAttribute.birthDate().withAge(24),
        ProfileAttribute.notificationsEnabled().withValue(false),
        // Updating custom attributes.
        ProfileAttribute.customString("born_in").withValueIfUndefined("Moscow"),
        ProfileAttribute.customString("address").withValueReset(),
        ProfileAttribute.customNumber("age").withValue(24),
        ProfileAttribute.customCounter("logins_count").withDelta(1),
        ProfileAttribute.customBool("has_premium").withValue(true)
    ])
    // ProfieID is set using the method of the AppMetrica class.
    AppMetrica.userProfileID = "id"

    // Sending profile attributes.
    AppMetrica.reportUserProfile(profile, onFailure: { (error) in
        print("REPORT ERROR: %@", error.localizedDescription)
    })
    ```

  - Objective-C

    Чтобы отправить атрибуты профиля, передайте в метод `+reportUserProfile:onFailure:` класса `AMAAppMetrica` следующие параметры:

    * `userProfile` — объект `AMAUserProfile`, который содержит массив обновлений атрибутов. Атрибуты профиля создаются с помощью методов класса `AMAProfileAttribute`.
    * `onFailure` — блок, в который передается ошибка. Если вы не хотите отслеживать ошибку, то передайте в качестве блока значение `nil`.

    ```obj-c translate=no
    AMAMutableUserProfile *profile = [[AMAMutableUserProfile alloc] init];
    // Updating a single user profile attribute.
    id<AMACustomCounterAttribute> timeLeftAttribute = [AMAProfileAttribute customCounter:@"time_left"];
    [profile apply:[timeLeftAttribute withDelta:-4.42]];
    // Updating multiple attributes.
    [profile applyFromArray:@[
        // Updating predefined attributes.
        [[AMAProfileAttribute name] withValue:@"John"],
        [[AMAProfileAttribute gender] withValue:AMAGenderTypeMale],
        [[AMAProfileAttribute birthDate] withAge:24],
        [[AMAProfileAttribute notificationsEnabled] withValue:NO],
        // Updating custom attributes.
        [[AMAProfileAttribute customString:@"born_in"] withValueIfUndefined:@"Moscow"],
        [[AMAProfileAttribute customString:@"address"] withValueReset],
        [[AMAProfileAttribute customNumber:@"age"] withValue:24],
        [[AMAProfileAttribute customCounter:@"logins_count"] withDelta:1],
        [[AMAProfileAttribute customBool:@"has_premium"] withValue:YES]
    ]];
    // ProfieID is set using the method of the AMAAppMetrica class.
    [AMAAppMetrica setUserProfileID:@"id"];

    // Sending profile attributes.
    [AMAAppMetrica reportUserProfile:[profile copy] onFailure:^(NSError *error) {
        NSLog(@"Error: %@", error);
    }];
    ```

{% endlist %}



## Отправка ECommerce-событий {#send-ecommerce}

В AppMetrica нет возможности сегментировать ECommerce-события на «тестовые» и «не тестовые». Если для отладки покупок вы используете основной API key, то тестовые события будут попадать в общую статистику. Поэтому, чтобы отладить отправку ECommerce-событий, используйте отправку статистики на дополнительный API key с помощью репортера.

### Шаг 1. Настройте отправку ECommerce-событий на тестовый API key {#send-ecommerce-test-key}

Для различных действий пользователя есть соответствующие типы ECommerce-событий. Чтобы создать конкретный тип события, используйте нужный метод класса `ECommerce`.

Ниже приведены примеры отправки конкретных типов событий:

{% cut "Открытие страницы" %}

   {% list tabs group=instructions %}

   - Swift

     ```swift translate=no
     // Creating a screen object.
     let screen = ECommerceScreen(
             name: "ProductCardScreen",
             categoryComponents: ["Акции", "Красная цена"],
             searchQuery: "даниссимо кленовый сироп",
             payload: ["full_screen": "true"]
     )
     // Sending an e-commerce event.
     if let reporter = AppMetrica.reporter(for: "Testing API key") {
        reporter.reportECommerce(.showScreenEvent(screen: screen))
     }
     ```

   - Objective-C

     ```obj-c translate=no
     // Creating a screen object.
     AMAECommerceScreen *screen = [[AMAECommerceScreen alloc] initWithName:@"ProductCardScreen"
                                                        categoryComponents:@[ @"Акции", @"Красная цена" ]
                                                               searchQuery:@"даниссимо кленовый сироп"
                                                                   payload:@{ @"full_screen": @"true" }];
     // Sending an e-commerce event.
     id<AMAAppMetricaReporting> reporter = [AMAAppMetrica reporterForAPIKey:@"Testing API key"];
     [reporter reportECommerce:[AMAECommerce showScreenEventWithScreen:screen] onFailure:nil];
     ```

   {% endlist %}

{% endcut %}

{% cut "Просмотр карточки товара" %}

   {% list tabs group=instructions %}

   - Swift

     ```swift translate=no
     // Creating a screen object.
     let screen = ECommerceScreen(
             name: "ProductCardScreen",
             categoryComponents: ["Акции", "Красная цена"],
             searchQuery: "даниссимо кленовый сироп",
             payload: ["full_screen": "true"]
     )
     // Creating an actualPrice object.
     let actualPrice = ECommercePrice(
             fiat: .init(unit: "USD", value: .init(string: "4.53")),
             internalComponents: [
                 .init(unit: "wood", value: .init(string: "30570000")),
                 .init(unit: "iron", value: .init(string: "26.89")),
                 .init(unit: "gold", value: .init(string: "5.1")),
             ]
     )
     // Creating a product object.
     let product = ECommerceProduct(
             sku: "779213",
             name: "Продукт творожный «Даниссимо» 5.9%, 130 г.",
             categoryComponents: ["Продукты", "Молочные продукты", "Йогурты"],
             payload: ["full_screen": "true"],
             actualPrice: actualPrice,
             originalPrice: .init(
                     fiat: .init(unit: "USD", value: .init(string: "5.78")),
                     internalComponents: [
                         .init(unit: "wood", value: .init(string: "30590000")),
                         .init(unit: "iron", value: .init(string: "26.92")),
                         .init(unit: "gold", value: .init(string: "5.5")),
                     ]
             ),
             promoCodes: ["BT79IYX", "UT5412EP"]
     )
     // Sending an e-commerce event.
     if let reporter = AppMetrica.reporter(for: "Testing API key") {
        reporter.reportECommerce(.showProductCardEvent(product: product, screen: screen))
     }
     ```

   - Objective-C

     ```obj-c translate=no
     // Creating a screen object.
     AMAECommerceScreen *screen = [[AMAECommerceScreen alloc] initWithName:@"ProductCardScreen"
                                                        categoryComponents:@[ @"Акции", @"Красная цена" ]
                                                               searchQuery:@"даниссимо кленовый сироп"
                                                                   payload:@{ @"full_screen": @"true" }];
     // Creating an actualPrice object.
     AMAECommerceAmount *actualFiat =
             [[AMAECommerceAmount alloc] initWithUnit:@"USD" value:[NSDecimalNumber decimalNumberWithString:@"4.53"]];
     AMAECommerceAmount *woodActualPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"wood" value:[NSDecimalNumber decimalNumberWithString:@"30570000"]];
     AMAECommerceAmount *ironActualPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"iron" value:[NSDecimalNumber decimalNumberWithString:@"26.89"]];
     AMAECommerceAmount *goldActualPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"gold" value:[NSDecimalNumber decimalNumberWithString:@"5.1"]];
     AMAECommercePrice *actualPrice = [[AMAECommercePrice alloc] initWithFiat:actualFiat
                                                           internalComponents:@[ woodActualPrice, ironActualPrice, goldActualPrice ]];
     // Creating an originalPrice object.
     AMAECommerceAmount *originalFiat =
             [[AMAECommerceAmount alloc] initWithUnit:@"USD" value:[NSDecimalNumber decimalNumberWithString:@"5.78"]];
     AMAECommerceAmount *woodOriginalPrice =
              [[AMAECommerceAmount alloc] initWithUnit:@"wood" value:[NSDecimalNumber decimalNumberWithString:@"30590000"]];
     AMAECommerceAmount *ironOriginalPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"iron" value:[NSDecimalNumber decimalNumberWithString:@"26.92"]];
     AMAECommerceAmount *goldOriginalPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"gold" value:[NSDecimalNumber decimalNumberWithString:@"5.5"]];
     AMAECommercePrice *originalPrice = [[AMAECommercePrice alloc] initWithFiat:originalFiat
                                                             internalComponents:@[ woodOriginalPrice, ironOriginalPrice, goldOriginalPrice ]];
     // Creating a product object.
     AMAECommerceProduct *product = [[AMAECommerceProduct alloc] initWithSKU:@"779213"
                                                                        name:@"Продукт творожный «Даниссимо» 5.9%, 130 г."
                                                          categoryComponents:@[ @"Продукты", @"Молочные продукты", @"Йогурты" ]
                                                                     payload:@{ @"full_screen" : @"true" }
                                                                 actualPrice:actualPrice
                                                               originalPrice:originalPrice
                                                                  promoCodes:@[ @"BT79IYX", @"UT5412EP" ]];
     // Sending an e-commerce event.
     id<AMAAppMetricaReporting> reporter = [AMAAppMetrica reporterForAPIKey:@"Testing API key"];
     [reporter reportECommerce:[AMAECommerce showProductCardEventWithProduct:product screen:screen] onFailure:nil];
     ```

   {% endlist %}

{% endcut %}

{% cut "Просмотр страницы товара" %}

   {% list tabs group=instructions %}

   - Swift

     ```swift translate=no
     // Creating a screen object.
     let screen = ECommerceScreen(
             name: "ProductCardScreen",
             categoryComponents: ["Акции", "Красная цена"],
             searchQuery: "даниссимо кленовый сироп",
             payload: ["full_screen": "true"]
     )
     // Creating an actualPrice object.
     let actualPrice = ECommercePrice(
             fiat: .init(unit: "USD", value: .init(string: "4.53")),
             internalComponents: [
                 .init(unit: "wood", value: .init(string: "30570000")),
                 .init(unit: "iron", value: .init(string: "26.89")),
                 .init(unit: "gold", value: .init(string: "5.1")),
             ]
     )
     // Creating a product object.
     let product = ECommerceProduct(
             sku: "779213",
             name: "Продукт творожный «Даниссимо» 5.9%, 130 г.",
             categoryComponents: ["Продукты", "Молочные продукты", "Йогурты"],
             payload: ["full_screen": "true"],
             actualPrice: actualPrice,
             originalPrice: .init(
                     fiat: .init(unit: "USD", value: .init(string: "5.78")),
                     internalComponents: [
                         .init(unit: "wood", value: .init(string: "30590000")),
                         .init(unit: "iron", value: .init(string: "26.92")),
                         .init(unit: "gold", value: .init(string: "5.5")),
                     ]
             ),
             promoCodes: ["BT79IYX", "UT5412EP"]
     )
     // Creating a referrer object.
     let referrer = ECommerceReferrer(type: "button", identifier: "76890", screen: screen)
     // Sending an e-commerce event.
     if let reporter = AppMetrica.reporter(for: "Testing API key") {
        reporter.reportECommerce(.showProductDetailsEvent(product: product, referrer: referrer))
     }
     ```

   - Objective-C

     ```obj-c translate=no
     // Creating a screen object.
     AMAECommerceScreen *screen = [[AMAECommerceScreen alloc] initWithName:@"ProductCardScreen"
                                                        categoryComponents:@[ @"Акции", @"Красная цена" ]
                                                               searchQuery:@"даниссимо кленовый сироп"
                                                                   payload:@{ @"full_screen": @"true" }];

     // Creating an actualPrice object.
     AMAECommerceAmount *actualFiat =
             [[AMAECommerceAmount alloc] initWithUnit:@"USD" value:[NSDecimalNumber decimalNumberWithString:@"4.53"]];
     AMAECommerceAmount *woodActualPrice =
              [[AMAECommerceAmount alloc] initWithUnit:@"wood" value:[NSDecimalNumber decimalNumberWithString:@"30570000"]];
     AMAECommerceAmount *ironActualPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"iron" value:[NSDecimalNumber decimalNumberWithString:@"26.89"]];
     AMAECommerceAmount *goldActualPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"gold" value:[NSDecimalNumber decimalNumberWithString:@"5.1"]];
     AMAECommercePrice *actualPrice = [[AMAECommercePrice alloc] initWithFiat:actualFiat
                                                           internalComponents:@[ woodActualPrice, ironActualPrice, goldActualPrice ]];
     // Creating an originalPrice object.
     AMAECommerceAmount *originalFiat =
             [[AMAECommerceAmount alloc] initWithUnit:@"USD" value:[NSDecimalNumber decimalNumberWithString:@"5.78"]];
     AMAECommerceAmount *woodOriginalPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"wood" value:[NSDecimalNumber decimalNumberWithString:@"30590000"]];
     AMAECommerceAmount *ironOriginalPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"iron" value:[NSDecimalNumber decimalNumberWithString:@"26.92"]];
     AMAECommerceAmount *goldOriginalPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"gold" value:[NSDecimalNumber decimalNumberWithString:@"5.5"]];
     AMAECommercePrice *originalPrice = [[AMAECommercePrice alloc] initWithFiat:originalFiat
                                                             internalComponents:@[ woodOriginalPrice, ironOriginalPrice, goldOriginalPrice ]];
     // Creating a product object.
     AMAECommerceProduct *product = [[AMAECommerceProduct alloc] initWithSKU:@"779213"
                                                                        name:@"Продукт творожный «Даниссимо» 5.9%, 130 г."
                                                           categoryComponents:@[ @"Продукты", @"Молочные продукты", @"Йогурты" ]
                                                                    payload:@{ @"full_screen" : @"true" }
                                                                 actualPrice:actualPrice
                                                               originalPrice:originalPrice
                                                                  promoCodes:@[ @"BT79IYX", @"UT5412EP" ]];
     // Creating a referrer object.
     AMAECommerceReferrer *referrer = [[AMAECommerceReferrer alloc] initWithType:@"button"
                                                                      identifier:@"76890"
                                                                          screen:screen];
     // Sending an e-commerce event.
     id<AMAAppMetricaReporting> reporter = [AMAAppMetrica reporterForAPIKey:@"Testing API key"];
     [reporter reportECommerce:[AMAECommerce showProductDetailsEventWithProduct:product referrer:referrer] onFailure:nil];
     ```

   {% endlist %}

{% endcut %}

{% cut "Добавление или удаление товара из корзины" %}

   {% list tabs group=instructions %}

   - Swift

     ```swift translate=no
     // Creating a screen object.
     let screen = ECommerceScreen(
             name: "ProductCardScreen",
             categoryComponents: ["Акции", "Красная цена"],
             searchQuery: "даниссимо кленовый сироп",
             payload: ["full_screen": "true"]
     )
     // Creating an actualPrice object.
     let actualPrice = ECommercePrice(
             fiat: .init(unit: "USD", value: .init(string: "4.53")),
             internalComponents: [
                 .init(unit: "wood", value: .init(string: "30570000")),
                 .init(unit: "iron", value: .init(string: "26.89")),
                 .init(unit: "gold", value: .init(string: "5.1")),
             ]
     )
     // Creating a product object.
     let product = ECommerceProduct(
             sku: "779213",
             name: "Продукт творожный «Даниссимо» 5.9%, 130 г.",
             categoryComponents: ["Продукты", "Молочные продукты", "Йогурты"],
             payload: ["full_screen": "true"],
             actualPrice: actualPrice,
             originalPrice: .init(
                     fiat: .init(unit: "USD", value: .init(string: "5.78")),
                     internalComponents: [
                         .init(unit: "wood", value: .init(string: "30590000")),
                         .init(unit: "iron", value: .init(string: "26.92")),
                         .init(unit: "gold", value: .init(string: "5.5")),
                     ]
             ),
             promoCodes: ["BT79IYX", "UT5412EP"]
     )
     // Creating a referrer object.
     let referrer = ECommerceReferrer(type: "button", identifier: "76890", screen: screen)
     // Creating a cartItem object.
     let addedItems = ECommerceCartItem(
             product: product,
             quantity: .init(string: "1"),
             revenue: actualPrice,
             referrer: referrer
     )
     // Sending an e-commerce event.
     if let reporter = AppMetrica.reporter(for: "Testing API key") {
        reporter.reportECommerce(.addCartItemEvent(cartItem: addedItems))
        // Or:
        reporter.reportECommerce(.removeCartItemEvent(cartItem: addedItems))
     }
     ```

   - Objective-C

     ```obj-c translate=no
     // Creating a screen object.
     AMAECommerceScreen *screen = [[AMAECommerceScreen alloc] initWithName:@"ProductCardScreen"
                                                        categoryComponents:@[ @"Акции", @"Красная цена" ]
                                                               searchQuery:@"даниссимо кленовый сироп"
                                                                   payload:@{ @"full_screen": @"true" }];
     // Creating an actualPrice object.
     AMAECommerceAmount *actualFiat =
             [[AMAECommerceAmount alloc] initWithUnit:@"USD" value:[NSDecimalNumber decimalNumberWithString:@"4.53"]];
     AMAECommerceAmount *woodActualPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"wood" value:[NSDecimalNumber decimalNumberWithString:@"30570000"]];
     AMAECommerceAmount *ironActualPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"iron" value:[NSDecimalNumber decimalNumberWithString:@"26.89"]];
     AMAECommerceAmount *goldActualPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"gold" value:[NSDecimalNumber decimalNumberWithString:@"5.1"]];
     AMAECommercePrice *actualPrice = [[AMAECommercePrice alloc] initWithFiat:actualFiat
                                                           internalComponents:@[ woodActualPrice, ironActualPrice, goldActualPrice ]];
     // Creating an originalPrice object.
     AMAECommerceAmount *originalFiat =
             [[AMAECommerceAmount alloc] initWithUnit:@"USD" value:[NSDecimalNumber decimalNumberWithString:@"5.78"]];
     AMAECommerceAmount *woodOriginalPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"wood" value:[NSDecimalNumber decimalNumberWithString:@"30590000"]];
     AMAECommerceAmount *ironOriginalPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"iron" value:[NSDecimalNumber decimalNumberWithString:@"26.92"]];
     AMAECommerceAmount *goldOriginalPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"gold" value:[NSDecimalNumber decimalNumberWithString:@"5.5"]];
     AMAECommercePrice *originalPrice = [[AMAECommercePrice alloc] initWithFiat:originalFiat
                                                             internalComponents:@[ woodOriginalPrice, ironOriginalPrice, goldOriginalPrice ]];
     // Creating a product object.
     AMAECommerceProduct *product = [[AMAECommerceProduct alloc] initWithSKU:@"779213"
                                                                        name:@"Продукт творожный «Даниссимо» 5.9%, 130 г."
                                                          categoryComponents:@[ @"Продукты", @"Молочные продукты", @"Йогурты" ]
                                                                     payload:@{ @"full_screen" : @"true" }
                                                                 actualPrice:actualPrice
                                                               originalPrice:originalPrice
                                                                  promoCodes:@[ @"BT79IYX", @"UT5412EP" ]];
     // Creating a referrer object.
     AMAECommerceReferrer *referrer = [[AMAECommerceReferrer alloc] initWithType:@"button"
                                                                      identifier:@"76890"
                                                                          screen:screen];
     // Creating a cartItem object.
     NSDecimalNumber *quantity = [NSDecimalNumber decimalNumberWithString:@"1"];
     AMAECommerceCartItem *addedItems = [[AMAECommerceCartItem alloc] initWithProduct:product
                                                                             quantity:quantity
                                                                              revenue:actualPrice
                                                                             referrer:referrer];
     // Sending an e-commerce event.
     id<AMAAppMetricaReporting> reporter = [AMAAppMetrica reporterForAPIKey:@"Testing API key"];
     [reporter reportECommerce:[AMAECommerce addCartItemEventWithItem:addedItems] onFailure:nil];
     // Or:
     [reporter reportECommerce:[AMAECommerce removeCartItemEventWithItem:addedItems] onFailure:nil];
     ```

   {% endlist %}

{% endcut %}

{% cut "Начало оформления и завершение покупки" %}

   {% list tabs group=instructions %}

   - Swift

     ```swift translate=no
     // Creating a screen object.
     let screen = ECommerceScreen(
             name: "ProductCardScreen",
             categoryComponents: ["Акции", "Красная цена"],
             searchQuery: "даниссимо кленовый сироп",
             payload: ["full_screen": "true"]
     )
     // Creating an actualPrice object.
     let actualPrice = ECommercePrice(
             fiat: .init(unit: "USD", value: .init(string: "4.53")),
             internalComponents: [
                 .init(unit: "wood", value: .init(string: "30570000")),
                 .init(unit: "iron", value: .init(string: "26.89")),
                 .init(unit: "gold", value: .init(string: "5.1")),
             ]
     )
     // Creating a product object.
     let product = ECommerceProduct(
             sku: "779213",
             name: "Продукт творожный «Даниссимо» 5.9%, 130 г.",
             categoryComponents: ["Продукты", "Молочные продукты", "Йогурты"],
             payload: ["full_screen": "true"],
             actualPrice: actualPrice,
             originalPrice: .init(
                     fiat: .init(unit: "USD", value: .init(string: "5.78")),
                     internalComponents: [
                         .init(unit: "wood", value: .init(string: "30590000")),
                         .init(unit: "iron", value: .init(string: "26.92")),
                         .init(unit: "gold", value: .init(string: "5.5")),
                     ]
             ),
             promoCodes: ["BT79IYX", "UT5412EP"]
     )
     // Creating a referrer object.
     let referrer = ECommerceReferrer(type: "button", identifier: "76890", screen: screen)
     // Creating a cartItem object.
     let addedItems = ECommerceCartItem(
             product: product,
             quantity: .init(string: "1"),
             revenue: actualPrice,
             referrer: referrer
     )
     // Creating an order object.
     let order = ECommerceOrder(
             identifier: "88528768",
             cartItems: [addedItems],
             payload: ["black_friday": "true"]
     )
     // Sending an e-commerce event.
     if let reporter = AppMetrica.reporter(for: "Testing API key") {
        reporter.reportECommerce(.beginCheckoutEvent(order:order))
        reporter.reportECommerce(.purchaseEvent(order: order))
     }
     ```

   - Objective-C

     ```obj-c translate=no
     // Creating a screen object.
     AMAECommerceScreen *screen = [[AMAECommerceScreen alloc] initWithName:@"ProductCardScreen"
                                                        categoryComponents:@[ @"Акции", @"Красная цена" ]
                                                               searchQuery:@"даниссимо кленовый сироп"
                                                                   payload:@{ @"full_screen": @"true" }];
     // Creating an actualPrice object.
     AMAECommerceAmount *actualFiat =
             [[AMAECommerceAmount alloc] initWithUnit:@"USD" value:[NSDecimalNumber decimalNumberWithString:@"4.53"]];
     AMAECommerceAmount *woodActualPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"wood" value:[NSDecimalNumber decimalNumberWithString:@"30570000"]];
     AMAECommerceAmount *ironActualPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"iron" value:[NSDecimalNumber decimalNumberWithString:@"26.89"]];
     AMAECommerceAmount *goldActualPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"gold" value:[NSDecimalNumber decimalNumberWithString:@"5.1"]];
     AMAECommercePrice *actualPrice = [[AMAECommercePrice alloc] initWithFiat:actualFiat
                                                           internalComponents:@[ woodActualPrice, ironActualPrice, goldActualPrice ]];
     // Creating an originalPrice object.
     AMAECommerceAmount *originalFiat =
             [[AMAECommerceAmount alloc] initWithUnit:@"USD" value:[NSDecimalNumber decimalNumberWithString:@"5.78"]];
     AMAECommerceAmount *woodOriginalPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"wood" value:[NSDecimalNumber decimalNumberWithString:@"30590000"]];
     AMAECommerceAmount *ironOriginalPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"iron" value:[NSDecimalNumber decimalNumberWithString:@"26.92"]];
     AMAECommerceAmount *goldOriginalPrice =
             [[AMAECommerceAmount alloc] initWithUnit:@"gold" value:[NSDecimalNumber decimalNumberWithString:@"5.5"]];
     AMAECommercePrice *originalPrice = [[AMAECommercePrice alloc] initWithFiat:originalFiat
                                                             internalComponents:@[ woodOriginalPrice, ironOriginalPrice, goldOriginalPrice ]];
     // Creating a product object.
     AMAECommerceProduct *product = [[AMAECommerceProduct alloc] initWithSKU:@"779213"
                                                                        name:@"Продукт творожный «Даниссимо» 5.9%, 130 г."
                                                          categoryComponents:@[ @"Продукты", @"Молочные продукты", @"Йогурты" ]
                                                                     payload:@{ @"full_screen" : @"true" }
                                                                 actualPrice:actualPrice
                                                               originalPrice:originalPrice
                                                                  promoCodes:@[ @"BT79IYX", @"UT5412EP" ]];
     // Creating a referrer object.
     AMAECommerceReferrer *referrer = [[AMAECommerceReferrer alloc] initWithType:@"button"
                                                                      identifier:@"76890"
                                                                          screen:screen];
     // Creating a cartItem object.
     NSDecimalNumber *quantity = [NSDecimalNumber decimalNumberWithString:@"1"];
     AMAECommerceCartItem *addedItems = [[AMAECommerceCartItem alloc] initWithProduct:product
                                                                             quantity:quantity
                                                                              revenue:actualPrice
                                                                             referrer:referrer];
     // Creating an order object.
     AMAECommerceOrder *order = [[AMAECommerceOrder alloc] initWithIdentifier:@"88528768"
                                                                    cartItems:@[ addedItems ]
                                                                      payload:@{ @"black_friday" : @"true"}];
     // Sending an e-commerce event.
     id<AMAAppMetricaReporting> reporter = [AMAAppMetrica reporterForAPIKey:@"Testing API key"];
     [reporter reportECommerce:[AMAECommerce beginCheckoutEventWithOrder:order] onFailure:nil];
     [reporter reportECommerce:[AMAECommerce purchaseEventWithOrder:order] onFailure:nil];
     ```

   {% endlist %}

{% endcut %}

### Шаг 2. Проверьте отчет тестового приложения {#send-ecommerce-test-app}

Совершите тестовые покупки в приложении. Через некоторое время в интерфейсе AppMetrica проверьте отчет «Ecommerce». Убедитесь, что ECommerce-события отображаются в отчете.

Подробнее об отчете в разделе [Ecommerce](../../../mobile-reports/ecommerce-report.md).

### Шаг 3. Настройте отправку на основной API key {#send-ecommerce-key}

После успешного тестирования настройте отправку ECommerce-событий на основной API key.

{% list tabs group=instructions %}

- Swift

  Чтобы отправить объект `ECommerce` на основной API key, используйте метода `reportECommerce(_:onFailure:)` класса `AppMetrica`.

  ```swift translate=no
  // ...
  // Sending an e-commerce event.
  AppMetrica.reportECommerce(.showScreenEvent(screen: screen))
  ```

- Objective-C

  Чтобы отправить объект `AMAECommerce` на основной API key, используйте метода `+reportECommerce:onFailure:` класса `AMAAppMetrica`.

  ```obj-c translate=no
  // ...
  // Sending an e-commerce event.
  [AMAAppMetrica reportECommerce:[AMAECommerce showScreenEventWithScreen:screen] onFailure:nil];
  ```

{% endlist %}

## Отправка Revenue {#send-revenue}

AppMetrica поддерживает валидацию покупок, которые реализованы с помощью библиотеки [StoreKit](https://developer.apple.com/documentation/storekit). Валидация позволяет фильтровать покупки, которые совершаются из взломанных приложений. Если валидация включена и покупка не проходит валидацию, она не отображается в отчетах.

{% note info %}

Чтобы покупки валидировались, включите валидацию в настройках. 

{% endnote %}

### Шаг 1. Протестируйте отправку Revenue {#send-revenue-test}

В AppMetrica нет возможности сегментировать Revenue на «тестовые» и «не тестовые». Если для отладки покупок вы используете основной API key, то тестовые покупки будут попадать в общую статистику. Поэтому, чтобы отладить отправку Revenue, используйте отправку статистики на дополнительный API key с помощью репортера.

Ниже описаны этапы отправки Revenue на дополнительный API key:

{% cut "С валидацией" %}

Чтобы покупки на iOS валидировались, в собственной реализации завершения транзакции настройте отправку поля `transactionID` и `receiptData`:

{% list tabs group=instructions %}

- Swift

  1. Инициализируйте объект `MutableRevenueInfo`.
  2. Для валидации покупки укажите `transactionID` и `receiptData`. Их необходимо получить до вызова `SKPaymentQueue.default().finishTransaction(transaction)`.
  3. Отправьте объект `MutableRevenueInfo` на тестовый API key с помощью репортера `AppMetricaReporting`. Подробнее о работе репортеров в разделе [Отправка статистики на дополнительный API key](#reporter).

  ```swift translate=no
   func completeTransaction(_ transaction: SKPaymentTransaction) {
       // ...
       let price = NSDecimalNumber(string: "2100.5")
       // Initializing the Revenue instance.
       let revenueInfo = MutableRevenueInfo(priceDecimal: price, currency: "BYN")
       revenueInfo.productID = "TV soundbar"
       revenueInfo.quantity = 2
       revenueInfo.payload = ["source": "AppStore"]
       // Set purchase information for validation.
       if let url = Bundle.main.appStoreReceiptURL, let data = try? Data(contentsOf: url), let transactionID = transaction.transactionIdentifier {
           revenueInfo.transactionID = transactionID
           revenueInfo.receiptData = data
       }
       // Sending the Revenue instance using reporter.
       guard let reporter = AppMetrica.reporter(for: "Testing API key") else {
          print("Failed to create AppMetrica reporter")
          return
       }
       reporter.reportRevenue(revenueInfo, onFailure: { (error) in
           print("Revenue error: \(error.localizedDescription)")
       })
       // Remove the transaction from the payment queue.
       SKPaymentQueue.default().finishTransaction(transaction)
  }
  ```

- Objective-C

  1. Инициализируйте объект `AMAMutableRevenueInfo`.
  2. Для валидации покупки укажите `transactionID` и `receiptData`. Их необходимо получить до вызова `[[SKPaymentQueue defaultQueue] finishTransaction:transaction]`.
  3. Отправьте объект `AMAMutableRevenueInfo` на тестовый API key с помощью репортера `AMAAppMetricaReporting`. Подробнее о работе репортеров в разделе [Отправка статистики на дополнительный API key](#reporter).

  ```obj-c translate=no
   - (void)completeTransaction:(SKPaymentTransaction *)transaction
   {
       // ...
       NSDecimalNumber *price = [NSDecimalNumber decimalNumberWithString:@"2100.5"];
       // Initializing the Revenue instance.
       AMAMutableRevenueInfo *revenueInfo = [[AMAMutableRevenueInfo alloc] initWithPriceDecimal:price currency:@"BYN"];
       revenueInfo.productID = @"TV soundbar";
       revenueInfo.quantity = 2;
       revenueInfo.payload = @{ @"source": @"AppStore" };
       // Set purchase information for validation.
       revenueInfo.transactionID = transaction.transactionIdentifier;
       revenueInfo.receiptData = [NSData dataWithContentsOfURL:[[NSBundle mainBundle] appStoreReceiptURL]];
       // Sending the Revenue instance using reporter.
       id<AMAAppMetricaReporting> reporter = [AMAAppMetrica reporterForAPIKey:@"Testing API key"];
       [reporter reportRevenue:[revenueInfo copy] onFailure:^(NSError *error) {
           NSLog(@"Revenue error: %@", error);
       }];
       // Remove the transaction from the payment queue.
       [[SKPaymentQueue defaultQueue] finishTransaction:transaction];
   }
  ```

{% endlist %}

{% endcut %}

{% cut "Без валидации" %}

Чтобы отправить информацию о покупке без валидации:

{% list tabs group=instructions %}

- Swift

  1. Инициализируйте объект `MutableRevenueInfo`.
  2. (Опционально) Чтобы группировать покупки по `OrderID`, укажите его в свойстве `payload`.
  
     {% note info %}
  
     Если идентификатор `OrderID` не указан, AppMetrica генерирует идентификатор автоматически.
  
     {% endnote %}
  
  3. Отправьте объект `MutableRevenueInfo` на тестовый API key с помощью репортера `AppMetricaReporting`. Подробнее о работе репортеров в разделе [Отправка статистики на дополнительный API key](#reporter).

  ```swift translate=no
   let price = NSDecimalNumber(string: "2100.5")
   // Initializing the Revenue instance.
   let revenueInfo = MutableRevenueInfo(priceDecimal: price, currency: "BYN")
   revenueInfo.productID = "TV soundbar"
   revenueInfo.quantity = 2
   // To group purchases, set the OrderID parameter in the payload property.
   revenueInfo.payload = ["OrderID": "Identifier", "source": "AppStore"]
   // Sending the Revenue instance using reporter.
   if let reporter = AppMetrica.reporter(for: "Testing API key") {
      reporter.reportRevenue(revenueInfo, onFailure: { (error) in
          print("Revenue error: \(error.localizedDescription)")
      })
   }
   ```

- Objective-C

  1. Инициализируйте объект `AMAMutableRevenueInfo`.
  2. (Опционально) Чтобы группировать покупки по `OrderID`, укажите его в свойстве `payload`.

     {% note info %}

     Если идентификатор `OrderID` не указан, AppMetrica генерирует идентификатор автоматически.

     {% endnote %}

  3. Отправьте объект `AMAMutableRevenueInfo` на тестовый API key с помощью репортера `AMAAppMetricaReporting`. Подробнее о работе репортеров в разделе [Отправка статистики на дополнительный API key](#reporter).

  ```obj-c translate=no
   NSDecimalNumber *price = [NSDecimalNumber decimalNumberWithString:@"2100.5"];
   // Initializing the Revenue instance.
   AMAMutableRevenueInfo *revenueInfo = [[AMAMutableRevenueInfo alloc] initWithPriceDecimal:price currency:@"BYN"];
   revenueInfo.productID = @"TV soundbar";
   revenueInfo.quantity = 2;
   // Setting the OrderID parameter in the payload property to group purchases
   revenueInfo.payload = @{ @"OrderID": @"Identifier", @"source": @"AppStore" };
   // Sending the Revenue instance using reporter.
   id<AMAAppMetricaReporting> reporter = [AMAAppMetrica reporterForAPIKey:@"Testing API key"];
   [reporter reportRevenue:[revenueInfo copy] onFailure:^(NSError *error) {
       NSLog(@"Revenue error: %@", error);
   }];
  ```

{% endlist %}

{% endcut %}

### Шаг 2. Настройте отправку Revenue на основной API key {#send-revenue-key}

После успешного тестирования настройте отправку Revenue на основной API key.

{% list tabs group=instructions %}

  - Swift

    Чтобы отправить объект `MutableRevenueInfo` на основной API key, используйте метод `reportRevenue(_:onFailure:)` класса `AppMetrica`.

    ```swift translate=no
    // ...
    // Sending the Revenue instance.
    AppMetrica.reportRevenue(revenueInfo, onFailure: { (error) in
        print("Revenue error: \(error)")
    })
    ```

  - Objective-C

    Чтобы отправить объект `AMAMutableRevenueInfo` на основной API key, используйте метод `+reportRevenue:onFailure:` класса `AMAAppMetrica`.

    ```obj-c translate=no
    // ...
    // Sending the Revenue instance.
    [AMAAppMetrica reportRevenue:[revenueInfo copy] onFailure:^(NSError *error) {
       NSLog(@"Revenue error: %@", error);
    }];
    ```

{% endlist %}

## Отправка Ad Revenue {#send-adrevenue}

### Шаг 1. Убедитесь, что SDK активирован {#send-adrevenue-activate}

Пример активации:

{% list tabs group=instructions %}

- Swift

  ```swift translate=no
  let configuration = AppMetricaConfiguration.init(apiKey: "API key")
  AppMetrica.activate(with: configuration!)
  ```
  
- Objective-C

  ```objectivec translate=no
  AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithApiKey:@"API_key"];
  [AMAAppMetrica activateWithConfiguration:configuration];
  ```

{% endlist %}

### Шаг 2. Настройте отправку Ad Revenue {#send-adrevenue-send}

{% list tabs %}

- AppLovin MAX

  1. Импортируйте необходимые модули:

     {% list tabs group=instructions %}

     - Swift

       ```swift translate=no
       import AppMetricaCore
       import AppLovinSDK
       ```

     - Objective-C

       ```objectivec translate=no
       #import <AppMetricaCore/AppMetricaCore.h>
       #import <AppLovinSDK/AppLovinSDK.h>
       ```

     {% endlist %}

  2. Добавьте вспомогательное расширение для `MAAdFormat`:
  
     {% list tabs group=instructions %}

     - Swift

       ```swift translate=no
       extension MAAdFormat {
           var appMetricaAdType: AdType {
               switch self {
               case .banner: return .banner
               case .interstitial: return .interstitial
               case .rewarded: return .rewarded
               case .native: return .native
               case .mrec: return .mrec
               case .appOpen: return .appOpen
               default: return .other
               }
           }
       }
       ```

     - Objective-C

       ```objectivec translate=no
       @implementation MAAdFormat (AppMetricaAdType)

       - (AMAAdType)appMetricaAdType {
           switch (self) {
               case MAAdFormat.banner:
                   return AMAAdTypeBanner;
               case MAAdFormat.interstitial:
                   return AMAAdTypeInterstitial;
               case MAAdFormat.rewarded:
                   return AMAAdTypeRewarded;
               case MAAdFormat.native:
                   return AMAAdTypeNative;
               case MAAdFormat.mrec:
                   return AMAAdTypeMrec;
               case MAAdFormat.appOpen:
                   return AMAAdTypeAppOpen;
               default:
                   return AdTypeOther;
          }
       }

       @end
       ```

     {% endlist %}

  3. Реализуйте `MAAdRevenueDelegate`:

     {% list tabs group=instructions %}

     - Swift

       ```swift translate=no
       class AdRevenueReporter: NSObject, MAAdRevenueDelegate {
           func didPayRevenue(for ad: MAAd) {
               // Create a MutableAdRevenueInfo object
               let adRevenueInfo = MutableAdRevenueInfo(adRevenue: NSDecimalNumber(value: ad.revenue), currency: "USD")

               // Set additional properties
               adRevenueInfo.adType = ad.format.appMetricaAdType
               adRevenueInfo.adNetwork = ad.networkName
               adRevenueInfo.adUnitID = ad.adUnitIdentifier
               adRevenueInfo.adPlacementName = ad.placement
               adRevenueInfo.precision = ad.revenuePrecision

               // Additional information can be added to payload if needed
               adRevenueInfo.payload = [
                   "adType": ad.format.label,
                   "countryCode": ALSdk.shared().configuration.countryCode,
                   "networkPlacement": ad.networkPlacement,
                   "original_ad_type": ad.format.label,
               ]

               // Report the ad revenue to AppMetrica
               AppMetrica.reportAdRevenue(adRevenueInfo)
           }
       }

       ```

     - Objective-C

       ```objectivec translate=no
       #import <AppMetricaCore/AppMetricaCore.h>
       #import <AppLovinSDK/AppLovinSDK.h>
       ```

     {% endlist %}

- Digital Turbine (Fyber)
  
  1. Импортируйте необходимые модули:

     {% list tabs group=instructions %}

     - Swift

       ```swift translate=no
       import AppMetricaCore
       import FairBidSDK
       ```

     - Objective-C

       ```objectivec translate=no
       #import <AppMetricaCore/AppMetricaCore.h>
       #import <FairBidSDK/FairBidSDK.h>
       ```

     {% endlist %}
  
  2. Создайте функцию для отправки Ad Revenue в AppMetrica:

     {% list tabs group=instructions %}

     - Swift

       ```swift translate=no
       func reportToAppMetrica(_ impressionData: FYBImpressionData, placementId: String, adType: AdType) {
           let revenue = impressionData.netPayout.map { NSDecimalNumber(decimal: $0.decimalValue) } ?? .zero
           let currency = impressionData.currency ?? "USD"

           let adRevenueInfo = MutableAdRevenueInfo(adRevenue: revenue, currency: currency)
           adRevenueInfo.adType = adType
           adRevenueInfo.adNetwork = impressionData.demandSource
           adRevenueInfo.adUnitID = impressionData.creativeId
           adRevenueInfo.precision = impressionData.priceAccuracy.appMetricaPrecision
           adRevenueInfo.payload = [
             "original_ad_type": String(impressionData.placementType.rawValue),
           ]
       
           AppMetrica.reportAdRevenue(adRevenueInfo) { error in
               print("Failed to report ad revenue to AppMetrica: \(error)")
           }
       }
       ```

     - Objective-C

       ```objectivec translate=no
       void reportToAppMetrica(FYBImpressionData *impressionData, NSString *placementId, AdType adType) {
           NSDecimalNumber *revenue = impressionData.netPayout ? [[NSDecimalNumber alloc] initWithDecimal:impressionData.netPayout.decimalValue] : [NSDecimalNumber zero];
           NSString *currency = impressionData.currency ? impressionData.currency : @"USD";

           MutableAdRevenueInfo *adRevenueInfo = [[MutableAdRevenueInfo alloc] initWithAdRevenue:revenue currency:currency];
           adRevenueInfo.adType = adType;
           adRevenueInfo.adNetwork = impressionData.demandSource;
           adRevenueInfo.adUnitID = impressionData.creativeId;
           adRevenueInfo.precision = [impressionData.priceAccuracy appMetricaPrecision];
           adRevenueInfo.payload = @{
               @"original_ad_type": @(impressionData.placementType)
           };
       
           [AppMetrica reportAdRevenue:adRevenueInfo completion:^(NSError *error) {
               if (error) {
                   NSLog(@"Failed to report ad revenue to AppMetrica: %@", error);
               }
           }];
       }
       ```

     {% endlist %}
  
  3. Добавьте расширение для преобразования формата цен Fyber в формат AppMetrica:

     {% list tabs group=instructions %}

     - Swift

       ```swift translate=no
       extension FYBImpressionDataPriceAccuracy {
           var appMetricaPrecision: String {
               switch self {
               case .undisclosed: return "undisclosed"
               case .predicted: return "predicted"
               case .programmatic: return "programmatic"
               @unknown default: return "unknown"
               }
           }
       }
       ```

     - Objective-C

       ```objectivec translate=no
       @implementation NSNumber (FYBImpressionDataPriceAccuracyAppMetricaPrecision)

       + (NSString *)appMetricaPrecisionForFYBImpressionDataPriceAccuracy:(FYBImpressionDataPriceAccuracy)accuracy {
           switch (accuracy) {
               case FYBImpressionDataPriceAccuracyUndisclosed:
                   return @"undisclosed";
               case FYBImpressionDataPriceAccuracyPredicted:
                   return @"predicted";
               case FYBImpressionDataPriceAccuracyProgrammatic:
                   return @"programmatic";
               default:
                   return @"unknown";
           }
       }

       @end
       ```

     {% endlist %}
  
  4. Создайте функцию для отчета о показах OfferWall в AppMetrica:

     {% list tabs group=instructions %}

     - Swift

       ```swift translate=no
       func reportOfferWallShowToAppMetrica(placementId: String) {
           let adRevenueInfo = MutableAdRevenueInfo(adRevenue: NSDecimalNumber.zero, currency: "USD")
           adRevenueInfo.adType = .other
           adRevenueInfo.adUnitID = placementId
           adRevenueInfo.payload = [
               "original_ad_type": "offerWall"
           ]

           AppMetrica.reportAdRevenue(adRevenueInfo) { error in
               print("Failed to report OfferWall show to AppMetrica: \(error)")
           }
       }
       ```

     - Objective-C

       ```objectivec translate=no
       - (void)reportOfferWallShowToAppMetricaWithPlacementId:(NSString *)placementId {
           AMAMutableAdRevenueInfo *adRevenueInfo = [[AMAMutableAdRevenueInfo alloc] initWithAdRevenue:[NSDecimalNumber zero] currency:@"USD"];

           adRevenueInfo.adType = AMAAdTypeOther;
           adRevenueInfo.adUnitID = placementId;
           adRevenueInfo.payload = @{
               @"original_ad_type": @"offerWall"
           };

           [AMAYandexMetrica reportAdRevenueWithInfo:adRevenueInfo completionHandler:^(NSError * _Nullable error) {
               if (error) {
                   NSLog(@"Failed to report OfferWall show to AppMetrica: %@", error);
               }
           }];
       }
       ```

     {% endlist %}

  5. Создайте делегаты для каждого формата рекламы и соответствующие методы к ним:

     {% list tabs group=instructions %}

     - Swift

       ```swift translate=no
       class YourBannerDelegate: NSObject, FYBBannerDelegate {
           func bannerDidShow(_ banner: FYBBannerAdView, impressionData: FYBImpressionData) {
               reportToAppMetrica(impressionData, placementId: banner.options.placementId, adType: .banner)
           }
           // Implement other delegate methods as needed
       }

       class YourInterstitialDelegate: NSObject, FYBInterstitialDelegate {
           func interstitialDidShow(_ placementId: String, impressionData: FYBImpressionData) {
               reportToAppMetrica(impressionData, placementId: placementId, adType: .interstitial)
           }
           // Implement other delegate methods as needed
       }

       class YourRewardedDelegate: NSObject, FYBRewardedDelegate {
           func rewardedDidShow(_ placementId: String, impressionData: FYBImpressionData) {
               reportToAppMetrica(impressionData, placementId: placementId, adType: .rewarded)
           }
           // Implement other delegate methods as needed
       }

       class YourOfferWallDelegate: NSObject, OfferWallDelegate {
           func didShow(_ placementId: String?) {
               reportOfferWallShowToAppMetrica(placementId: placementId ?? "unknown")
           }
           // Implement other delegate methods as needed
       }
       ```

     - Objective-C

       ```objectivec translate=no
       // YourBannerDelegate
       @interface YourBannerDelegate : NSObject <FYBBannerDelegate>
       @end

       @implementation YourBannerDelegate
       - (void)bannerDidShow:(FYBBannerAdView *)banner impressionData:(FYBImpressionData *)impressionData {
           [self reportToAppMetricaWithImpressionData:impressionData placementId:banner.options.placementId adType:AdTypeBanner];
       }
       // Implement other delegate methods as needed
       @end

       // YourInterstitialDelegate
       @interface YourInterstitialDelegate : NSObject <FYBInterstitialDelegate>
       @end

       @implementation YourInterstitialDelegate
       - (void)interstitialDidShowWithPlacementId:(NSString *)placementId impressionData:(FYBImpressionData *)impressionData {
           [self reportToAppMetricaWithImpressionData:impressionData placementId:placementId adType:AdTypeInterstitial];
       }
       // Implement other delegate methods as needed
       @end

       // YourRewardedDelegate
       @interface YourRewardedDelegate : NSObject <FYBRewardedDelegate>
       @end

       @implementation YourRewardedDelegate
       - (void)rewardedDidShowWithPlacementId:(NSString *)placementId impressionData:(FYBImpressionData *)impressionData {
           [self reportToAppMetricaWithImpressionData:impressionData placementId:placementId adType:AdTypeRewarded];
       }
       // Implement other delegate methods as needed
       @end

       // YourOfferWallDelegate
       @interface YourOfferWallDelegate : NSObject <OfferWallDelegate>
       @end

       @implementation YourOfferWallDelegate
       - (void)didShowWithPlacementId:(NSString *)placementId {
           // Assuming reportOfferWallShowToAppMetrica is implemented elsewhere
           [self reportOfferWallShowToAppMetricaWithPlacementId:placementId ? placementId : @"unknown"];
       }
       // Implement other delegate methods as needed
       @end
       ```

     {% endlist %}

- Google AdMob

  1. Импортируйте необходимые модули:

     {% list tabs group=instructions %}

     - Swift

       ```swift translate=no
       import AppMetricaCore
       import GoogleMobileAds
       ```

     - Objective-C

       ```objectivec translate=no
       #import <AppMetricaCore/AppMetricaCore.h>
       #import <GoogleMobileAds/GoogleMobileAds.h>
       ```

     {% endlist %}
  
  2. Добавьте вспомогательное расширение для `GADAdValuePrecision`:
  
     {% list tabs group=instructions %}

     - Swift

       ```swift translate=no
       extension GADAdValuePrecision: CustomStringConvertible {
           public var description: String {
               switch self {
               case .precise: return "precise"
               case .estimated: return "estimated"
               case .publisherProvided: return "publisher_defined"
               case .unknown: fallthrough
               @unknown default: return "unknown"
               }
           }
       }
       
       enum GAAdType: String {
           case banner = "bannerAd"
           case interstitial = "interstitialAd"
           case rewarded = "rewardedAd"
           case native = "nativeAd"
           case appOpen = "appOpenAd"
       }
       
       ```

     - Objective-C

       ```objectivec translate=no
       @interface GADAdValuePrecisionHelper : NSObject

       + (NSString *)stringFromAdValuePrecision:(GADAdValuePrecision)precision;

       @end

       @implementation GADAdValuePrecisionHelper

       + (NSString *)stringFromAdValuePrecision:(GADAdValuePrecision)precision {
           switch (precision) {
               case GADAdValuePrecisionPrecise:
                   return @"precise";
               case GADAdValuePrecisionEstimated:
                   return @"estimated";
               case GADAdValuePrecisionPublisherProvided:
                   return @"publisher_defined";
               case GADAdValuePrecisionUnknown:
               default:
                   return @"unknown";
           }
       }

       @end
       
       typedef NSString *GAAdType NS_TYPED_ENUM;
       
       GAAdType GAAdTypeBanner = @"bannerAd";
       GAAdType GAAdTypeInterstitial = @"interstitialAd";
       GAAdType GAAdTypeRewarded = @"rewardedAd";
       GAAdType GAAdTypeNative = @"nativeAd";
       GAAdType GAAdTypeAppOpen = @"appOpen";
       ```

     {% endlist %}

  3. Реализуйте логику загрузки рекламы и создания отчетов о показах:

     {% list tabs group=instructions %}

     - Swift

       ```swift translate=no
       class ViewController: UIViewController, GADFullScreenContentDelegate {
           var rewardedAd: GADRewardedAd?

           func requestRewardedAd() {
               let originalType: GAAdType = .rewarded
               let adType: AdType = .rewarded
       
               GADRewardedAd.load(
                   withAdUnitID: "AD_UNIT_ID", request: GADRequest()
               ) { [weak self] (ad, error) in
                   if let error = error {
                       print("Rewarded ad failed to load with error: \(error.localizedDescription)")
                       return
                   }
                   if let ad = ad {
                       self?.rewardedAd = ad
                       self?.rewardedAd?.paidEventHandler = { adValue in
                           // Extract the impression-level ad revenue data
                           let value = adValue.value
                           let precision = adValue.precision
                           let currencyCode = adValue.currencyCode

                           // Get the ad unit ID
                           let adUnitId = ad.adUnitID

                           // Get additional response info
                           let responseInfo = ad.responseInfo
                           let loadedAdNetworkResponseInfo = responseInfo.loadedAdNetworkResponseInfo
                           let adSourceId = loadedAdNetworkResponseInfo?.adSourceID
                           let adSourceInstanceId = loadedAdNetworkResponseInfo?.adSourceInstanceID
                           let adSourceInstanceName = loadedAdNetworkResponseInfo?.adSourceInstanceName
                           let adSourceName = loadedAdNetworkResponseInfo?.adSourceName
                           let mediationGroupName = responseInfo.extrasDictionary["mediation_group_name"] as? String
                           let mediationABTestName = responseInfo.extrasDictionary["mediation_ab_test_name"] as? String
                           let mediationABTestVariant = responseInfo.extrasDictionary["mediation_ab_test_variant"] as? String

                           // Create AdRevenueInfo object
                           let adRevenueInfo = MutableAdRevenueInfo(adRevenue: value, currency: currencyCode)
                           adRevenueInfo.adType = adType
                           adRevenueInfo.adNetwork = adSourceName ?? "AdMob"
                           adRevenueInfo.adUnitID = adUnitId
                           adRevenueInfo.adPlacementID = adSourceId
                           adRevenueInfo.precision = precision.description

                           // Create payload with additional information
                           var payload: [String: String] = [
                               "original_ad_type": originalType.rawValue
                           ]
                           if let adSourceInstanceId = adSourceInstanceId {
                               payload["ad_source_instance_id"] = adSourceInstanceId
                           }
                           if let adSourceInstanceName = adSourceInstanceName {
                               payload["ad_source_instance_name"] = adSourceInstanceName
                           }
                           if let mediationGroupName = mediationGroupName {
                              payload["mediation_group_name"] = mediationGroupName
                           }
                           if let mediationABTestName = mediationABTestName {
                              payload["mediation_ab_test_name"] = mediationABTestName
                           }
                           if let mediationABTestVariant = mediationABTestVariant {
                              payload["mediation_ab_test_variant"] = mediationABTestVariant
                           }

                           adRevenueInfo.payload = payload

                           // Report to AppMetrica
                           AppMetrica.reportAdRevenue(adRevenueInfo) { error in
                               print("Failed to report ad revenue: \(error)")
                           }
                       }
                   }
                }
           }
       }
       ```

     - Objective-C

       ```objectivec translate=no
       @interface ViewController : UIViewController <GADFullScreenContentDelegate>

       @property (nonatomic, strong) GADRewardedAd *rewardedAd;

       @end

       @implementation ViewController

       - (void)requestRewardedAd {
           GAAdType originalType = GAAdTypeRewarded;
           AMAAdType adType = AMAAdTypeRewarded;
           [GADRewardedAd loadWithAdUnitID:@"AD_UNIT_ID"
                                   request:[GADRequest request]
                         completionHandler:^(GADRewardedAd * _Nullable rewardedAd, NSError * _Nullable error) {
                      
               if (error) {
                   NSLog(@"Rewarded ad failed to load with error: %@", [error localizedDescription]);
                   return;
               }

               self.rewardedAd = rewardedAd;
               __weak typeof(self) weakSelf = self; // Avoid strong reference cycles
               self.rewardedAd.paidEventHandler = ^(GADAdValue *adValue) {
                   // Extract the impression-level ad revenue data
                   NSDecimalNumber *value = adValue.value;
                   GADAdValuePrecision precision = adValue.precision;
                   NSString *currencyCode = adValue.currencyCode;
            
                   // Get the ad unit ID
                   NSString *adUnitId = weakSelf.rewardedAd.adUnitID;

                   // Create AdRevenueInfo object
                   AMAMutableAdRevenueInfo *adRevenueInfo = [[AMAMutableAdRevenueInfo alloc] initWithAdRevenue:value.doubleValue currency:currencyCode];
                   adRevenueInfo.adType = adType;
                   adRevenueInfo.adNetwork = @"AdMob";
                   adRevenueInfo.adUnitID = adUnitId;
                   adRevenueInfo.precision = [NSString stringWithFormat:@"%ld", (long)precision];
                   adRevenueInfo.payload = @{
                       @"original_ad_type": originalType
                   };
            
                   // Report to AppMetrica
                   [AMAYandexMetrica reportAdRevenue:adRevenueInfo onFailure:^(NSError *error) {
                       NSLog(@"Failed to report ad revenue: %@", error);
                   }];
               };
           }];
       }

       @end
       ```

     {% endlist %}

  #### Адаптируйте реализацию для других рекламных форматов {#send-adrevenue-format}

  1. Замените `GADRewardedAd` соответствующим классом:
  
     - Banner: `GADBannerView`
     - Interstitial: `GADInterstitialAd`
     - Native: `GADNativeAd`
     - AppOpen: `GADAppOpenAd`
  
  2. Измените `originalType` и `adType` в методе `requestRewardedAd`

     {% list tabs group=instructions %}

     - Swift

       ```swift translate=no
       // For banner ads
       let originalType: GAAdType = .banner
       let adType: AdType = .banner
       
       // For interstitial and rewarded interstitial ads
       let originalType: GAAdType = .interstitial
       let adType: AdType = .interstitial

       // For native ads
       let originalType: GAAdType = .native
       let adType: AdType = .native
       
       // For rewarded ads (current example)
       let originalType: GAAdType = .native
       let adType: AdType = .rewarded     
       
       // For app open ads
       let originalType: GAAdType = .appOpen
       let adType: AdType = .appOpen
       ```

     - Objective-C

       ```objectivec translate=no
       // For banner ads
       GAAdType originalType = GAAdTypeBanner;
       AMAAdType adType = AMAAdTypeBanner;

       // For interstitial and rewarded interstitial ads
       GAAdType originalType = GAAdTypeInterstitial;
       AMAAdType adType = AMAAdTypeInterstitial;
       
       // For native ads
       GAAdType originalType = GAAdTypeNative;
       AMAAdType adType = AMAAdTypeNative;
       
       // For rewarded ads (current example)
       GAAdType originalType = GAAdTypeRewarded;
       AMAAdType adType = AMAAdTypeRewarded;
       
       // For app open ads
       GAAdType originalType = GAAdTypeAppOpen;
       AMAAdType adType = AMAAdTypeOther;
       ```

     {% endlist %}

  3. Настройте обработчик `paidEventHandler` на соответствующем этапе процесса загрузки рекламы для каждого формата. Реализация самого обработчика остается прежней.
  4. Для баннерной рекламы установите обработчик `paidEventHandler` непосредственно в экземпляре `GADBannerView`:

     {% list tabs group=instructions %}

     - Swift

       ```swift translate=no
       bannerView.paidEventHandler = { adValue in
           // Use the same implementation as in the rewarded ad example
       }
       ```

     - Objective-C

       ```objectivec translate=no
       bannerView.paidEventHandler = ^(GADAdValue *adValue) {
           // Use the same implementation as in the rewarded ad example
       };
       ```

     {% endlist %}
  
  5. Для Interstitial, Rewarded interstitial и Native, установите обработчик `paidEventHandler` в обработчике завершения загрузки рекламы, как в примере с Rewarded.
  
  {% note info %}
  
  Не забудьте заменить `AD_UNIT_ID` на ваш реальный идентификатор рекламного блока AdMob для каждого используемого формата рекламы.
  
  {% endnote %}

- ironSource

  Данные о доходах от рекламы из ironSource SDK в AppMetrica передаются с помощью `AppMetricaIronSourceAdapter`:
  - Адаптер должен быть инициализирован до активации ironSource.
  - Порядок, в котором активируются AppMetrica и адаптер, не имеет значения, но AppMetrica следует активировать только один раз в течение жизненного цикла приложения.
  
  1. Импортируйте необходимые модули:

     {% list tabs group=instructions %}

     - Swift

       ```swift translate=no
       import AppMetricaCore
       import AppMetricaIronSourceAdapter
       import IronSource
       ```

     - Objective-C

       ```objectivec translate=no
       #import <AppMetricaCore/AppMetricaCore.h>
       #import <AppMetricaIronSourceAdapter/AppMetricaIronSourceAdapter.h>
       import <IronSource/IronSource.h>
       ```

     {% endlist %}

  2. Инициализируйте `AppMetricaIronSourceAdapter` перед активацией ironSource. Обычно это можно сделать в коде инициализации вашего приложения, например, в структуре `AppDelegate` или `main App` для приложений `SwiftUI`.

     {% list tabs group=instructions %}

     - Swift

       ```swift translate=no
       AppMetricaIronSourceAdapter.shared.initialize()
       ```

     - Objective-C

       ```objectivec translate=no
       [[AppMetricaIronSourceAdapter shared] initialize];
       ```

     {% endlist %}
  
  3. Настройте и активируйте ironSource и AppMetrica:

     {% list tabs group=instructions %}

     - Swift

       ```swift translate=no
       // Initialize IronSource
       IronSource.initWithAppKey("YOUR_IRONSOURCE_APP_KEY", adUnits: [IS_BANNER, IS_INTERSTITIAL, IS_REWARDED_VIDEO])

       // Activate AppMetrica
       guard let configuration = AppMetricaConfiguration(apiKey: "YOUR_APPMETRICA_API_KEY") else { return }
       AppMetrica.activate(with: configuration)
       ```

     - Objective-C

       ```objectivec translate=no
       // Initialize IronSource
       [IronSource initWithAppKey:@"YOUR_IRONSOURCE_APP_KEY" adUnits:@[IS_BANNER, IS_INTERSTITIAL, IS_REWARDED_VIDEO]];

       // Activate AppMetrica
       AppMetricaConfiguration *configuration = [[AppMetricaConfiguration alloc] initWithApiKey:@"YOUR_APPMETRICA_API_KEY"];
       if (configuration == nil) {
           return;
       }
       [AppMetrica activateWithConfiguration:configuration];
       ```

    {% endlist %}

  {% note info %}
  
  `AppMetricaIronSourceAdapter` автоматически передает данные о доходах от рекламы из ironSource в AppMetrica. Вам не нужно вручную сообщать о показах или доходах.
  
  {% endnote %}

- TopOn
  
  1. Импортируйте необходимые модули:

     {% list tabs group=instructions %}

     - Swift

       ```swift translate=no
       import AppMetricaCore
       import AnyThinkSDK
       import AnyThinkBanner
       import AnyThinkNative
       import AnyThinkInterstitial
       import AnyThinkRewardedVideo
       import AnyThinkMediaVideo
       ```

     - Objective-C

       ```objectivec translate=no
       #import <AppMetricaCore/AppMetricaCore.h>
       #import <AnyThinkSDK/AnyThinkSDK.h>
       import <AnyThinkBanner/AnyThinkBanner.h>
       import <AnyThinkNative/AnyThinkNative.h>
       import <AnyThinkInterstitial/AnyThinkInterstitial.h>
       import <AnyThinkRewardedVideo/AnyThinkRewardedVideo.h>
       import <AnyThinkMediaVideo/AnyThinkMediaVideo.h>
       ```

     {% endlist %}
  
  2. Создайте функцию для отправки Ad Revenue в AppMetrica:

     {% list tabs group=instructions %}

     - Swift

       ```swift translate=no
       enum ATAdType: String {
           case rewarded = "rewardedAd"
           case interstitial = "interstitialAd"
           case splash = "splashAd"
           case banner = "bannerAd"
           case native = "nativeAd"
           case mediaVideo = "mediaVideoAd"
       }
       
       func reportToAppMetrica(
           _ extra: [AnyHashable: Any], 
           placementID: String, 
           adType: AdType, 
           originalAdType: ATAdType
       ) {
           guard let revenue = extra[kATADDelegateExtraPublisherRevenueKey] as? Double,
                 let currency = extra[kATADDelegateExtraCurrencyKey] as? String else {
               print("Missing required revenue information")
               return
           }

           let adRevenueInfo = MutableAdRevenueInfo(adRevenue: NSDecimalNumber(value: revenue), currency: currency)

           adRevenueInfo.adType = adType
           adRevenueInfo.adNetwork = extra[kATADDelegateExtraNetworkNameKey] as? String
           adRevenueInfo.adUnitID = extra[kATADDelegateExtraAdunitIDKey] as? String
           adRevenueInfo.adPlacementID = placementID
           adRevenueInfo.precision = extra[kATADDelegateExtraPrecisionKey] as? String

           // Additional information in payload
           var payload: [String: String] = [
               "original_ad_type": originalAdType.rawValue
           ]
           if let networkFirmId = extra[kATADDelegateExtraNetworkFirmIdKey] as? Int {
               payload["network_firm_id"] = String(networkFirmId)
           }
           payload["adsource_id"] = extra[kATADDelegateExtraAdSourceIdKey] as? String
           // Add other relevant information to payload...

           adRevenueInfo.payload = payload

           AppMetrica.reportAdRevenue(adRevenueInfo) { error in
               print("Failed to report ad revenue to AppMetrica: \(error)")
           }
       }
       ```

     - Objective-C

       ```objectivec translate=no
       typedef NSString *ATAdType NS_TYPED_ENUM; 
       
       ATAdType ATAdTypeRewarded = @"rewardedAd";
       ATAdType ATAdTypeInterstitial = @"interstitialAd";
       ATAdType ATAdTypeSplash = @"splashAd";
       ATAdType ATAdTypeBanner = @"bannerAd";
       ATAdType ATAdTypeNative = @"nativeAd";
       ATAdType ATAdTypeMediaVideo = @"mediaVideoAd";

       - (void)reportToAppMetricaWithExtra:(NSDictionary<AnyHashable, id> *)extra 
                               placementID:(NSString *)placementID 
                                    adType:(AdType)adType
                            originalAdType:(ATAdType)originalAdType {
           NSNumber *revenue = extra[kATADDelegateExtraPublisherRevenueKey];
           NSString *currency = extra[kATADDelegateExtraCurrencyKey];

           if (revenue == nil || currency == nil) {
               NSLog(@"Missing required revenue information");
               return;
           }

           MutableAdRevenueInfo *adRevenueInfo = [[MutableAdRevenueInfo alloc] initWithAdRevenue:[NSDecimalNumber decimalNumberWithDecimal:[revenue decimalValue]] currency:currency];

           adRevenueInfo.adType = adType;
           adRevenueInfo.adNetwork = extra[kATADDelegateExtraNetworkNameKey];
           adRevenueInfo.adUnitID = extra[kATADDelegateExtraAdunitIDKey];
           adRevenueInfo.adPlacementID = placementID;
           adRevenueInfo.precision = extra[kATADDelegateExtraPrecisionKey];

           // Additional information in payload
           NSMutableDictionary<NSString *, NSString *> *payload = [NSMutableDictionary new];
           payload[@"original_ad_type"] = originalAdType;
           NSNumber *networkFirmId = extra[kATADDelegateExtraNetworkFirmIdKey];
           if (networkFirmId != nil) {
               payload[@"network_firm_id"] = [networkFirmId stringValue];
           }
           payload[@"adsource_id"] = extra[kATADDelegateExtraAdSourceIdKey];
           // Add other relevant information to payload...

           adRevenueInfo.payload = payload;

           [AppMetrica reportAdRevenue:adRevenueInfo completion:^(NSError * _Nullable error) {
               if (error) {
                   NSLog(@"Failed to report ad revenue to AppMetrica: %@", error);
               }
           }];
       }
       ```

     {% endlist %}

  3. Имплементируйте соответствующие методы делегата для каждого формата рекламы:

     {% list tabs group=instructions %}

     - Swift

       ```swift translate=no
       class YourBannerDelegate: NSObject, ATBannerDelegate {
           func bannerView(_ bannerView: ATBannerView, didShowAdWithPlacementID placementID: String, extra: [AnyHashable : Any]) {
               reportToAppMetrica(
                   extra, 
                   placementID: placementID, 
                   adType: .banner, 
                   originalAdType: .banner
               )
           }
           // Implement other delegate methods as needed
       }

       class YourNativeDelegate: NSObject, ATNativeADDelegate {
           func didShowNativeAd(in adView: ATNativeADView, placementID: String, extra: [AnyHashable : Any]) {
               reportToAppMetrica(
                   extra, 
                   placementID: placementID, 
                   adType: .native, 
                   originalAdType: .native
               )
           }
           // Implement other delegate methods as needed
       }

       class YourInterstitialDelegate: NSObject, ATInterstitialDelegate {
           func interstitialDidShow(forPlacementID placementID: String, extra: [AnyHashable : Any]) {
               reportToAppMetrica(
                   extra, 
                   placementID: placementID, 
                   adType: .interstitial, 
                   originalAdType: .interstitial
               )
           }
           // Implement other delegate methods as needed
       }

       class YourRewardedVideoDelegate: NSObject, ATRewardedVideoDelegate {
           func rewardedVideoDidShow(forPlacementID placementID: String, extra: [AnyHashable : Any]) {
               reportToAppMetrica(
                   extra, 
                   placementID: placementID, 
                   adType: .rewarded, 
                   originalAdType: .rewarded
               )
           }
           // Implement other delegate methods as needed
       }

       class YourSplashDelegate: NSObject, ATSplashDelegate {
           func splashDidShow(forPlacementID placementID: String, extra: [AnyHashable : Any]) {
               reportToAppMetrica(
                   extra, 
                   placementID: placementID, 
                   adType: .other, 
                   originalAdType: .splash
               )
           }
           // Implement other delegate methods as needed
       }

       class YourMediaVideoDelegate: NSObject, ATMediaVideoDelegate {
           func mediaVideoDidStartPlaying(forPlacementID placementID: String, extra: [AnyHashable : Any]) {
               reportToAppMetrica(
                   extra, 
                   placementID: placementID, 
                   adType: .other, 
                   originalAdType: .mediaVideo
               )
           }
           // Implement other delegate methods as needed
       }
       ```

     - Objective-C

       ```objectivec translate=no
       #import <AppMetricaCore/AppMetricaCore.h>
       #import <AnyThinkSDK/AnyThinkSDK.h>
       import <AnyThinkBanner/AnyThinkBanner.h>
       import <AnyThinkNative/AnyThinkNative.h>
       import <AnyThinkInterstitial/AnyThinkInterstitial.h>
       import <AnyThinkRewardedVideo/AnyThinkRewardedVideo.h>
       import <AnyThinkMediaVideo/AnyThinkMediaVideo.h>
       ```

     {% endlist %}

- Настройка для других систем
  
  1. Инициализируйте объект `MutableAdRevenueInfo`.
  2. Отправьте объект `MutableAdRevenueInfo` на основной API key с помощью метода `+reportAdRevenue:onFailure:` класса `AppMetrica`.
  
     {% list tabs group=instructions %}

     - Swift

       ```swift translate=no
       AppMetrica.report(adRevenue: adRevenueInfo) { error in
           print("AdRevenue error: \(error)")
       }
       ```

     - Objective-C

       ```objectivec translate=no
       [AMAAppMetrica reportAdRevenue:[adRevenueInfo copy] onFailure:^(NSError *error) {
           NSLog(@"AdRevenue error: %@", error);
       }];

       ```

     {% endlist %}

{% endlist %}

### Шаг 3. Убедитесь, что Ad Revenue отображается в отчетах {#send-adrevenue-check-reports}

1. Совершите просмотры рекламы в приложении.

2. Убедитесь, что в отчете [In-app и Ad Revenue](../../../mobile-reports/revenue-report.md) количество событий Ad Revenue соответствует количеству просмотров рекламы.

## Установка длительности тайм-аута сессии {#session-timeout}

По умолчанию длительность таймаута сессии равна 10 секундам. Это минимально допустимое значение свойства `sessionTimeout`.

{% list tabs group=instructions %}

  - Swift

    Чтобы изменить длительность таймаута, передайте значение в секундах в свойство `sessionTimeout` конфигурации `AppMetricaConfiguration`.

    ```swift translate=no
    // Creating an extended library configuration.
    if let configuration = AppMetricaConfiguration(apiKey: "API key") {
        // Setting the session timeout.
        configuration.sessionTimeout = 15
        // Initializing the AppMetrica SDK.
        AppMetrica.activate(with: configuration)
    }
    ```

  - Objective-C

    Чтобы изменить длительность таймаута, передайте значение в секундах в свойство `sessionTimeout` конфигурации `AMAAppMetricaConfiguration`.

    ```obj-c translate=no
    // Creating an extended library configuration.
    AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithAPIKey:@"API key"];
    // Setting the session timeout.
    configuration.sessionTimeout = 15;
    // Initializing the AppMetrica SDK.
    [AMAAppMetrica activateWithConfiguration:configuration];
    ```

{% endlist %}

## Установка версии приложения {#version-app}

По умолчанию версия приложения задается в файле Info.plist (`CFBundleShortVersionString`).

{% list tabs group=instructions %}

  - Swift

    Чтобы указать версию приложения из кода, передайте версию приложения в свойство `appVersion` конфигурации `AppMetricaConfiguration`.

    ```swift translate=no
    // Creating an extended library configuration.
    if let configuration = AppMetricaConfiguration(apiKey: "API key") {
        // Setting the app version.
        configuration.appVersion = "1.13.2"
        // Initializing the AppMetrica SDK.
        AppMetrica.activate(with: configuration)
    }
    ```

  - Objective-C

    Чтобы указать версию приложения из кода, передайте версию приложения в свойство `appVersion` конфигурации `AMAAppMetricaConfiguration`.

    ```obj-c translate=no
    // Creating an extended library configuration.
    AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithAPIKey:@"API key"];
    // Setting the app version.
    configuration.appVersion = @"1.13.2";
    // Initializing the AppMetrica SDK.
    [AMAAppMetrica activateWithConfiguration:configuration];
    ```

{% endlist %}

## Отслеживание открытий приложения с помощью deeplink {#deeplink}

{% include notitle [tracking-deplink](../../../_includes/tracking-deeplink.md) %}

См. также [Как создать ремаркетинг-кампанию в AppMetrica](../../../troubleshooting/troubleshooting.md#remarketing-campaign).

## Учет новых пользователей {#new-user}

По умолчанию в момент первого запуска приложения все пользователи определяются как новые. Если AppMetrica SDK подключается к приложению, у которого уже есть активные пользователи, то для корректного отслеживания статистики можно настроить учет новых и старых пользователей.

{% list tabs group=instructions %}

  - Objective-C

    Для этого необходимо инициализировать AppMetrica SDK, используя расширенную стартовую конфигурацию `AMAAppMetricaConfiguration`.

    ```obj-c translate=no
    BOOL isFirstLaunch = NO;
    // Creating an extended library configuration.
    AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithAPIKey:@"API key"];
    // Implement the logic for detecting whether the app is starting for the first time.
    // For example, you can check for files (settings, databases, and so on),
    // which the app creates on its first launch.
    if (conditions) {
        isFirstLaunch = YES;
    }
    configuration.handleFirstActivationAsUpdate = !isFirstLaunch;
    // Initializing the AppMetrica SDK.
    [AMAAppMetrica activateWithConfiguration:configuration];
    ```

  - Swift

    Для этого необходимо инициализировать AppMetrica SDK, используя расширенную стартовую конфигурацию `AppMetricaConfiguration`.

    ```swift translate=no
    var isFirstLaunch = false
    // Creating an extended library configuration.
    guard let configuration = AppMetricaConfiguration(apiKey: "API key") else {
        print("AppMetricaConfiguration initialization failed.")
        return // or return someDefaultValue or throw someError
    }
    // Implement the logic for detecting whether the app is starting for the first time.
    // For example, you can check for files (settings, databases, and so on),
    // which the app creates on its first launch.
    if conditions {
        isFirstLaunch = true
    }
    configuration.handleFirstActivationAsUpdate = !isFirstLaunch
    // Initializing the AppMetrica SDK.
    AppMetrica.activate(with: configuration)
    ```    

{% endlist %}

## Отключение и включение отправки статистики {#stat}

Если для отправки статистических данных требуется согласие пользователя, необходимо инициализировать библиотеку с отключенной опцией отправки статистики.

{% list tabs group=instructions %}

  - Objective-C

    Для этого установите значение `NO` для свойства `dataSendingEnabled` конфигурации `AMAAppMetricaConfiguration`.

    ```obj-c translate=no
    // Creating an extended library configuration.
    AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithAPIKey:@"API key"];
    // Disabling sending statistics.
    configuration.dataSendingEnabled = NO;
    // Initializing the AppMetrica SDK.
    [AMAAppMetrica activateWithConfiguration:configuration];
    ```

    После того как пользователь дал согласие на отправку статистики (например, в настройках приложения или в соглашении при первом открытии), необходимо включить отправку с помощью метода `+setDataSendingEnabled:` класса `AMAAppMetrica`.

    ```obj-c translate=no
    // Checking the status of the boolean variable. It shows the user confirmation.
    if (flag) {
        // Enabling sending statistics.
        [AMAAppMetrica setDataSendingEnabled:YES];
    }
    ```

  - Swift

    Для этого установите значение `false` для свойства `dataSendingEnabled` конфигурации `AppMetricaConfiguration`.

    ```swift translate=no
    // Creating an extended library configuration.
    if let configuration = AppMetricaConfiguration(apiKey: "API key") {
        // Disabling sending statistics.
        configuration.dataSendingEnabled = false
        // Initializing the AppMetrica SDK.
        AppMetrica.activate(with: configuration)
    }
    ```

    После того как пользователь дал согласие на отправку статистики (например, в настройках приложения или в соглашении при первом открытии), необходимо включить отправку с помощью метода `setDataSendingEnabled(_:)` класса `AppMetrica`.

    ```swift translate=no
    // Checking the status of the boolean variable. It shows the user confirmation.
    if flag {
        // Enabling sending statistics.
        AppMetrica.setDataSendingEnabled(true);
    }
    ```

{% endlist %}

### Пример оповещения {#stat-alert-example}

Для информирования пользователей вы можете использовать любой текст. Например:

> Это приложение использует сервис аналитики AppMetrica, предоставляемый компанией ООО «ЯНДЕКС», 119021, Россия, Москва, ул. Л. Толстого, 16 (далее — Яндекс) на [Условиях использования сервиса](https://yandex.ru/legal/metrica_termsofuse/).
>
> AppMetrica анализирует данные об использовании приложения, в том числе об устройстве, на котором оно функционирует, источнике установки, составляет конверсию и статистику вашей активности в целях продуктовой аналитики, анализа и оптимизации рекламных кампаний, а также для устранения ошибок. Собранная таким образом информация не может идентифицировать вас.
>
> Информация об использовании вами данного приложения, собранная при помощи инструментов AppMetrica, в обезличенном виде будет передаваться Яндексу и храниться на сервере Яндекса в ЕС и Российской Федерации. Яндекс будет обрабатывать эту информацию для предоставления статистики использования вами приложения, составления для нас отчетов о работе приложения, и предоставления других услуг.

## Получение различных идентификаторов AppMetrica SDK {#get-ids}

Чтобы получить различные идентификаторы AppMetrica SDK (`DeviceId`, `DeviceIdHash`, `UUID`) используйте метод `requestStartupIdentifiersWithKeys()` / `requestStartupIdentifiers()`. Для получения `appmetrica_device_id` нужно запрашивать `DeviceIdHash`.

{% list tabs group=instructions %}

- Objective-C

  ```obj-c translate=no
  AMAIdentifiersCompletionBlock block = ^(NSDictionary<AMAStartupKey,id> * _Nullable identifiers, NSError * _Nullable error) {
      if (identifiers[kAMADeviceIDHashKey] != nil) {
          NSLog(@"deviceIDHash = %@", identifiers[kAMADeviceIDHashKey]);
      }
      if (identifiers[kAMADeviceIDKey] != nil) {
          NSLog(@"deviceID = %@", identifiers[kAMADeviceIDKey]);
      }
      if (identifiers[kAMAUUIDKey] != nil) {
          NSLog(@"uuid = %@", identifiers[kAMAUUIDKey]);
      }
  };
  [AMAAppMetrica requestStartupIdentifiersWithKeys:@[kAMADeviceIDHashKey, kAMADeviceIDKey, kAMAUUIDKey] completionQueue:nil completionBlock:block];
  ```  

- Swift

  ```swift translate=no
  // Specifying the keys for which we need to get identifiers
  let keys: [StartupKey] = [StartupKey.deviceIDKey, StartupKey.deviceIDHashKey, StartupKey.uuidKey]

  // Specifying the queue on which the completion handler will be executed (for example, the main thread)
  let queue = DispatchQueue.main

  // Requesting IDs
  AppMetrica.requestStartupIdentifiers(for: keys, on: queue) { identifiers, error in
      if let error = error {
          print("Произошла ошибка: \(error.localizedDescription)")
      } else if let identifiers = identifiers {
          // Processing the received IDs
          if let deviceIDHash = identifiers[StartupKey.deviceIDHashKey] as? String {
              print("AppMetrica deviceIDHash: \(deviceIDHash)")
          }
          if let deviceID = identifiers[StartupKey.deviceIDKey] as? String {
              print("AppMetrica deviceID: \(deviceID)")
          }
          if let uuid = identifiers[StartupKey.uuidKey] as? String {
              print("AppMetrica uuid: \(uuid)")
          }
      }
  }  
  ```

{% endlist %}

{{ feedback }}		

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}

[*ремаркетинг-кампаний]: Рекламная кампания, которая направлена на возвращение пользователей в установленное приложение. Подробнее о создании ремаркетинг-кампании в разделе [Создание ремаркетинг-трекера](../../../mobile-tracking/add-remarketing-tracker.md).
