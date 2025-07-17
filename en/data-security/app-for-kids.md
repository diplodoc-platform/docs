# Support for children's apps (iOS)

If you have an app for kids, use the `appForKids` property of the `YMMYandexMetricaConfiguration` configuration. This property defines the application type as "children's" to match the [rules for checking children's apps](https://developer.apple.com/app-store/review/guidelines/#kids).

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

If this option is enabled, the AppMetrica SDK doesn't send advertising IDs or location information.

{% endnote %}

## See also

- [ISO/IEC 27001 compliance](iso-27001.md)
- [Masking the IP address](ip-masking.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
