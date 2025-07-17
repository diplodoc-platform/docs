# Поддержка детских приложений (iOS)

Если ваше приложение относится к категории детских приложений, используйте свойство `appForKids` конфигурации `YMMYandexMetricaConfiguration`. Свойство определяет тип приложения как "детский", чтобы соответствовать [правилам проверки детских приложений](https://developer.apple.com/app-store/review/guidelines/#kids).

{% list tabs group=instructions %}

- Objective-C
  
  ```objectivec translate=no
  - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
  {
      // Creating an extended library configuration.
      YMMYandexMetricaConfiguration *configuration = [[YMMYandexMetricaConfiguration alloc] initWithApiKey:@"API_key"];
      // Setting up the configuration.
      configuration.appForKids = YES;
      ...
      // Initializing the AppMetrica SDK.
      [YMMYandexMetrica activateWithConfiguration:configuration];
  }
  ```

- Swift
  
  ```swift translate=no
  func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey : AnyObject]? = nil) -> Bool {
      // Creating an extended library configuration.
      let configuration = YMMYandexMetricaConfiguration.init(apiKey: "API key")
      // Setting up the configuration.
      configuration?.appForKids = true
      ...
      // Initializing the AppMetrica SDK.
      YMMYandexMetrica.activate(with: configuration!) 
      return true
  }
  ```

{% endlist %}

{% note info %}

Если опция включена, AppMetrica SDK не отправляет рекламные идентификаторы и информацию о местоположении.

{% endnote %}

## См. также

- [Соответствие ISO / IEC-27001](iso-27001.md)
- [Маскировка IP-адреса](ip-masking.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
