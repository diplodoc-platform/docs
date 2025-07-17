# Предупреждение о сборе данных

Вы можете предупредить пользователей вашего приложения о сборе данных и инициализировать библиотеку с отключенной отправкой статистики до получения согласия. Ниже описаны этапы отключения и включения сбора статистики:

{% list tabs %}

- Android

  Чтобы инициализировать библиотеку с отключенной отправкой статистики, передайте значение `false` в метод `withStatisticsSending(boolean value)` при создании расширенной конфигурации библиотеки.
  
  ```java translate=no
  // Creating an extended library configuration.
  AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_key)
          // Disabling sending statistics.
          .withStatisticsSending(false)
          .build();
  // Initializing the AppMetrica SDK.
  AppMetrica.activate(getApplicationContext(), config);
  ```
  
  После того как пользователь дал согласие на отправку статистики (например, в настройках приложения или в соглашении при первом открытии), включите отправку статистики с помощью метода `AppMetrica.setStatisticsSending(Context context, boolean enabled)`:

  ```java translate=no
  // Checking the status of the boolean variable. It shows the user confirmation.
  if (flag) {
      // Enabling sending statistics.
      AppMetrica.setStatisticsSending(getApplicationContext(), true);
  }
  ```

- iOS (Objective-C)

  Чтобы инициализировать библиотеку с отключенной отправкой статистики, установите значение `NO` для свойства `statisticsSending` конфигурации `YMMYandexMetricaConfiguration`.
  
  ```objectivec translate=no
  // Creating an extended library configuration.
  YMMYandexMetricaConfiguration *configuration = [[YMMYandexMetricaConfiguration alloc] initWithApiKey:@"API_key"];
  // Disabling sending statistics.
  configuration.statisticsSending = NO;
  // Initializing the AppMetrica SDK.
  [YMMYandexMetrica activateWithConfiguration:configuration];
  ```
  
  После того как пользователь дал согласие на отправку статистики (например, в настройках приложения или в соглашении при первом открытии), включите отправку статистики с помощью метода `+setStatisticsSending:` класса `YMMYandexMetrica`.

  ```objectivec translate=no
  // Checking the status of the boolean variable. It shows the user confirmation.
  if (flag) {
      // Enabling sending statistics.
      [YMMYandexMetrica setStatisticsSending:YES];
  }
  ```

- iOS (Swift)

  Чтобы инициализировать библиотеку с отключенной отправкой статистики, установите значение `NO` для свойства `statisticsSending` конфигурации `YMMYandexMetricaConfiguration`.
  
  ```swift translate=no
  // Creating an extended library configuration.
  let configuration = YMMYandexMetricaConfiguration.init(apiKey: "API key")
  // Disabling sending statistics.
  configuration?.statisticsSending = false
  // Initializing the AppMetrica SDK.
  YMMYandexMetrica.activate(with: configuration!)
  ```
  
  После того как пользователь дал согласие на отправку статистики (например, в настройках приложения или в соглашении при первом открытии), необходимо включить отправку с помощью метода `setStatisticsSending(_:)` класса `YMMYandexMetrica`.

  ```swift translate=no
  // Checking the status of the boolean variable. It shows the user confirmation.
  if flag {
      // Enabling sending statistics.
      YMMYandexMetrica.setStatisticsSending(true);
  }
  ```

{% endlist %}

## Пример оповещения {#example-section}

Для информирования пользователей вы можете использовать любой текст. Например:

> Это приложение использует сервис аналитики AppMetrica (Яндекс.Метрика для приложений), предоставляемый компанией ООО «ЯНДЕКС», 119021, Россия, Москва, ул. Л. Толстого, 16 (далее — Яндекс) на [Условиях использования сервиса](https://yandex.ru/legal/metrica_termsofuse/).
> 
> AppMetrica анализирует данные об использовании приложения, в том числе об устройстве, на котором оно функционирует, источнике установки, составляет конверсию и статистику вашей активности в целях продуктовой аналитики, анализа и оптимизации рекламных кампаний, а также для устранения ошибок. Собранная таким образом информация не может идентифицировать вас.
> 
> Информация об использовании вами данного приложения, собранная при помощи инструментов AppMetrica, в обезличенном виде будет передаваться Яндексу и храниться на сервере Яндекса в ЕС и Российской Федерации. Яндекс будет обрабатывать эту информацию для предоставления статистики использования вами приложения, составления для нас отчетов о работе приложения, и предоставления других услуг.

## См. также

- [Соответствие Генеральному регламенту о защите данных (GDPR)](gdpr.md)
- [Соответствие ISO / IEC-27001](iso-27001.md)
- [Маскировка IP-адреса](ip-masking.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
